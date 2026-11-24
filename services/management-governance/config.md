# AWS Config

**Category:** Management & governance  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

AWS Config records how your resources are set up over time and checks them against rules you choose.

## Real-life comparison

Config is like a building inspector with a camera. It photographs every room each time something changes and ticks off a checklist: fire doors closed? Exits clear?

## What problem does it solve?

You need to know "what did this security group look like last Tuesday?" and "are all our disks encrypted?". Config answers both automatically.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Configuration item** | A snapshot of one resource's settings at a point in time. |
| **Configuration recorder** | The setting that turns recording on. |
| **Config rule** | A check, e.g. `s3-bucket-public-read-prohibited`. |
| **Conformance pack** | A bundle of rules for a standard. |
| **Remediation** | An automatic fix for a failed rule. |

## How it works (step by step)

1. Turn on the **recorder** and choose a bucket for history.
2. Config records every change to supported resources.
3. Add **rules**; each resource is marked compliant or non-compliant.
4. Optionally add **remediation** to fix problems automatically.

## When to use it

- Audits, compliance and change history.
- Needed by [Security Hub](../security-identity-compliance/security-hub.md).

## When NOT to use it (and what to use instead)

- **Who made a change.** → [CloudTrail](cloudtrail.md) (Config links to it).

## Real-world example

**Scenario:** An auditor asks for proof that every EBS volume is encrypted.

**How it helps:** The rule `encrypted-volumes` shows 2 non-compliant volumes; the team fixes them and exports the report.

**What it looks like:**

```
 Resources ──changes──► Config recorder ──► history (S3)
                                   └──► rules ──► compliant ✓ / non-compliant ✗
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per configuration item recorded and per rule evaluation. Stop the recorder after testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **AWS Config** → **Get started** / **1-click setup**.
2. Go to **Rules** → **Add rule** → search `s3-bucket-public-read-prohibited` → add it.
3. After a few minutes, view compliance results.

### Option B – Using the AWS CLI (typing commands)

```bash
# See compliance for all rules
aws configservice describe-compliance-by-config-rule
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# Managed rule: S3 buckets must not allow public read (recorder must already be on)
resource "aws_config_config_rule" "no_public_read" {
  name = "s3-bucket-public-read-prohibited"
  source {
    owner             = "AWS"
    source_identifier = "S3_BUCKET_PUBLIC_READ_PROHIBITED"
  }
}
```

### Clean up (delete what you made)

1. Delete the rules you added.
2. **Settings** → stop the recorder (or delete it).

## How much does it cost?

Per configuration item recorded, per rule evaluation and per conformance pack evaluation.

Official pricing: <https://aws.amazon.com/config/pricing/>

## Security tips

- Record in every Region and keep history in a central account.

## Common mistakes

- Recording every resource type in a busy account and getting a large bill – choose what to record.

## Works well with

- [Security Hub](../security-identity-compliance/security-hub.md), [CloudTrail](cloudtrail.md), [Systems Manager](systems-manager.md) (for remediation).

## Quick check (test yourself)

1. What does Config record?
   <details><summary>Answer</summary>How resources are configured over time.</details>
2. What is a Config rule?
   <details><summary>Answer</summary>A check that marks resources compliant or non-compliant.</details>
3. Which service shows who made the change?
   <details><summary>Answer</summary>CloudTrail.</details>

## Learn more

- [AWS Config Developer Guide](https://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html)
- [AWS Config pricing](https://aws.amazon.com/config/pricing/)
