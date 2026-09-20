# WELL-KNOWN-PORTS.md
## 代表的なウェルノウンポート一覧

**覚えてください！**（スライドで赤字だったポート番号を**太字**にしている）

***

## ポート番号順

| ポート番号 | プロトコル | 用途 |
| --- | --- | --- |
| **20** | TCP | FTP (データ転送) |
| **21** | TCP | FTP (コントロール) |
| **22** | TCP | SSH |
| **23** | TCP | Telnet |
| **25** | TCP | SMTP |
| **53** | TCP/UDP | DNS |
| 67 | UDP | DHCP (サーバ) |
| 68 | UDP | DHCP (クライアント) |
| **80** | TCP | HTTP |
| **110** | TCP | POP3 |
| **123** | UDP | NTP |
| **143** | TCP | IMAP |
| 161 | UDP | SNMP |
| 162 | UDP | SNMP Trap |
| 179 | TCP | BGP経路交換 |
| 220 | TCP | IMAP3 |
| **443** | TCP | HTTPS |
| **445** | TCP | SMB |
| 514 | UDP | Syslog |
| **587** | TCP | SMTPサブミッションポート (STARTTLS) |
| **993** | TCP | IMAPS |
| **995** | TCP | POP3S |

## 用途別

| 分類 | ポート |
| --- | --- |
| メール送信 | 25 (SMTP) / 587 (サブミッション・STARTTLS) |
| メール受信 | 110 (POP3) / 995 (POP3S) / 143 (IMAP) / 993 (IMAPS) / 220 (IMAP3) |
| Web | 80 (HTTP) / 443 (HTTPS) |
| ファイル転送・共有 | 20・21 (FTP) / 445 (SMB) |
| リモート操作 | 22 (SSH) / 23 (Telnet) |
| 運用管理 | 161・162 (SNMP) / 514 (Syslog) / 123 (NTP) |
| 名前解決・アドレス配布 | 53 (DNS) / 67・68 (DHCP) |
| 経路制御 | 179 (BGP) |

関連: [dhcp.md](dhcp.md) / [email-header.md](email-header.md)
