# Amazon EventBridge

**Category:** Application integration  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

EventBridge receives events from AWS services, your apps and partner SaaS tools, and sends each one to the right targets based on rules – it also runs scheduled jobs.

## Real-life comparison

EventBridge is like a post-room sorting office. Letters (events) arrive from everywhere; sorting rules decide which department gets each one ("anything from the bank → finance").

## What problem does it solve?

Reacting to things that happen – "an EC2 instance stopped", "a new customer signed up" – without hard-wiring every service to every other one.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Event** | A JSON message describing something that happened. |
| **Event bus** | Where events arrive (the default bus gets AWS service events). |
| **Rule** | A pattern that matches events and sends them to targets. |
| **Target** | Where matched events go, e.g. Lambda, SNS, SQS, Step Functions. |
| **EventBridge Scheduler** | Runs tasks on a schedule (like cron). |

## How it works (step by step)

1. Events arrive on an **event bus**.
2. Each **rule** checks whether events match its pattern.
3. Matching events are sent to the rule's **targets**.
4. Separately, **Scheduler** triggers targets at set times.

## When to use it

- Reacting to AWS events (e.g. GuardDuty findings, EC2 state changes).
- Scheduled jobs ("every weekday at 7am").
- Event-driven apps.

## When NOT to use it (and what to use instead)

- **Work that must wait in a queue.** → [SQS](sqs.md).

## Real-world example

**Scenario:** A team wants a Slack message whenever an EC2 instance is stopped in production.

**How it helps:** A rule matches "EC2 instance state change → stopped" and sends it to SNS, which forwards to Slack via a chat integration.

**What it looks like:**

```
 EC2 state change ──► default event bus ──rule (state=stopped)──► SNS ──► Slack
```

## Try it yourself

> ⚠️ **Cost warning:** AWS service events on the default bus are free; custom events and Scheduler invocations are charged per million, with a free allowance.

### Option A – Using the AWS Console (clicking in the website)

1. Open **EventBridge** → **Rules** → **Create rule**.
2. Name `ec2-stopped`, default bus, **Rule with an event pattern**.
3. Event source **AWS services** → **EC2** → **EC2 Instance State-change Notification** → specific state **stopped**.
4. Target **SNS topic** → `alerts`. Create.
5. Stop a test instance and check your email.

### Option B – Using the AWS CLI (typing commands)

```bash
# Rule that matches EC2 instances changing to "stopped"
aws events put-rule --name ec2-stopped --event-pattern \
  '{"source":["aws.ec2"],"detail-type":["EC2 Instance State-change Notification"],"detail":{"state":["stopped"]}}'
```

### Option C – Using Terraform (infrastructure as code)

```hcl
resource "aws_cloudwatch_event_rule" "ec2_stopped" {
  name = "ec2-stopped"
  event_pattern = jsonencode({
    source        = ["aws.ec2"]
    "detail-type" = ["EC2 Instance State-change Notification"]
    detail        = { state = ["stopped"] }
  })
}
```

### Clean up (delete what you made)

1. Delete the rule (remove targets first if using the CLI).

## How much does it cost?

AWS service events: free. Custom/partner events: per million. Scheduler, Pipes and archive/replay are charged separately.

Official pricing: <https://aws.amazon.com/eventbridge/pricing/>

## Security tips

- Use resource policies on custom buses to control who can send events.

## Common mistakes

- Event pattern typos – test patterns in the Console's sandbox.

## Works well with

- [Lambda](../compute/lambda.md), [SNS](sns.md), [Step Functions](step-functions.md), [GuardDuty](../security-identity-compliance/guardduty.md).

## Quick check (test yourself)

1. What does a rule do?
   <details><summary>Answer</summary>Matches events and sends them to targets.</details>
2. How do you run a job every day at 7am?
   <details><summary>Answer</summary>EventBridge Scheduler.</details>
3. Are AWS service events on the default bus charged?
   <details><summary>Answer</summary>No.</details>

## Learn more

- [Amazon EventBridge User Guide](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
- [EventBridge pricing](https://aws.amazon.com/eventbridge/pricing/)
