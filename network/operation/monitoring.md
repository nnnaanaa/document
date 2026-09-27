# MONITORING.md
## ネットワークの監視（LLDP / SNMP / Syslog / NetFlow・IPFIX）

***

## 機器情報の通知 - LLDP

**LLDP** (Link Layer Discovery Protocol)
* 隣接する機器に対して**自身の機器情報を通知**するための **L2** プロトコル
* **IEEE802.1ab** で標準化 / **マルチキャストMACアドレス 01:80:C2:00:00:0E** を利用
* 自動でネットワーク構成を把握したり、トラブルシューティングのために利用できる
* 交換する情報の例: デバイスID, Port ID, デバイス名, ポート状態, 管理アドレス … 等

LLDPの情報を基にネットワークマップを作成するような製品も存在する。

## ネットワークの監視

| プロトコル | 概要 | ポート |
| --- | --- | --- |
| **SNMP** (Simple Network Management Protocol) | ネットワーク経由で**機器の監視や制御**をするためのプロトコル。SNMP Manager が各 SNMP Agent から機器の状態を収集したり、設定変更を適用する | **UDP/161** (Manager → Agent)、**UDP/162** (Agent → Manager) |
| **Syslog** | ネットワーク経由で**ログを転送**するためのプロトコル。監視対象の機器は Syslog サーバ宛にログを転送する | 一般的には **UDP/514** |
| **NetFlow / IPFIX** (Internet Protocol Flow Information Export) | ネットワークを流れる**フロー（IP, Protocol, Port 等の組み合わせ）を監視/分析**するためのプロトコル。**コレクタ**に**エクスポーター（一般的にはネットワーク機器）**からのフロー情報を集約する。NetFlow は Cisco によって開発され、その拡張版として IPFIX が標準化された | NetFlow では UDP/9985 が多く、**IPFIX は UDP/4739 or TCP/4739** が多く利用される |

SNMPとSyslogは機器の監視に特化、NetFlow/IPFIXはフローの監視や分析に特化。

## SNMP と MIB

**SNMP**
* ネットワーク経由で**機器の監視や制御**をするための **L7** プロトコル
* 「SNMPマネージャからSNMPエージェントへの**ポーリング**による情報取得」と「SNMPエージェントからSNMPマネージャへの**トラップ/インフォーム**通知」の2種類の仕組みにより実現

**MIB** (Management Information Base)
* SNMP Agent で**管理される情報の集合**（例: デバイス名, Interface速度 …）
* **標準MIB** で一般的な情報を定義し、**拡張MIB** でメーカー独自の情報等を定義
* デバイス名やInterface速度といった情報は **OID (Object ID) で識別**され、OIDを指定し情報をやり取り

| MIB | OID |
| --- | --- |
| ifSpeed (Interface速度) | 1.3.6.1.2.1.2.2.1.5 |
| hrProcessorLoad (CPU負荷) | 1.3.6.1.2.1.25.3.3.1.2 |

例）SNMP Manager「OID 1.3.6.1.2.1.2.2.1.5 をください」→ SNMP Agent は指定されたOIDに対応する値（Interfaceの速度）を応答。

## SNMP - メッセージ

| メッセージ | 送信者 | Version | 詳細 |
| --- | --- | --- | --- |
| **Get-Request** | Manager | v1〜 | **OIDを指定して情報を要求** |
| Get-Next-Request | Manager | v1〜 | 前回指定したOIDの次のOIDを要求 |
| Get-Bulk-Request | Manager | v2c〜 | Get-Next-Requestを改良し、複数のOIDの情報を一度に要求 |
| Set-Request | Manager | v1〜 | OIDを指定して設定変更を要求 |
| **Get-Response** | Agent | v1〜 | **要求されたOIDに対応する値や操作のステータス等を応答** |
| **Trap** | Agent | v1〜 | **特定のイベント検知時にAgentが自発的に情報を送信** |
| **Inform-Request** | Agent | v2c〜 | **Trapに確認応答の仕組みを設け、Managerから応答がない場合メッセージを再送する** |

| 仕組み | やり取り |
| --- | --- |
| **ポーリング** | Manager → Agent: Get-Request / Agent → Manager: Get-Response |
| **トラップ** | Agent → Manager: Trap（応答なし） |
| **インフォーム** | Agent → Manager: Inform-Request（応答がなければ再送）/ Manager → Agent: 確認応答 |

## SNMP - Version

| Version | サポートするメッセージ | 認証 |
| --- | --- | --- |
| **SNMP v1** | **Get-Request や Get-Response, Trap** など、基本的なSNMPメッセージ | **SNMPコミュニティによる平文認証** |
| **SNMP v2c** | **Inform-Request や Get-Bulk-Request** といった拡張されたSNMPメッセージ | SNMPコミュニティによる平文認証 |
| **SNMP v3** | Inform-Request や Get-Bulk-Request といった拡張されたSNMPメッセージ | コミュニティではなく**ユーザー単位の認証, 暗号化, ユーザー単位でアクセス可能なMIBも制限可能** |

関連: [../protocol/well-known-ports.md](../protocol/well-known-ports.md)（161 / 162 / 514）
