# Amazon Kinesis

**Category:** Analytics  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Kinesis collects and processes streams of data – like clicks, logs or sensor readings – in real time, as they happen.

## Real-life comparison

A normal database is like a letterbox you check once a day. Kinesis is like a conveyor belt of parcels that never stops – workers handle each one as it passes.

## What problem does it solve?

Some data is only useful if you act on it within seconds (fraud alerts, live dashboards). Kinesis handles huge flows of small records continuously.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Kinesis Data Streams** | Stores a stream for apps to read and replay. |
| **Amazon Data Firehose** | (formerly Kinesis Data Firehose) Delivers streams to S3, Redshift, OpenSearch with no code. |
| **Shard** | A unit of stream capacity (in provisioned mode). |
| **Producer / consumer** | Sends / reads records. |

## How it works (step by step)

1. Create a data stream (on-demand or provisioned).
2. Producers send records.
3. Consumers (e.g. Lambda) read and process them.
4. Or use Firehose to deliver straight into S3.

## When to use it

- Real-time analytics, clickstreams, log collection, IoT data.

## When NOT to use it (and what to use instead)

- **Simple work queues.** → [SQS](../application-integration/sqs.md).
- **Teams already using Kafka.** → [MSK](msk.md).

## Real-world example

**Scenario:** A games company wants live player activity.

**How it helps:** Game servers send events to a stream; Lambda updates a live leaderboard and Firehose saves everything to S3.

**What it looks like:**

```
 Game servers ──► Kinesis Data Stream ──► Lambda (live stats)
                                      └──► Firehose ──► S3
```

## Try it yourself

> ⚠️ **Cost warning:** Streams are charged per hour (per shard or on-demand stream) plus data. Delete the stream soon after testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Kinesis** → **Create data stream** → name `demo-stream`, **On-demand**.
2. Delete it after looking around.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create a small provisioned stream with one shard
aws kinesis create-stream --stream-name demo-stream --shard-count 1

# Send a record
aws kinesis put-record --stream-name demo-stream --partition-key p1 \
  --cli-binary-format raw-in-base64-out --data '{"event":"click"}'
```

### Option C – Using Terraform (infrastructure as code)

```hcl
resource "aws_kinesis_stream" "demo" {
  name        = "demo-stream"
  shard_count = 1
}
```

### Clean up (delete what you made)

```bash
aws kinesis delete-stream --stream-name demo-stream
```

## How much does it cost?

Data Streams: per shard-hour or per on-demand stream-hour plus data. Firehose: per GB ingested.

Official pricing: <https://aws.amazon.com/kinesis/data-streams/pricing/>

## Security tips

- Turn on server-side encryption with KMS.

## Common mistakes

- Forgetting a stream costs money every hour, even with no data.

## Works well with

- [Lambda](../compute/lambda.md), [S3](../storage/s3.md), [OpenSearch](opensearch.md).

## Quick check (test yourself)

1. What is Firehose for?
   <details><summary>Answer</summary>Delivering streaming data to stores like S3 with no code.</details>
2. What is a shard?
   <details><summary>Answer</summary>A unit of stream capacity.</details>
3. For a simple work queue, what's better?
   <details><summary>Answer</summary>SQS.</details>

## Learn more

- [Amazon Kinesis Data Streams Developer Guide](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)
