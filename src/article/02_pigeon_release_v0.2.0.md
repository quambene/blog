# Pigeon Release v0.2.0: Send email to arbitrary SMTP endpoints

[Pigeon](https://github.com/quambene/pigeon-rs)  is a command line tool for cheap and efficient email automation written in Rust.

New features in release v0.2.0 \[1\] include support for MIME and SMTP. Both standards are implemented in Pigeon via library Lettre \[2\].

MIME (Multipurpose Internet Mail Extensions) is the standard for building or formatting emails: the subject, the plaintext version as well as the HTML version of your email, attachments, etc.

SMTP (Simple Mail Transfer Protocol) is the standard for email transmission from email client to email server. It also serves as email relay, i.e., transmission of email from server to server. (Whereas IMAP or POP are used to retrieve an email from the server.) The email client is also called Message User Agent (MUA) and the email server is called the Message Transfer Agent (MTA).

Sending an email via SMTP looks like this:

* The client connects to the SMTP endpoint via TLS on port 587
* the client authenticates with username and password (SMTP Authentication)
* the MIME formatted email is transferred
* the MTA checks if sender and receiver email address are from the same domain
  * if this is the case, the email is already at its destination
  * if not, the MTA identifies the receiver's domain using DNS, and transfers the email to the right MTA (mail relay)

Let's see how you can achieve sending emails via SMTP in Pigeon in three steps:

1.) Set the SMTP endpoint, username and password in your `.env`. For example, using AWS Simple Email Service (SES):

``` bash
SMTP_SERVER=email-smtp.eu-west-1.amazonaws.com
SMTP_USERNAME=...
SMTP_PASSWORD=...
```

2.) Source your environment:

``` bash
set -a && source .env && set +a
```

3.) Send the email:

``` bash
pigeon send \
    sender@your-domain.com \
    receiver@gmail.com \
    --subject "Your invoice" \
    --text-file "./message.txt" \
    --html-file "./message.html" \
    --attachment "./invoice.pdf" \
    --archive
```

where `--text-file` and `--html-file` define the plaintext and html version of your email; and `--archive` stores your email in `.eml` format.

That's it for today. Happy for your feedback. Especially, if you have pain points using current email automation software.

TODO: Support oauth2 authentication which is used by gmail for example. Compare with plain SMTP authentication above (username and password) which is used by aws and others.

\[1\] [https://github.com/quambene/pigeon-rs](https://github.com/quambene/pigeon-rs)

\[2\] [https://crates.io/crates/lettre](https://crates.io/crates/lettre)

_First published on [Reddit](https://www.reddit.com/r/rust/comments/rwtkvw/pigeonrs_v020_open_source_email_automation_send/) (2022-01-05)._
