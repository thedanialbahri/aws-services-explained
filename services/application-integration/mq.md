# Amazon MQ

**Category:** Application integration  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Amazon MQ runs the message brokers Apache ActiveMQ and RabbitMQ for you, so existing apps that use them can move to AWS without rewriting.

## Real-life comparison

If SQS is AWS's own postal service, Amazon MQ is AWS running a franchise of the courier firm your company already uses – same forms, same rules.

## What problem does it solve?

Older apps often use standard messaging protocols (JMS, AMQP, MQTT, STOMP). Rewriting them for SQS is costly. Amazon MQ supports those protocols directly.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Message broker** | Software that passes messages between apps. |
| **ActiveMQ / RabbitMQ** | Two popular open-source brokers. |
| **AMQP / JMS / MQTT** | Standard messaging protocols. |

## How it works (step by step)

1. Create a broker (choose engine, size and single or multi-AZ).
2. Point your existing apps at its endpoints.
3. AWS handles patching and failover.

## When to use it

- Moving existing apps that use ActiveMQ or RabbitMQ.

## When NOT to use it (and what to use instead)

- **New cloud apps.** → [SQS](sqs.md) and [SNS](sns.md) are simpler and scale better.

## Real-world example

**Scenario:** An insurance company's Java app uses ActiveMQ on old servers.

**How it helps:** They move to Amazon MQ without code changes.

**What it looks like:**

```
 Java apps ──JMS──► Amazon MQ (ActiveMQ, multi-AZ)
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per broker-hour and storage. A small broker may be in the Free Tier for new accounts – check. Delete it straight after.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon MQ** → **Create brokers** and review the options.

### Option B – Using the AWS CLI (typing commands)

```bash
aws mq list-brokers
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete any broker you created.

## How much does it cost?

Per broker instance-hour plus storage per GB-month.

Official pricing: <https://aws.amazon.com/amazon-mq/pricing/>

## Security tips

- Keep brokers private; use strong credentials.

## Common mistakes

- Choosing MQ for a brand-new app.

## Works well with

- [EC2](../compute/ec2.md), [ECS](../containers/ecs.md).

## Quick check (test yourself)

1. Which brokers does Amazon MQ run?
   <details><summary>Answer</summary>ActiveMQ and RabbitMQ.</details>
2. When should you choose SQS instead?
   <details><summary>Answer</summary>For new cloud-native apps.</details>
3. Why use MQ?
   <details><summary>Answer</summary>To move existing apps without rewriting their messaging.</details>

## Learn more

- [Amazon MQ Developer Guide](https://docs.aws.amazon.com/amazon-mq/latest/developer-guide/welcome.html)
