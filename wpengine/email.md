---
nav_order: 4
title: Email
has_toc: false
parent: WPEngine
---

# Email Troubleshooting
WPEngine installs can send emails by default, and this usually just works.
However, some configurations may have issues.

## Microsoft Outlook/Exchange
Microsoft Exchange servers[^exchange] commonly block emails sent by WPEngine,
often without any trace of those emails for debugging.

1. Make sure [SPF Records](#spf-record) are set correctly.
1. Set [Exchange spam rules](#exchange-spam-rules).

[^exchange]: Outlook is the end-user email client. Exchange is the email server.
### Exchange Spam Rules
Exchange Admin Center -> Mail Flow -> Rules
- Add rule: From email address in question, set spam confidence to "Bypass Spam Filtering"

Alternatively, it may work to add the address to the company-wide allow list.


## Server Sends To Itself
When a server attempts to send an email to the domain it is serving,
e.g. `mangrove-web.com` sends to an `@mangrove-web.com` address,
it might not check the DNS records at all, and just send the email to itself.
WPEngine is configured by default not to receive emails, so this is not a likely issue on WPE.

## MX Record
MX records must be set to identify the host(s) emails should be sent to.
Email services will provide the correct values for your MX records;
check that these are set properly.

## SPF Record
Technically, any email system can send an email "from" any address.
Using this to make an email appear to come from a source other than it's actual source
is called email spoofing.

One protection against email spoofing is the SPF DNS record.
The SPF record lists all servers that can legitimately send emails from that domain,
and specifies a recommended policy on how to handle emails that do not meet those specifications.
Note that it is up to the recipient email server to actually check and follow the policies
specified in the SPF record.
Most services will follow these policies,
but there may be differences in behavior between different email systems.

### SPF Configuration
SPF records are a TXT record at the relevant domain.
In most cases, this will be the root domain.
In most DNS interfaces, this is set with a blank or `@` name field.

The SPF value is a string with several sections[^3]:
- First is the SPF version; use `v=spf1`.
- Next are the `include` statements.  
    `include:validsender.com` all valid sender domains, separated by spaces.
- Finally, specify a policy for emails from other origins.
    - `-a` Fail emails from servers not authorized in the SPF record.  
        Emails from unlisted servers will likely be immediately deleted and not show under spam.
    - `~a` Softfail email from unlisted servers. 
        Emails will be accepted, but marked as suspicious or spam.
    - `+a` Pass all. Don't do this. This allows any server to present as a legitimate sender.

Microsoft (Outlook) [recommends](https://docs.microsoft.com/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider?view=o365-worldwide)
using the `-a` hard fail option.
This offers more more confidence in the legitimacy of emails, however,
the discarding of failed emails can make debugging configuration issues more difficult.
I recommend using the `~a` Softfail option, as recommended by other services,
to avoid these debugging issues.[^1]


### Example SPF Record
WPEngine uses MailChannels to send emails,
so, for WPE, `include ` MailChannels.[^2]

- Record Type: `TXT`
- Name: `@`
- Value: `v=spf1 include:relay.mailchannels.net ~all`

To include Outlook:
- Value: `v=spf1 include:spf.protection.outlook.com include:relay.mailchannels.net ~all`

### SPF Validator
Validate your SPF records with the [SPF Record Checker](https://www.dmarcanalyzer.com/spf/checker/).

### Other Resources:
- [SendGrid SPF Settings](https://sendgrid.com/docs/glossary/spf/)
- [Mailgun SPF Settings](https://documentation.mailgun.com/en/latest/quickstart-sending.html)
- [Microsoft Office SPF Settings](https://docs.microsoft.com/en-us/microsoft-365/security/office-365-security/set-up-spf-in-office-365-to-help-prevent-spoofing?view=o365-worldwide)
- [Microsoft Office SPF to Prevent Spoofing](https://docs.microsoft.com/en-us/microsoft-365/security/office-365-security/how-office-365-uses-spf-to-prevent-spoofing?view=o365-worldwide)

[^1]: [-all vs ~all](https://dmarcian.com/what-is-the-difference-between-spf-all-and-all/)
[^2]: [WPEngine DMARC Best Practices](https://wpengine.com/support/dmarc-best-practices-get-email-inbox/)
[^3]: [How to Create and SPF Record](https://www.dmarcanalyzer.com/spf/how-to-create-an-spf-txt-record/)
