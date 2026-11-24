# AWS Security Hub

**Category:** Security, identity & compliance  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Security Hub collects security findings from many AWS services into one dashboard and checks your setup against best-practice standards.

## Real-life comparison

It's like the main control panel in a building's security office. Instead of checking the CCTV, door logs and fire alarms separately, every alert appears on one screen, with a score showing how safe the building is.

## What problem does it solve?

Alerts come from GuardDuty, Inspector, Macie, Config and more. Checking each separately is slow. Security Hub puts them together, ranks them and runs checks like "is MFA on for root?".

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Security standard** | A checklist, e.g. AWS Foundational Security Best Practices or CIS. |
| **Control** | One check in a standard. |
| **Security score** | The percentage of controls you pass. |
| **Finding** | An alert from Security Hub or another service. |

## How it works (step by step)

1. You turn on Security Hub (it needs [AWS Config](../management-governance/config.md) recording).
2. You enable standards.
3. It runs checks and pulls in findings from other services.
4. You fix problems, and your score rises.

## When to use it

- Any account you want to keep secure – especially many accounts.

## When NOT to use it (and what to use instead)

- **You only want threat detection.** → [GuardDuty](guardduty.md) alone.

## Real-world example

**Scenario:** A start-up wants to pass a customer's security review.

**How it helps:** Security Hub shows a score and a list of failed checks (e.g. public S3 bucket, no MFA). The team fixes them and exports the results.

**What it looks like:**

```
 GuardDuty ─┐
 Inspector ─┼─► Security Hub (dashboard + score) ──► EventBridge alerts
 Macie     ─┤
 Config    ─┘
```

## Try it yourself

> ⚠️ **Cost warning:** Free trial for new users, then charged per check and per finding ingested. It also uses AWS Config, which has its own charges. Disable both after testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Security Hub** → **Go to Security Hub** → enable with default standards.
2. After a while, open **Security standards** and look at failed controls.

### Option B – Using the AWS CLI (typing commands)

```bash
# Turn on Security Hub with default standards
aws securityhub enable-security-hub --enable-default-standards
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# Turn on Security Hub in this account and Region
resource "aws_securityhub_account" "main" {}
```

### Clean up (delete what you made)

1. **Settings** → **General** → **Disable AWS Security Hub**.
2. Stop the AWS Config recorder if you started it only for this.

## How much does it cost?

Per security check per month and per finding ingested, above free amounts.

Official pricing: <https://aws.amazon.com/security-hub/pricing/>

## Security tips

- Use a central admin account to see findings for all accounts.

## Common mistakes

- Forgetting AWS Config must be recording for checks to work.

## Works well with

- [GuardDuty](guardduty.md), [Inspector](inspector.md), [Macie](macie.md), [AWS Config](../management-governance/config.md).

## Quick check (test yourself)

1. What does Security Hub need running to do its checks?
   <details><summary>Answer</summary>AWS Config.</details>
2. What is a security standard?
   <details><summary>Answer</summary>A checklist of best-practice controls.</details>
3. Does Security Hub replace GuardDuty?
   <details><summary>Answer</summary>No, it collects GuardDuty's findings alongside others.</details>

## Learn more

- [AWS Security Hub User Guide](https://docs.aws.amazon.com/securityhub/latest/userguide/what-is-securityhub.html)
- [Security Hub pricing](https://aws.amazon.com/security-hub/pricing/)
