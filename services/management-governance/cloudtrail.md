# AWS CloudTrail

**Category:** Management & governance  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

CloudTrail records every action taken in your AWS account – who did it, what they did, when, and from where.

## Real-life comparison

CloudTrail is like the visitor book and CCTV log at a building's reception. Every time someone enters, opens a door or moves something, it's written down with their name and the time.

## What problem does it solve?

When something changes or breaks ("who deleted the database?"), you need evidence. CloudTrail gives you a record of API calls and Console actions for security investigations, audits and troubleshooting.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Event** | One recorded action, e.g. `TerminateInstances`. |
| **Event history** | The last 90 days of management events, free and on by default. |
| **Trail** | A setting that saves events to an S3 bucket for longer. |
| **Management events** | Actions that change your setup (create, delete, modify). |
| **Data events** | Actions on data, e.g. reading an S3 object (off by default, extra cost). |

## How it works (step by step)

1. Someone (or something) calls an AWS API – via the Console, CLI, SDK or another service.
2. CloudTrail records the **event**: identity, time, source IP, action and result.
3. You can view the last 90 days in **Event history**.
4. To keep events longer, create a **trail** that saves them to S3 (and optionally CloudWatch Logs).

## When to use it

- Always. Create at least one multi-Region trail in every account.
- Security investigations, audits, "who changed this?" questions.

## When NOT to use it (and what to use instead)

- **Performance monitoring.** → [CloudWatch](cloudwatch.md).
- **Seeing what a resource's settings looked like over time.** → [AWS Config](config.md).

## Real-world example

**Scenario:** A small agency's live website suddenly disappears on a Friday afternoon.

**The problem:** Nobody admits to touching anything.

**How CloudTrail helps:** Event history shows a `DeleteStack` call at 15:42 by a contractor's role. The team restores the stack and tightens the contractor's permissions.

**What it looks like:**

```
 User / role / service ──API call──► AWS ──► CloudTrail event
                                            ├─► Event history (90 days)
                                            └─► Trail ──► S3 bucket (long-term)
```

## Try it yourself

> ⚠️ **Cost warning:** Event history is free. One trail delivering management events to S3 is free (you pay for S3 storage). Extra trails and data events cost money.

### Option A – Using the AWS Console (clicking in the website)

1. Open **CloudTrail** → **Event history**.
2. Look for an action you did earlier (e.g. `RunInstances` or `CreateBucket`). Click it to see the details.
3. Click **Trails** → **Create trail**.
4. Name `account-trail`, create a new S3 bucket, keep **Log file SSE-KMS encryption** as suggested (or disable it for a simple test).
5. Click **Next**, keep **Management events** ticked, **Next**, **Create trail**.

### Option B – Using the AWS CLI (typing commands)

```bash
# Show the last 5 "TerminateInstances" events
aws cloudtrail lookup-events \
  --lookup-attributes AttributeKey=EventName,AttributeValue=TerminateInstances \
  --max-results 5
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# A multi-Region trail writing to an existing bucket
# (the bucket needs a policy allowing CloudTrail to write to it)
resource "aws_cloudtrail" "account" {
  name                          = "account-trail"
  s3_bucket_name                = "my-example-trail-bucket"
  is_multi_region_trail         = true
  include_global_service_events = true
  enable_log_file_validation    = true
}
```

### Clean up (delete what you made)

Keeping one trail is good practice. If you want to remove it:
1. **Trails** → tick the trail → **Delete**.
2. Empty and delete its S3 bucket.

## How much does it cost?

- Event history: free.
- First copy of management events to S3: free (S3 storage charged).
- Extra copies and data events: charged per event. (CloudTrail Lake closed to new customers on 31 May 2026.)

Official pricing: <https://aws.amazon.com/cloudtrail/pricing/>

## Security tips

- Turn on **log file validation** so tampering can be detected.
- Store logs in a separate, locked-down account if you can.
- Send events to CloudWatch Logs for alerting.

## Common mistakes

- Relying only on the 90-day history.
- Creating a single-Region trail and missing activity elsewhere.

## Works well with

- [S3](../storage/s3.md), [CloudWatch](cloudwatch.md), [GuardDuty](../security-identity-compliance/guardduty.md), [Athena](../analytics/athena.md) (to search logs).

## Quick check (test yourself)

1. How long does free event history keep events?
   <details><summary>Answer</summary>90 days.</details>
2. What do you create to keep events longer?
   <details><summary>Answer</summary>A trail that delivers to S3.</details>
3. Which service shows CPU usage – CloudTrail or CloudWatch?
   <details><summary>Answer</summary>CloudWatch.</details>

## Learn more

- [AWS CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)
- [AWS CloudTrail pricing](https://aws.amazon.com/cloudtrail/pricing/)
