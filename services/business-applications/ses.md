# Amazon Simple Email Service (SES)

**Category:** Business applications  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

SES sends emails from your apps – like order confirmations, password resets and newsletters – reliably and cheaply.

## Real-life comparison

SES is like a professional post room for your business. You hand over letters (emails); it stamps them properly so they're trusted, sends them, and tells you which ones bounced.

## What problem does it solve?

Sending email from your own server often ends up in spam folders, and big volumes get blocked. SES handles delivery, reputation and authentication (SPF, DKIM, DMARC) for you.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Verified identity** | An email address or domain you've proved you own. |
| **Sandbox** | New accounts can only send to verified addresses until you request production access. |
| **Bounce** | An email that couldn't be delivered. |
| **Complaint** | Someone marked your email as spam. |
| **DKIM / SPF / DMARC** | DNS records that prove your emails are genuine. |

## How it works (step by step)

1. Verify your domain (add DNS records) or an email address.
2. While in the **sandbox**, send only to verified addresses.
3. Request **production access** to email anyone.
4. Your app sends email through the SES API or SMTP.
5. Track bounces and complaints.

## When to use it

- Transactional emails (receipts, password resets) and marketing emails.

## When NOT to use it (and what to use instead)

- **Staff mailboxes with inboxes and calendars.** → Microsoft 365 or Google Workspace.
- **SMS or push notifications.** → [SNS](../application-integration/sns.md) or AWS End User Messaging.

## Real-world example

**Scenario:** An online bakery's order confirmations land in spam.

**How it helps:** The bakery verifies its domain in SES with DKIM, sends through SES and confirmations reach inboxes.

**What it looks like:**

```
 Website ──► Lambda ──► SES (signed with DKIM) ──► customer's inbox
```

## Try it yourself

> ⚠️ **Cost warning:** SES charges per 1,000 emails, with a free allowance for new accounts. Sandbox testing costs almost nothing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon SES** → **Identities** → **Create identity** → **Email address** → your email.
2. Click the verification link sent to you.
3. Open the identity → **Send test email** → send to yourself.

### Option B – Using the AWS CLI (typing commands)

```bash
# Send a simple email (both addresses must be verified while in the sandbox)
aws sesv2 send-email --from-email-address you@example.com \
  --destination ToAddresses=you@example.com \
  --content 'Simple={Subject={Data="Hello"},Body={Text={Data="Sent with SES"}}}'
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# Verify an email address identity
resource "aws_sesv2_email_identity" "me" {
  email_identity = "you@example.com"
}
```

### Clean up (delete what you made)

1. **Identities** → tick your test identity → **Delete**.

## How much does it cost?

Per 1,000 emails sent, plus per GB of attachments; dedicated IPs and some features cost extra.

Official pricing: <https://aws.amazon.com/ses/pricing/>

## Security tips

- Set up SPF, DKIM and DMARC for your domain.
- Never let users send any email they like through your SES account (spam risk).

## Common mistakes

- Forgetting you're in the sandbox, so emails to customers fail.
- Ignoring bounces and complaints – your account can be paused.

## Works well with

- [Lambda](../compute/lambda.md), [SNS](../application-integration/sns.md), [Route 53](../networking/route-53.md).

## Quick check (test yourself)

1. What is the SES sandbox?
   <details><summary>Answer</summary>A starting mode where you can only send to verified addresses.</details>
2. What helps emails avoid spam folders?
   <details><summary>Answer</summary>SPF, DKIM and DMARC records.</details>
3. Is SES a mailbox service for staff?
   <details><summary>Answer</summary>No – it's for sending (and receiving) email from apps.</details>

## Learn more

- [Amazon SES Developer Guide](https://docs.aws.amazon.com/ses/latest/dg/Welcome.html)
- [Amazon SES pricing](https://aws.amazon.com/ses/pricing/)
