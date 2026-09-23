# VRRP.md
## VRRP (Virtual Router Redundancy Protocol)

***

## VRRPアドバタイズメント

Masterから Backup ルータに向けて定期的にやりとりされる管理用のパケット。**Masterの選出やダウン検知に使用**。**マルチキャストアドレス 224.0.0.18** が使用される。

| フィールド | 詳細 |
| --- | --- |
| Version | VRRPのバージョンを指定（基本は2が入る） |
| **VRID**（Virtual Router ID） | VRRPのグループを示すIDを指定（グループ内でMaster/Backupを選出） |
| **Priority** | Masterを選出する際に使用する優先度を指定（**大きいほど優先**） |
| Advertise Interval | アドバタイズメントの送信間隔 |

## Masterの選出とフェールオーバー

**Masterの選出:**
1. 各ルーターがアドバタイズメントの送信を開始
2. **Priorityが最も大きいルーター**をMasterに選出
3. Priorityが同じ場合、**実IPアドレスが最も大きいルーター**をMasterに選出

（Masterが仮想IPアドレス/仮想MACアドレスを保持）

**フェールオーバー:**
* Masterからのアドバタイズメントが届かない場合、残ったルーターで再度Masterの選出を行う
* 残ったBackupルーターの中からMasterルーターを選出する

**Preempt機能（プリエンプト機能）:**
* 一度Masterを選出すると、現在のMasterがダウンするまで通常はMasterの再選出は行われない
* Preempt機能が有効な場合、より Priorityの高いルーターが現れた場合そのルーターがMasterとなる
