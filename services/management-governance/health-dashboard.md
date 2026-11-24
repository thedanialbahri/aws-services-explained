# AWS Health Dashboard

**Category:** Management & governance  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

The AWS Health Dashboard tells you when AWS has a problem or planned maintenance that affects your resources.

## Real-life comparison

It's like the travel updates board at a train station – but personalised. It shows not just "delays on the network" but "your 08:15 train is cancelled".

## What problem does it solve?

When something breaks, you need to know quickly if it's your fault or AWS's. Health shows service issues in your Regions and events affecting your specific resources (like scheduled server retirement).

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Service health** | The public status of all AWS services. |
| **Your account health** | Events affecting your own resources. |
| **Scheduled change** | Planned maintenance, e.g. an instance retirement. |

## How it works (step by step)

1. AWS posts events.
2. You view them in the dashboard.
3. You can send events to [EventBridge](../application-integration/eventbridge.md) to alert your team automatically.

## When to use it

- Whenever something seems wrong.
- Planning for scheduled maintenance.

## When NOT to use it (and what to use instead)

- **Monitoring your own app.** → [CloudWatch](cloudwatch.md).

## Real-world example

**Scenario:** An EC2 instance's underlying hardware is due to retire.

**How it helps:** Health shows the event two weeks ahead, so the team moves the server in a quiet period.

**What it looks like:**

```
 AWS ──event──► Health Dashboard ──► EventBridge ──► SNS ──► team email
```

## Try it yourself

> ⚠️ **Cost warning:** Free.

### Option A – Using the AWS Console (clicking in the website)

1. Click the bell icon in the Console header, or search for **Health**.
2. Look at **Your account health** and **Service health**.

### Option B – Using the AWS CLI (typing commands)

The Health API needs Business support or higher. Use the Console.

### Option C – Using Terraform (infrastructure as code)

An EventBridge rule for `aws.health` events can be built in Terraform – see [EventBridge](../application-integration/eventbridge.md).

### Clean up (delete what you made)

Nothing to clean up.

## How much does it cost?

Free.

## Security tips

- Security-related notifications (e.g. leaked access key reports) appear here – watch them.

## Common mistakes

- Not setting up alerts for Health events.

## Works well with

- [EventBridge](../application-integration/eventbridge.md), [SNS](../application-integration/sns.md).

## Quick check (test yourself)

1. What's the difference between service health and account health?
   <details><summary>Answer</summary>Service health is general status; account health is events affecting your resources.</details>
2. How can you get alerts for Health events?
   <details><summary>Answer</summary>With an EventBridge rule sending to SNS.</details>
3. Is it free?
   <details><summary>Answer</summary>Yes.</details>

## Learn more

- [AWS Health User Guide](https://docs.aws.amazon.com/health/latest/ug/what-is-aws-health.html)
