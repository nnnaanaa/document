# ネットワークスペシャリスト 午後対策ノート

IPA ネットワークスペシャリスト試験の午後（記述式）に向けて作った暗記シートです。

- 各分野の **暗記シート** に、しくみ・図（Mermaid）・試験でよく問われるポイント・答えの型をまとめています
- **直前シート** は、暗記シートから要点と答えの型だけを抜き出した、1枚1画面の短い版です
- 図は Mermaid で書いているので、GitHub 上でそのまま表示されます

## 直前シート（要点と答えの型だけ）

| シート | 内容 |
| --- | --- |
| [サブネット計算 直前シート](network/final/subnet.md) | 公式・ブロック幅・例 |
| [IPv6 直前シート](network/final/ipv6.md) | アドレス・NDP・PMTUD・移行技術の要点 |
| [L2 冗長化 直前シート](network/final/l2-redundancy.md) | STP/RSTP・エッジポート・LAG の要点 |
| [VXLAN 直前シート](network/final/vxlan.md) | VNI・MTU・Leaf-Spine・EVPN の要点 |
| [無線LAN 直前シート](network/final/wifi.md) | 規格・DFS・CSMA/CA・WPA3・802.1X の要点 |
| [IPsec 直前シート](network/final/ipsec.md) | ESP/IKE・SA・NAT トラバーサル・MSS の要点 |
| [SD-WAN 直前シート](network/final/sd-wan.md) | コントローラ・アプリ別経路・ブレイクアウトの要点 |
| [OSPF 直前シート](network/final/ospf.md) | コスト・DR/BDR・エリア・LSA の要点 |
| [BGP 直前シート](network/final/bgp.md) | iBGP/eBGP・属性・経路制御の要点 |
| [マルチキャスト 直前シート](network/final/multicast.md) | アドレス・IGMP・PIM・RPF の要点 |
| [VRRP 直前シート](network/final/vrrp.md) | マスタ選出・GARP・トラッキングの要点 |
| [負荷分散・プロキシ 直前シート](network/final/lb-proxy.md) | セッション維持・DSR・GSLB・プロキシの要点 |
| [運用・監視 直前シート](network/final/ops-monitoring.md) | SNMP・Syslog・フロー情報の要点 |
| [計算問題 直前シート](network/final/calculation.md) | 公式と覚えておく数 |
| [TCP・QoS 直前シート](network/final/tcp-qos.md) | MSS・再送・輻輳制御・マーキングの要点 |
| [DHCP・NAT 直前シート](network/final/dhcp-nat.md) | 4つのメッセージ・リレー・NAPT の要点 |
| [DNS 直前シート](network/final/dns.md) | レコード・TTL・ゾーン転送・攻撃と対策の要点 |
| [メール 直前シート](network/final/mail.md) | ポート・SPF/DKIM/DMARC の要点 |
| [IoT 直前シート](network/final/iot.md) | LPWA・MQTT・CoAP の要点 |
| [認証・PKI 直前シート](network/final/auth-pki.md) | 証明書・TLS・RADIUS・Kerberos・SAML の要点 |
| [セキュリティ 直前シート](network/final/security.md) | FW・DMZ・IPS・DoS・標的型攻撃の要点 |

## IP アドレス

| シート | 内容 |
| --- | --- |
| [サブネット計算暗記シート](network/ip-address/subnet-cheatsheet.md) | サブネット計算の公式・早見表まとめ |
| [サブネット計算の実例](network/ip-address/ipaddr.md) | サブネットマスク計算の実例2パターン |
| [IPv6 暗記シート](network/ip-address/ipv6.md) | IPv6のアドレス・NDP・SLAAC/DHCPv6・移行技術まとめ |

## LAN・L2

| シート | 内容 |
| --- | --- |
| [イーサネット規格](network/lan/ethernet-types.md) | 10BASE-T等イーサネット規格と伝送速度 |
| [PoE](network/lan/poe.md) | PoE規格(802.3af/at/bt)と給電電力 |
| [IEEE 802.X 規格一覧](network/lan/ieee802x.md) | 試験に頻出するIEEE802.X規格一覧 |
| [LAG・STP](network/lan/lag-stp.md) | LAGとSTP(ポート役割/ステータス/RSTP/MSTP) |
| [L2 冗長化 暗記シート](network/lan/l2-redundancy.md) | ループ・STP/RSTP/MSTP・リンクアグリゲーション・スタックまとめ |
| [VXLAN 暗記シート](network/lan/vxlan.md) | VXLANのヘッダ・MTU・Leaf-Spine・EVPN・ESIまとめ |
| [無線LAN 暗記シート](network/lan/wifi-cheatsheet.md) | 規格・チャネル/DFS・CSMA/CA・WPA3/802.1X・WLC・ローミングまとめ |

