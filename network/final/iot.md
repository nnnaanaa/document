# IOT.md
## IoT 直前シート

元のシート: [IoT 暗記シート](../protocol/iot.md)

### 要点

| 論点 | 覚えること |
| --- | --- |
| LPWA の分類 | **セルラー系 ＝ LTE-M・NB-IoT**（**3GPP**、免許帯域、SIM）、**非セルラー系 ＝ LoRaWAN・Sigfox**（920MHz） |
| 920MHz 帯 | **ISM バンド**。2.4GHz より**干渉が少なく遠くまで**届く |
| LTE-M / NB-IoT | LTE-M は**移動できて速め**、NB-IoT は**固定の機器向け** |
| MQTT | **TCP 1883**、**Publish/Subscribe**、ブローカ、トピック。機器から**外向きに接続** |
| MQTT の QoS | 0 最大1回、1 最低1回（**PUBACK**）、2 ちょうど1回（**PUBREC → PUBREL → PUBCOMP**） |
| MQTT のパケット | 接続 **CONNECT / CONNACK**、購読 **SUBSCRIBE / SUBACK** |
| CoAP | **UDP 5683**、**RESTful**、CON・NON・ACK、**メッセージ ID** で重複検出、**指数バックオフ** |
| CoAP のコード | **0.01 GET、0.02 POST、0.03 PUT、0.04 DELETE** ／ **2.01 Created、2.02 Deleted、2.04 Changed、2.05 Content** |

### 答えの型

| 問われ方 | 答えの型 |
| --- | --- |
| LPWA を使う理由 | 「**消費電力が小さく**電池で長く動き、**広い範囲**をカバーできる」 |
| 920MHz 帯の利点 | 「2.4GHz 帯より**電波干渉が少なく**、遠くまで届く」 |
| 機器からブローカへ接続する利点 | 「**NAPT や FW の内側**でも、外部から接続を受けずに通信できる」 |
| Publish/Subscribe の利点 | 「送り手と受け手が**互いを知らなくてよい**」 |
| CoAP のメッセージ ID の理由 | 「UDP では**重複**が起きるので、**重複を検出**し ACK と対応付ける」 |
| QoS 2 の利点と欠点 | 「**ちょうど1回**届く」が「**やり取りが4回**で通信量と電力を使う」 |
