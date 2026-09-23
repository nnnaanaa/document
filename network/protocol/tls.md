# TLS.md
## TLS 1.2 / 1.3 のネゴシエーション

***

## TLS 1.2 のネゴシエーション

| Client → Server | 説明 |
| --- | --- |
| TCP 3 way handshake ↔ TCP 3 way handshake | - |
| **Client Hello** → | サポートプロトコル, 暗号/圧縮スイート, Session ID …を交換 |
| ← **Server Hello** | サポートプロトコル, 暗号/圧縮スイート, Session ID …を交換 |
| ← Server Certificate (任意) | サーバー証明書を送付。Client側でルート証明書による検証 |
| ← Server Key Exchange (任意) | サーバ証明書に公開鍵を含まない場合（DHEやECDHEを用いる場合）等に公開鍵を送付 |
| ← Certificate Request (任意) | Clientにクライアント証明書を要求 |
| ← Server Hello Done | Server Helloの完了を通知 |
| Client Certificate (任意) → | クライアント証明書を送付 |
| **Client Key Exchange** → | 共通鍵のもとになる情報（プリマスターシークレット）を送付 |
| Client Verify (任意) → | 送付したクライアント証明書に対する電子署名を送付 |
| Change Cipher Spec → | これ以降、共通鍵による暗号化通信を開始することを通知 |
| Finished → | ネゴシエーションの終了を通知 |
| ← Change Cipher Spec | これ以降、共通鍵による暗号化通信を開始することを通知 |
| ← Finished | ネゴシエーションの終了を通知 |
| HTTPS通信 ↔ HTTPS通信 | **3往復目**から共通鍵による暗号化通信を開始 |

## TLS 1.2 から TLS 1.3 への変更点

### TLS 1.2
* 最初の1往復でサーバー/クライアント間の認証を行う（**RSA鍵交換**が使われる）
* 次の1往復で暗号化に必要な情報を交換する
* 最後に暗号化通信を開始する

### TLS 1.3
* 最初の1往復で暗号化に必要な情報を交換する
* 共通鍵の生成には（楕円曲線）ディフィー・ヘルマン鍵交換 **(EC)DHE** と呼ばれる方式が利用される
  * TLS 1.2ではRSA鍵交換が広く使われていたが、**TLS 1.3ではRSA鍵交換が廃止**
* これにより**公開鍵による暗号化が不要**で、安全に共通鍵を両端で生成できるようになった
  * **前方秘匿性**（通信セッションが終了した後に、過去の通信内容を復号することが困難）
* **2往復目**の途中から暗号化通信を開始し、その中で認証も行う
  * これは**認証付き暗号 / AEAD**（Authenticated Encryption with Associated Data）と呼ばれる

→ TLS1.2に比べ往復数が少なくなり、高速にネゴシエーションが完了する

## TLS 1.3 のネゴシエーション

| Client → Server | 説明 |
| --- | --- |
| TCP 3 way handshake ↔ TCP 3 way handshake | - |
| **Client Hello** → | TLS version, 暗号スイート, Session ID, **共通鍵のもとになる情報(key_share)**, …を交換 |
| ← **Server Hello** | TLS version, 暗号スイート, Session ID, **共通鍵のもとになる情報(key_share)** …を交換 |
| 暗号化通信を開始 ↔ 暗号化通信を開始 | key_shareで生成した共有鍵でネゴシエーション中から暗号化、**2往復目からHTTPのやり取りがされる(AEAD)** |
| ← Encrypted Extensions | 拡張機能のネゴシエーションに使用 |
| ← Certificate Request (任意) | クライアント証明書を要求 |
| ← Server Certificate (任意) | サーバー証明書を送付 |
| ← Server Certificate Verify (任意) | 送付したサーバー証明書に対する電子署名を送付 |
| ← Server Finished | ネゴシエーションの終了を通知 |
| Client Certificate (任意) → | クライアント証明書を送付 |
| Client Certificate Verify (任意) → | 送付したクライアント証明書に対する電子署名を送付 |
| Client Finished → | ネゴシエーションの終了を通知 |
| HTTPS通信 ↔ HTTPS通信 | - |

関連: [http.md](http.md)（HTTP/3とQUICのネゴシエーション高速化）
