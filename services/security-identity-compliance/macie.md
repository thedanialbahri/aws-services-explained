# Amazon Macie

**Category:** Security, identity & compliance  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Macie scans your S3 buckets to find sensitive data, like names, card numbers or passport numbers, and warns you about risky bucket settings.

## Real-life comparison

Macie is like a data protection officer who walks through every filing cabinet looking for documents with personal details that shouldn't be lying around.

## What problem does it solve?

Companies often don't know where personal data has ended up. Under laws like UK GDPR, that's a risk. Macie finds it automatically.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Sensitive data** | Personal or financial information (PII). |
| **Managed data identifiers** | Built-in patterns, e.g. credit card numbers. |
| **Discovery job** | A scan of chosen buckets. |

## How it works (step by step)

1. Turn on Macie.
2. It lists your buckets and flags public or unencrypted ones.
3. Automated discovery samples objects, or you run a **discovery job**.
4. Findings show which files contain what types of sensitive data.

## When to use it

- Any account storing customer or staff data in S3.

## When NOT to use it (and what to use instead)

- **Data outside S3.** Macie only scans S3.

## Real-world example

**Scenario:** A marketing agency finds an old export of customer emails in a shared bucket.

**How it helps:** Macie reveals three more buckets with personal data, one of them public. The team locks them down and deletes what isn't needed.

**What it looks like:**

```
 S3 buckets ──scan──► Macie ──findings──► Security Hub / EventBridge
```

## Try it yourself

> ⚠️ **Cost warning:** Free trial, then charged per bucket monitored and per GB scanned. Disable after testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Macie** → **Get started** → **Enable Macie**.
2. View the **S3 buckets** summary for public or unencrypted buckets.

### Option B – Using the AWS CLI (typing commands)

```bash
aws macie2 enable-macie
```

### Option C – Using Terraform (infrastructure as code)

```hcl
resource "aws_macie2_account" "main" {}
```

### Clean up (delete what you made)

1. **Settings** → **Disable Macie**.

## How much does it cost?

Per bucket evaluated per month and per GB of data inspected.

Official pricing: <https://aws.amazon.com/macie/pricing/>

## Security tips

- Act on findings quickly; delete data you don't need.

## Common mistakes

- Scanning huge buckets without sampling – costly.

## Works well with

- [S3](../storage/s3.md), [Security Hub](security-hub.md).

## Quick check (test yourself)

1. What does Macie scan?
   <details><summary>Answer</summary>S3 buckets.</details>
2. What is it looking for?
   <details><summary>Answer</summary>Sensitive data like personal and financial details.</details>
3. Why does this matter in the UK?
   <details><summary>Answer</summary>UK GDPR requires you to protect and know about personal data you hold.</details>

## Learn more

- [Amazon Macie User Guide](https://docs.aws.amazon.com/macie/latest/user/what-is-macie.html)
- [Macie pricing](https://aws.amazon.com/macie/pricing/)