## WAN・VPN

| シート | 内容 |
| --- | --- |
| [WAN・VPNの分類](network/wan-vpn/wan-vpn.md) | WAN/VPNの分類とインターネット経由の有無 |
| [IP-VPN・MPLS](network/wan-vpn/mpls.md) | IP-VPNを支えるMPLSのラベル転送と用語 |
| [IPsec 暗記シート](network/wan-vpn/ipsec.md) | ESP/IKE・SA・モード・NATトラバーサル・MSS調整・冗長化と答えの型まとめ |
| [PPP・PPPoE](network/wan-vpn/ppp.md) | PPPの認証(PAP/CHAP)とPPPoEのフレーム構造 |
| [SD-WAN 暗記シート](network/wan-vpn/sd-wan.md) | SD-WANの構成・アプリ別経路制御・ローカルブレイクアウト・SASEまとめ |

## ルーティング

| シート | 内容 |
| --- | --- |
| [OSPF 暗記シート](network/routing/ospf.md) | OSPFのコスト・ネイバー・DR/BDR・エリア・LSA・集約まとめ |
| [BGP 暗記シート](network/routing/bgp-cheatsheet.md) | iBGP/eBGP・最適経路の選択・経路制御・セキュリティまとめ |
| [ECMP・BFD](network/routing/reliability.md) | ECMPによる負荷分散とBFDの死活監視 |
| [マルチキャスト 暗記シート](network/routing/multicast.md) | アドレス・MAC対応・IGMP・IGMPスヌーピング・PIM・RPFまとめ |

## 冗長化・負荷分散

| シート | 内容 |
| --- | --- |
| [VRRP 暗記シート](network/redundancy/vrrp.md) | 仮想IP/MAC・マスタ選出・切替え・トラッキング・プリエンプトまとめ |
| [負荷分散・プロキシ 暗記シート](network/redundancy/lb-proxy.md) | セッション維持・ヘルスチェック・DSR・GSLB・プロキシ・CDNまとめ |

## 運用管理

| シート | 内容 |
| --- | --- |
| [QoS](network/operation/qos.md) | 帯域/優先度制御・DiffServ・CoS/DSCP |
| [運用・監視 暗記シート](network/operation/ops-monitoring.md) | SNMP・Syslog・NTP・フロー情報・ミラーポート・障害の切り分けまとめ |
| [計算問題 暗記シート](network/operation/calculation.md) | 伝送時間・稼働率・待ち行列・呼量・VoIP帯域などの公式と例題 |

## プロトコル

| シート | 内容 |
| --- | --- |
| [TCP・QoS 暗記シート](network/protocol/tcp-qos.md) | 再送・フロー/輻輳制御・MSS・マーキング・シェーピングまとめ |
| [UDP](network/protocol/udp.md) | UDPヘッダ構造(8Byte固定) |
| [ウェルノウンポート](network/protocol/well-known-ports.md) | 代表的なポート番号と用途の一覧 |
| [DHCP・NAT 暗記シート](network/protocol/dhcp-nat.md) | 4つのメッセージ・リレー・スヌーピング・NAPT・ヘアピンNATまとめ |
| [DNS 暗記シート](network/protocol/dns.md) | 名前解決・レコード・TTL・構成・DNSへの攻撃と対策まとめ |
| [HTTP](network/protocol/http.md) | ステータスコード・ヘッダー・認証方式 |
| [TLS](network/protocol/tls.md) | TLS1.2/1.3のネゴシエーション比較 |
| [電子メールのヘッダ](network/protocol/email-header.md) | 電子メールヘッダの構造と偽装可能性 |
| [送信ドメイン認証](network/protocol/mail-security.md) | SPF/DKIM/DMARCによる送信ドメイン認証 |
| [メール 暗記シート](network/protocol/mail.md) | SMTP・MX・エンベロープ・OP25B・SPF/DKIM/DMARCまとめ |
| [VoIP](network/protocol/voip.md) | VoIPのSIP/RTPによる通話の流れと音声符号化 |
| [IoT 暗記シート](network/protocol/iot.md) | LPWA（LTE-M・NB-IoT・LoRaWAN）・MQTT・CoAPまとめ |

## セキュリティ

| シート | 内容 |
| --- | --- |
| [認証・PKI 暗記シート](network/security/auth-pki.md) | 暗号・証明書・TLS・RADIUS/802.1X・Kerberos・SAML/OAuthまとめ |
| [セキュリティ 暗記シート](network/security/security.md) | FW・DMZ・NAT・IDS/IPS・DoS・標的型攻撃と対策まとめ |

## 復習

| シート | 内容 |
| --- | --- |
| [午後 単語集の復習](network/review/gogo-miss.md) | 一問一答で間違えた問題の答えと覚え方（四択問題で繰り返せる） |
