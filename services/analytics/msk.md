# Amazon Managed Streaming for Apache Kafka (MSK)

**Category:** Analytics  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

MSK runs Apache Kafka for you – the popular open-source platform for streaming data between systems.

## Real-life comparison

Kafka is like a giant, durable noticeboard where systems pin up events and many readers can read them in order, at their own pace.

## What problem does it solve?

Kafka is powerful but hard to run (brokers, storage, upgrades). MSK manages it, including a serverless option.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Topic** | A named stream of events. |
| **Broker** | A Kafka server. |
| **Partition** | A slice of a topic for parallel reading. |
| **MSK Serverless** | Kafka without sizing brokers. |

## How it works (step by step)

1. Create an MSK cluster or serverless cluster.
2. Create topics.
3. Producers write events; consumers read them.

## When to use it

- Teams already using Kafka; event streaming at scale.

## When NOT to use it (and what to use instead)

- **New, simpler streaming needs.** → [Kinesis](kinesis.md).

## Real-world example

**Scenario:** A bank moves its Kafka-based payment events platform to AWS.

**How it helps:** MSK runs the same Kafka APIs, so apps don't change.

**What it looks like:**

```
 Payment apps ──► MSK topic "payments" ──► fraud checks, ledger, notifications
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per broker-hour or serverless cluster-hour plus storage. Not cheap to leave running.

### Option A – Using the AWS Console (clicking in the website)

1. Open **MSK** → **Create cluster** → review **Quick create** settings.

### Option B – Using the AWS CLI (typing commands)

```bash
aws kafka list-clusters-v2
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete the cluster.

## How much does it cost?

Per broker instance-hour and storage, or per cluster-hour and partition for serverless.

Official pricing: <https://aws.amazon.com/msk/pricing/>

## Security tips

- Use IAM authentication and TLS; keep clusters private.

## Common mistakes

- Over-provisioning brokers.

## Works well with

- [Lambda](../compute/lambda.md), [Glue](glue.md).

## Quick check (test yourself)

1. What is Kafka?
   <details><summary>Answer</summary>An open-source event streaming platform.</details>
2. What is a topic?
   <details><summary>Answer</summary>A named stream of events.</details>
3. For simpler streaming, what could you use?
   <details><summary>Answer</summary>Amazon Kinesis.</details>

## Learn more

- [Amazon MSK Developer Guide](https://docs.aws.amazon.com/msk/latest/developerguide/what-is-msk.html)
