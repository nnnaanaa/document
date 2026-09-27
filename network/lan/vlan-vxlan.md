# VLAN-VXLAN.md
## IEEE 802.1Q タグVLAN と VXLAN

***

## IEEE 802.1Q タグVLANフレーム

```
| 宛先MAC | 送信元MAC | タグVLANヘッダ | タイプ | データ |
                          └ | TPID | PCP | CFI/DEI | VID |
```

| フィールド | 詳細 |
| --- | --- |
| **TPID** (Tag Protocol Identifier) | IEEE802.1Q形式のフレームであることを示す情報が入る。**固定で 0x8100** となり、フレームがIEEE 802.1Qのタグ付きフレームであることを示す |
| **PCP** (Priority Code Point) | QoSで使用する優先度の情報が入る。トラフィックの**優先順位（0〜7）**を指定 |
| CFI (Canonical Format Indicator) / DEI (Drop Eligibility Indicator) | MACアドレスのフォーマットを示す情報が入る |
| **VID** (VLAN Identifier) | VLAN IDが入る。**12bit で 0〜4095（2^12=4096）**の値が入る |

PCPを使った優先度制御（CoS）は [../operation/qos.md](../operation/qos.md) を参照。

***

## VXLAN の概要

**VXLAN** (Virtual Extensible Local Area Network)

* **L3ネットワーク上に仮想的なL2ネットワークを構築**するためのトンネリングプロトコル
* **24bit の VNI** (VXLAN Network Identifier) により**約1,677万（2^24=16,777,216）以上**のL2ネットワークを識別可能
  * 対応できるネットワーク数が VLAN の 4096（2^12）よりも多い

**VTEP** (VXLAN Tunnel Endpoint)

* VXLAN対応のスイッチ又はインターフェースを指し、**VXLANトンネルを終端する**役割を持つ
* インターフェース障害に対応するために、**Loopback Interface に VTEP アドレスを割り当てる**ことが多い
* 物理スイッチや、ハイパーバイザー/OS上の仮想スイッチがVTEPとなる場合が多い

```
Server ─ VTEP ═══ L3ネットワーク ═══ VTEP ─ Server
Original Frame → [Outer Ethernet | Outer IP | Outer UDP | VXLAN Header(VNI) | Original Frame] → Original Frame
```

VXLAN Header でカプセル化することで、**L3ネットワーク上でL2のEthernet Frameを転送**できる。

## VXLAN によるカプセル化

* **L3ネットワーク上を転送するため**に、Original Frame（元のフレーム）を VXLANヘッダー、UDPヘッダー、IPヘッダー、Ethernetヘッダーで**カプセル化**する
* **UDP 4789 port** を利用するのが一般的

| Outer Ethernet Header | Outer IP Header | Outer UDP Header | **VXLAN Header** | Original Frame |
| --- | --- | --- | --- | --- |
| VXLANでカプセル化 | ← | ← | ← | 元のフレーム |

VXLAN Header の詳細: `Flags | Reserved | VNI (VXLAN ID) | Reserved`

VNI以外のヘッダーは簡単なフラグや予約済みフィールドであるため、基本意識しないでOK。

## VXLAN の利用シーン

* VXLANは主に**データセンター**ネットワークで利用されることが多い
* データセンターに**複数テナント（顧客）**を収容する場合、テナント間でIPアドレス範囲の重複が生じるが、割り当てる **VNI を分けることでIPアドレスが競合することなく複数テナント間の通信を転送可能**

【参考】データセンターではServer間の通信が多く、効率よく捌ける **Leaf-Spine 構成**をとることが多い。各Leafスイッチは全てのSpineスイッチに接続され、逆に各Spineスイッチも全てのLeafスイッチに接続される。

例）Server01〜03 の上に 顧客A (VNI 01): VM01〜03 = 10.0.0.1〜3、顧客B (VNI 11): VM11〜13 = 10.0.0.1〜3 が同居していても、VNIが異なるため競合しない。

## VTEP と VM の紐づけ（Control Plane）

VXLANは**あくまでトンネリングプロトコル（Data Plane）**であるため、どのVTEP配下にどのVMが所属するかを把握する手段（Control Plane）が必要。

主な Control Plane は以下の2つ。

| 方式 | 紐づけの学習方法 |
| --- | --- |
| **Flood & Learn** | **Multicast** を使用して VTEP と VM の紐づけを学習 |
| **EVPN** (Ethernet VPN) | **MP-BGP** (Multi Protocol BGP) を使用して VTEP と VM の紐づけを学習 |

紐づけ学習テーブルの例: `VNI01 - VM01 - VTEP01`, `VNI01 - VM02 - VTEP02`, …

### Flood & Learn

* フラッディングが発生するフェーズ: **初回通信時 / BUMトラフィック**
* **VNI毎に Multicast Group を定義**し、VTEPとVMの紐づけの学習やBUMの転送を行う方式

| 項目 | 方法 |
| --- | --- |
| VTEPとVMの紐づけ学習 | **Multicast**: 配下のVMからのARP要求を Local VTEP が学習し、さらにそれを Remote VTEP に転送して Remote VTEP でも学習（**マルチキャストによる通信が発生**） |
| Unicast Traffic の転送 | **Unicast**: 学習した紐づけに従いVMが存在するVTEPに対して送信 |
| BUM Traffic の転送 | **Multicast**: 定義した Multicast Group 宛に送信 |

**BUM** = **B**roadcast + **U**nknown-Unicast + **M**ulticast（Flooding で転送される Traffic の総称）

| 種類 | 内容 |
| --- | --- |
| Broadcast | 全てのノードに送信されるトラフィック（例: ARPリクエスト） |
| Unknown Unicast | 宛先が不明なユニキャスト通信。宛先情報が不明なときにフラッディングされる |
| Multicast | 特定のマルチキャストグループに対して送信されるトラフィック |

### EVPN (Ethernet VPN)

* **MP-BGP** (Multi Protocol BGP) を使用して VTEP と VM の紐づけを学習するVXLANの方式。**EVPN-VXLAN** とも
* VXLAN通信に必要な情報を交換できるよう拡張された BGP (MP-BGP) を利用する

| 項目 | 方法 |
| --- | --- |
| VTEPとVMの紐づけ学習 | **MP-BGP**: VMからARP要求を受信したVTEPは、このリクエストをBGPのルート情報に変換し、MP-BGPによりBGP Peerに紐づけ情報を広報（**BGP経由なのでマルチキャストを使わない**） |
| Unicast Traffic の転送 | **Unicast**: 学習した紐づけに従いVMが存在するVTEPに対して送信 |
| BUM Traffic の転送 | **Multicast or Unicast**: Flood & Learn と同様に定義した Multicast Group 宛に送信 <Multicast> / **Ingress Replication** 機能で必要なVTEPのみにUnicast通信を複製して送信 <Unicast> |

VTEPとVMの紐づけを学習する際、**Flood & Learn 方式と違い最初に宛先が分からない場合でも Multicast 通信が生じない**ため、効率的に VXLAN ネットワークを構築、維持できる。

関連: [lag-stp.md](lag-stp.md) / [../routing/bgp.md](../routing/bgp.md)
