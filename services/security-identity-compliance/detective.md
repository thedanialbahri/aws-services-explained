# Amazon Detective

**Category:** Security, identity & compliance  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Detective helps you investigate security alerts by linking together activity from your logs, so you can see what happened, who did it and what was affected.

## Real-life comparison

If GuardDuty is the alarm going off, Detective is the investigator who pieces together the timeline: who came in, which rooms they entered and what they touched.

## What problem does it solve?

After an alert, working out the full story from raw logs takes hours. Detective builds a graph of related activity automatically.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Behaviour graph** | Detective's linked model of activity in your accounts. |
| **Investigation** | Looking into a finding, user or resource. |

## How it works (step by step)

1. Turn on Detective (GuardDuty should already be on).
2. It builds a behaviour graph from CloudTrail, VPC Flow Logs and GuardDuty findings.
3. From a GuardDuty finding, click **Investigate in Detective** to see timelines and related activity.

## When to use it

- Security teams investigating incidents.

## When NOT to use it (and what to use instead)

- **Detecting threats.** → [GuardDuty](guardduty.md) (Detective investigates, it doesn't detect).

## Real-world example

**Scenario:** GuardDuty flags an IAM user calling APIs from an unusual country.

**How it helps:** Detective shows when the activity started, which IPs were used and what else that user did, so the team can judge the damage.

**What it looks like:**

```
 GuardDuty finding ──► Detective (timeline, related IPs, resources) ──► response decision
```

## Try it yourself

> ⚠️ **Cost warning:** Free trial, then charged per GB of data ingested. Disable after testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Detective** → **Enable Amazon Detective**.
2. Generate GuardDuty sample findings and open one in Detective.

### Option B – Using the AWS CLI (typing commands)

```bash
aws detective create-graph
```

### Option C – Using Terraform (infrastructure as code)

```hcl
resource "aws_detective_graph" "main" {}
```

### Clean up (delete what you made)

1. **Settings** → **General** → **Disable Amazon Detective**.

## How much does it cost?

Per GB of data ingested into the behaviour graph.

Official pricing: <https://aws.amazon.com/detective/pricing/>

## Security tips

- Limit who can use Detective – it shows sensitive activity.

## Common mistakes

- Expecting Detective to raise alerts on its own.

## Works well with

- [GuardDuty](guardduty.md), [Security Hub](security-hub.md), [CloudTrail](../management-governance/cloudtrail.md).

## Quick check (test yourself)

1. Does Detective detect threats?
   <details><summary>Answer</summary>No, it helps investigate them.</details>
2. What should be turned on first?
   <details><summary>Answer</summary>GuardDuty.</details>
3. What is a behaviour graph?
   <details><summary>Answer</summary>A linked model of activity in your accounts.</details>

## Learn more

- [Amazon Detective User Guide](https://docs.aws.amazon.com/detective/latest/userguide/what-is-detective.html)
- [Detective pricing](https://aws.amazon.com/detective/pricing/)
