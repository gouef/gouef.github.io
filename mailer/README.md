<p align="center">
  <img width="168" src="docs/gouef_logo.png" alt="gouef mailer logo" />
</p>

# mailer

<p align="center">
  <strong>Composable mailer package for Go with MIME building, transports, failover, and DKIM support.</strong><br/>
  Build plain-text and HTML e-mails, attach files and inline assets, and send through SMTP, sendmail, or native transport wrappers.
</p>

<p align="center">
  <a href="#-features"><strong>Features</strong></a>
  ·
  <a href="#-usage"><strong>Usage</strong></a>
  ·
  <a href="#-security"><strong>Security</strong></a>
  ·
  <a href="#-compatibility-notes"><strong>Compatibility</strong></a>
  ·
  <a href="#contributors"><strong>Contributors</strong></a>
</p>

[![Static Badge](https://img.shields.io/badge/Github-gouef%2Fmailer-blue?style=for-the-badge&logo=github&link=github.com%2Fgouef%2Fmailer)](https://github.com/gouef/mailer)
![Stable Version](https://img.shields.io/github/v/release/gouef/mailer?label=Stable&labelColor=green)
![GitHub Release](https://img.shields.io/github/v/release/gouef/mailer?label=RC&include_prereleases&filter=*rc*&logoSize=diago)
![GitHub Release](https://img.shields.io/github/v/release/gouef/mailer?label=Beta&include_prereleases&filter=*beta*&logoSize=diago)
[![GoDoc](https://pkg.go.dev/badge/github.com/gouef/mailer.svg)](https://pkg.go.dev/github.com/gouef/mailer)
[![Go Report Card](https://goreportcard.com/badge/github.com/gouef/mailer)](https://goreportcard.com/report/github.com/gouef/mailer)
[![codecov](https://codecov.io/github/gouef/mailer/branch/main/graph/badge.svg?token=YUG8EMH6Q8)](https://codecov.io/github/gouef/mailer)

Go package for composing e-mails.

> [!TIP]
>
> Quick start:
>
> ```go
> message := mailer.New().
>   SetFrom("noreply@example.com").
>   AddTo("john@example.com").
>   SetSubject("Welcome").
>   SetTextBody("Hello from Gouef Mailer")
>
> smtpMailer := mailer.NewSMTPMailer("smtp.example.com", 587).
>   SetAuth("smtp-user", "smtp-password").
>   SetSecurity(mailer.SecurityStartTLS)
>
> if err := smtpMailer.Send(message); err != nil {
>   log.Fatal(err)
> }
> ```

## ✨ Features

- Fluent message builder
- To, Cc, Bcc and Reply-To recipients
- Plain text and HTML bodies
- Multipart/alternative output
- File and in-memory attachments
- Inline attachments with Content-ID
- Custom e-mail headers
- Auto-generated Message-ID
- List-Unsubscribe helpers (including One-Click)
- SMTP failover (multiple servers)
- Fallback mailer chaining
- Message interceptors
- DKIM signing (RSA-SHA256)
- Sendmail transport
- Native transport wrapper
- Priority, Return-Path, Read-Receipt, Organization helpers
- First-class Address type

## 🚀 Usage

### 📨 Build a Message

```go
package main

import (
  "fmt"
  "log"

  "github.com/gouef/mailer"
)

func main() {
  message := mailer.New().
    SetFrom("noreply@example.com").
    AddTo("john@example.com").
    AddCc("team@example.com").
    SetReplyTo([]string{"support@example.com"}).
    SetSubject("Welcome").
    SetTextBody("Hello from text version").
    SetHtmlBody("<h1>Hello from HTML version</h1>")

  if _, err := message.AddAttachmentFromPath("./invoice.pdf"); err != nil {
    log.Fatal(err)
  }

  mimeMessage, err := message.ToMIME()
  if err != nil {
    log.Fatal(err)
  }

  fmt.Println(string(mimeMessage))
}
```

### 👤 Addresses with Display Names

```go
message := mailer.New()

if _, err := message.SetFromAddress("noreply@example.com", "Billing Bot"); err != nil {
  log.Fatal(err)
}
if _, err := message.AddToAddress("john@example.com", "John Doe"); err != nil {
  log.Fatal(err)
}

from, err := mailer.NewAddress("billing@example.com", "Billing Team")
if err != nil {
  log.Fatal(err)
}
if _, err := message.SetFromMailbox(from); err != nil {
  log.Fatal(err)
}

to := []mailer.Address{}
toJohn, _ := mailer.NewAddress("john@example.com", "John Doe")
toJane, _ := mailer.NewAddress("jane@example.com", "Jane Doe")
to = append(to, toJohn, toJane)

if _, err := message.SetToMailboxes(to); err != nil {
  log.Fatal(err)
}
```

### 🖼️ Add Inline Image

```go
if _, err := message.AddEmbeddedFile("./logo.png", "logo-cid"); err != nil {
  log.Fatal(err)
}

message.SetHtmlBody(`<p><img src="cid:logo-cid" alt="Logo" /></p>`)
```

### 📤 Send via SMTP

```go
smtpMailer := mailer.NewSMTPMailer("smtp.example.com", 587).
  SetAuth("smtp-user", "smtp-password").
  SetSecurity(mailer.SecurityStartTLS)

if err := smtpMailer.Send(message); err != nil {
  log.Fatal(err)
}
```

If you use SMTP authentication, prefer `SecurityStartTLS` on port `587` or `SecurityTLS` on port `465`.
`SecurityAuto` will not send credentials over an unencrypted connection.

### 📮 Send via Sendmail

```go
sendmail := mailer.NewSendmailMailer("/usr/sbin/sendmail")
if err := sendmail.Send(message); err != nil {
  log.Fatal(err)
}
```

### 🧰 Send via Native Transport

```go
nativeMailer, err := mailer.NewNativeMailer()
if err != nil {
  log.Fatal(err)
}

if err := nativeMailer.Send(message); err != nil {
  log.Fatal(err)
}
```

### 🔁 SMTP Failover

```go
smtpMailer := mailer.NewSMTPMailer("smtp-primary.example.com", 587).
  AddServer("smtp-backup.example.com", 587).
  SetAuth("smtp-user", "smtp-password").
  SetSecurity(mailer.SecurityStartTLS)
```

The mailer tries servers in order until sending succeeds.

### 🛟 Fallback Mailer

```go
primary := mailer.NewSMTPMailer("smtp-primary.example.com", 587)
backup := mailer.NewSMTPMailer("smtp-backup.example.com", 587)

sender := mailer.NewFallbackMailer(primary, backup)
if err := sender.Send(message); err != nil {
  log.Fatal(err)
}
```

### 🪝 Interceptor

```go
smtpMailer := mailer.NewSMTPMailer("smtp.example.com", 587).
  Use(func(m *mailer.Message) error {
    m.SetHeader("X-App", "billing")
    return nil
  })
```

Interceptors run before MIME generation and sending.

### ✍️ DKIM

```go
pemKey := []byte(`-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----`)

signer, err := mailer.NewDKIMSigner("example.com", "mail", pemKey)
if err != nil {
  log.Fatal(err)
}

smtpMailer := mailer.NewSMTPMailer("smtp.example.com", 587).
  SetDKIMSigner(signer)

sendmail := mailer.NewSendmailMailer("/usr/sbin/sendmail").
  SetDKIMSigner(signer)
```

### 🏷️ Additional Message Metadata

```go
message.
  SetPriority(1).
  SetReturnPath("bounce@example.com").
  SetReadReceiptTo("receipt@example.com").
  SetOrganization("Gouef").
  SetMessageID("custom-id@example.com")
```

For SMTPS on port 465:

```go
smtpMailer := mailer.NewSMTPMailer("smtp.example.com", 465).
  SetAuth("smtp-user", "smtp-password").
  SetSecurity(mailer.SecurityTLS)
```

If you explicitly need plaintext SMTP AUTH for a trusted local relay, use `SecurityNone`.

## 🔐 Security

- SMTP authentication is blocked on unencrypted connections unless you explicitly use `SecurityNone`.
- `SecurityAuto` will not send credentials over plaintext SMTP.
- Custom header names are validated before serialization.
- Invalid header names containing `:`, CR, or LF are ignored.
- Header values are normalized to a single line during MIME serialization.
- Invalid raw address strings are not emitted into address headers.

Notes:

- `SecurityNone` is an explicit opt-in for plaintext SMTP and should only be used with trusted local relays or controlled networks.
- Attachments loaded from disk are read fully into memory.
- The sendmail and native transports trust the selected local `sendmail` binary and host environment.

## 🧩 Compatibility Notes

The API shape follows Mail concepts where practical in Go:

- `SetFrom`, `AddTo`, `AddCc`, `AddBcc`, `SetSubject`
- `SetFromAddress`, `AddToAddress`, `AddCcAddress`, `AddBccAddress`, `AddReplyToAddress`
- `SetFromMailbox`, `AddToMailbox`, `AddCcMailbox`, `AddBccMailbox`, `AddReplyToMailbox`
- `SetFromMailboxes` (exactly one sender)
- `SetToMailboxes`, `SetCcMailboxes`, `SetBccMailboxes`, `SetReplyToMailboxes`
- `AddToMailboxes`, `AddCcMailboxes`, `AddBccMailboxes`, `AddReplyToMailboxes`
- `SetTextBody`, `SetHtmlBody`
- `AddAttachmentFromPath`, `AddEmbeddedFile`
- `AddHeader` / `SetHeader`
- `SetListUnsubscribe`, `SetListUnsubscribePostOneClick`
- `Use` interceptor hooks
- `SetDKIMSigner`

Custom headers added with `AddHeader` and `SetHeader` are validated before serialization.
Invalid header names such as names containing `:`, CR, or LF are ignored.

SMTP transport is available through `NewSMTPMailer(...).Send(message)`.

The package now includes both message composition and SMTP transport.

## 🛠️ Development

- Edit go.mod and rename to your package module
- Uncomment .github/workflows/tests.yml

## 🤝 Contributing

Read [Contributing](CONTRIBUTING.md)

## Contributors

<div>
  <a href="https://github.com/gouef/mailer/graphs/contributors">
    <img src="https://contrib.rocks/image?repo=gouef/mailer" />
  </a>
</div>

## 💬 Community

[![Discord](https://img.shields.io/discord/1334331501462163509?style=for-the-badge&logo=discord&logoColor=white&logoSize=auto&label=Community%20discord&labelColor=blue&link=https%3A%2F%2Fdiscord.gg%2FwjGqeWFnqK
)](https://discord.gg/wjGqeWFnqK)

Click above to join our community on Discord!
