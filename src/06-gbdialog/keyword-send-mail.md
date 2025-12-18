# SEND MAIL

Send email messages.

## Syntax

```basic
SEND MAIL to, subject, body
SEND MAIL to, subject, body USING "account@example.com"
```

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `to` | String | Recipient email address(es), comma-separated for multiple |
| `subject` | String | Email subject line |
| `body` | String | Email body (plain text or HTML) |
| `account` | String | (Optional) Connected account to send through |

## Description

The `SEND MAIL` keyword sends emails using either:

1. **Default SMTP** - Configuration from `config.csv`
2. **Connected Account** - Send through Gmail, Outlook, etc. configured in Sources app

## Configuration

Default SMTP in `config.csv`:

```csv
name,value
email-from,noreply@example.com
email-server,smtp.example.com
email-port,587
email-user,smtp-user@example.com
email-pass,smtp-password
```

## Examples

```basic
SEND MAIL "user@example.com", "Welcome!", "Thank you for signing up."
```

```basic
recipients = "john@example.com, jane@example.com"
SEND MAIL recipients, "Team Update", "Meeting tomorrow at 3 PM"
```

```basic
body = "<h1>Welcome!</h1><p>Thank you for joining us.</p>"
SEND MAIL "user@example.com", "Getting Started", body
```

## USING Clause

Send through a connected account configured in Suite → Sources → Accounts:

```basic
SEND MAIL "customer@example.com", "Subject", body USING "support@company.com"
```

The email appears from that account's address with proper authentication.

```basic
SEND MAIL "customer@example.com", "Ticket Update", "Your ticket has been resolved." USING "support@company.com"
```

## Delivery Status

```basic
status = SEND MAIL "user@example.com", "Test", "Message"
IF status = "sent" THEN
    TALK "Email delivered successfully"
END IF
```

## Best Practices

1. Use connected accounts for better deliverability
2. Validate email addresses before sending
3. Implement delays for bulk emails
4. Handle failures gracefully

## Troubleshooting

| Issue | Cause | Solution |
|-------|-------|----------|
| Auth failed | Invalid credentials | Check config.csv or re-authenticate account |
| Not sending | Firewall blocking | Verify port 587/465 is open |
| Going to spam | No domain auth | Configure SPF/DKIM |
| Account not found | Not configured | Add account in Suite → Sources |

## See Also

- [USE ACCOUNT](./keyword-use-account.md)
- [WAIT](./keyword-wait.md)

## Implementation

Located in `src/basic/keywords/send_mail.rs`
