# Amazon GuardDuty

**Category:** Security, identity & compliance  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

GuardDuty constantly watches your AWS account's activity and network traffic for signs of hacking, and alerts you when it finds something.

## Real-life comparison

GuardDuty is like a CCTV control room for your building. Staff watch the cameras 24/7 and raise the alarm if someone tries doors at 3am or a stranger enters a restricted area.

## What problem does it solve?

Attackers who steal an access key might start crypto-mining servers or copy data. Spotting this by reading logs yourself is nearly impossible. GuardDuty analyses logs automatically using threat intelligence and machine learning.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Finding** | An alert about something suspicious, with a severity (low, medium, high, critical). |
| **Detector** | GuardDuty switched on in one Region of an account. |
| **Threat intelligence** | Lists of known bad IP addresses and domains. |
| **Protection plans** | Extra checks, e.g. for S3, EKS, malware, RDS logins, Lambda. |

## How it works (step by step)

1. You turn on GuardDuty in each Region (one click).
2. It reads CloudTrail events, VPC Flow Logs and DNS logs behind the scenes – you don't need to set these up.
3. It compares activity with normal behaviour and threat lists.
4. It creates **findings**, which you can send to email or Slack through [EventBridge](../application-integration/eventbridge.md) and [SNS](../application-integration/sns.md).

## When to use it

- In every account and every Region you use. It's one of the first things to turn on.

## When NOT to use it (and what to use instead)

- **Checking settings against best practices.** → [Security Hub](security-hub.md) / [AWS Config](../management-governance/config.md).
- **Finding software vulnerabilities.** → [Inspector](inspector.md).

## Real-world example

**Scenario:** A developer accidentally pushed an access key to a public GitHub repo.

**What happens:** Within minutes, someone uses it from an unusual country to launch large servers. GuardDuty raises a high-severity finding, EventBridge sends an alert, and the team disables the key.

**What it looks like:**

```
 CloudTrail + VPC Flow Logs + DNS ──► GuardDuty ──finding──► EventBridge ──► SNS ──► Email/Slack
```

## Try it yourself

> ⚠️ **Cost warning:** New accounts get a free trial period (check the console). After that, it's charged by the volume of logs and events analysed. Disable it after the trial if you don't want charges.

### Option A – Using the AWS Console (clicking in the website)

1. Open **GuardDuty** → **Get started** → **Enable GuardDuty**.
2. Go to **Settings** → **Generate sample findings**.
3. Open **Findings** and click one to read what it means and how to respond.

### Option B – Using the AWS CLI (typing commands)

```bash
# Turn on GuardDuty in this Region
aws guardduty create-detector --enable

# Create sample findings to practise with (replace the detector ID)
aws guardduty create-sample-findings --detector-id 12abc34d567e8fa901bc2d34e56789f0
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# Turn on GuardDuty in this Region
resource "aws_guardduty_detector" "main" {
  enable = true
}
```

### Clean up (delete what you made)

1. **Settings** → **Suspend GuardDuty** or **Disable GuardDuty** (disabling deletes findings).

## How much does it cost?

Charged by the amount of data analysed (CloudTrail events, VPC Flow Logs, DNS logs) plus each protection plan you turn on.

Official pricing: <https://aws.amazon.com/guardduty/pricing/>

## Security tips

- Enable it in **all Regions**, even ones you don't use – attackers love unused Regions.
- Use a delegated admin account with Organizations to see all accounts in one place.

## Common mistakes

- Turning it on but never looking at the findings – set up alerts.

## Works well with

- [Security Hub](security-hub.md), [Detective](detective.md), [EventBridge](../application-integration/eventbridge.md).

## Quick check (test yourself)

1. Do you need to turn on VPC Flow Logs for GuardDuty to use them?
   <details><summary>Answer</summary>No, it reads them independently.</details>
2. What is a finding?
   <details><summary>Answer</summary>An alert about suspicious activity.</details>
3. Why enable it in unused Regions?
   <details><summary>Answer</summary>Attackers often use Regions you don't watch.</details>

## Learn more

- [Amazon GuardDuty User Guide](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html)
- [GuardDuty pricing](https://aws.amazon.com/guardduty/pricing/)
