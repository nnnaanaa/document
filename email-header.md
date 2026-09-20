# EMAIL-HEADER.md
## 電子メールのヘッダ

***

## ヘッダの例

```
Return-Path: <bounce@mailer.example.com>
Received: from mx1.example.net ([198.51.100.1]) by mx2.example.org with SMTP;
        Mon, 25 Sep 2023 16:20:00 +0000
Received: from mail.example.com (mail.example.com [192.0.2.1])
        by mx1.example.net (Postfix) with ESMTPS id 67890FGHIJ
        for <bob.johnson@example.org>; Mon, 25 Sep 2023 16:18:00 +0000
From: Alice Smith <alice.smith@example.com>
To: Bob Johnson <bob.johnson@example.org>
Subject: Meeting Confirmation
Date: Mon, 25 Sep 2023 16:18:00 +0000
MIME-Version: 1.0
Content-Type: text/plain; charset=UTF-8
Message-ID: <CAFe+Xx1234Xx56@mailer.example.com>
Reply-To: Alice Smith <alice.smith@example.com>
X-Mailer: ExampleMailer (Version 5.2)
```

## 各ヘッダの意味

| ヘッダ | 意味 |
| --- | --- |
| **Return-Path** | メール配送に失敗した場合の**エラーメールの送信先** |
| **Received** | **メールの転送経路**。下から上にたどる（**上から新しい順**） |
| From | メールの差出人 |
| To | メールの宛先 |
| Subject | メールの件名 |
| Date | メールの送信日時 |
| **MIME-Version** | MIMEのバージョン |
| Content-Type | メール本文の形式 |
| Message-ID | メールの一意な識別子 |
| Reply-To | 返信する場合の返信先アドレス |
| X-Mailer | メールを作成したメールクライアント |

## ポイント

* `Received` は経路上のサーバが**先頭に追加していく**ため、上が新しく、**下から上にたどる**と送信元から受信者までの経路になる
* **電子メールのヘッダは偽装することができる**

関連: [well-known-ports.md](well-known-ports.md)（SMTP 25 / 587、POP3 110、IMAP 143 など）
