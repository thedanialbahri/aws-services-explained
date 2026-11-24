# AWS IoT Events

**Category:** Internet of Things (IoT)  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ⛔ **No longer available.** AWS IoT Events stopped accepting new customers on 20 May 2025 and reached end of support on 20 May 2026. Use [IoT Core](iot-core.md) rules with [Lambda](../compute/lambda.md), [Step Functions](../application-integration/step-functions.md) or CloudWatch alarms instead.

## In one sentence

IoT Events watched device data and triggered actions when certain patterns or states occurred.

## Real-life comparison

It was like a smoke alarm with rules: "if temperature rises fast and stays high for 2 minutes, raise an alarm".

## What problem does it solve?

It let you define device "states" and transitions without writing code.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Detector model** | A state machine for a device. |
| **Alarm** | An alert when a condition is met. |

## How it works (step by step)

1. Data came in from IoT Core or SiteWise.
2. Detector models tracked each device's state.
3. Actions ran when states changed.

## When to use it

- No longer possible – the service has shut down.

## When NOT to use it (and what to use instead)

- **All cases.** → IoT Core rules + Lambda/Step Functions, or CloudWatch alarms.

## Real-world example

**Scenario:** A freezer company alerted engineers if a freezer warmed up for too long.

**Today:** An IoT Core rule sends readings to a Lambda function, which tracks the state and alerts via SNS.

**What it looks like:**

```
 Freezer sensor ──► IoT Core rule ──► Lambda (state logic) ──► SNS alert
```

## Try it yourself

> ⚠️ **Cost warning:** Not applicable.

### Option A – Using the AWS Console (clicking in the website)

Not applicable – service shut down.

### Option B – Using the AWS CLI (typing commands)

Not applicable.

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Not applicable.

## How much does it cost?

Not applicable.

## Security tips

- Apply the same least-privilege rules to replacement Lambda functions.

## Common mistakes

- Following old tutorials that use IoT Events.

## Works well with

- [IoT Core](iot-core.md), [Lambda](../compute/lambda.md).

## Quick check (test yourself)

1. Is IoT Events available?
   <details><summary>Answer</summary>No, it reached end of support on 20 May 2026.</details>
2. What's a replacement approach?
   <details><summary>Answer</summary>IoT Core rules with Lambda or Step Functions.</details>
3. What was a detector model?
   <details><summary>Answer</summary>A state machine tracking a device's state.</details>

## Learn more

- [AWS IoT Events end of support](https://docs.aws.amazon.com/iotevents/latest/developerguide/iotevents-end-of-support.html)
