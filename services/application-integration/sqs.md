# Amazon Simple Queue Service (SQS)

**Category:** Application integration  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

SQS is a message queue: one part of your app puts messages in, another part takes them out and processes them when it's ready.

## Real-life comparison

SQS is like the order-ticket rail in a busy restaurant kitchen. Waiters clip orders on the rail as they come in. Chefs take the next ticket when they're free. If there's a rush, tickets wait on the rail instead of being lost, and more chefs can help.

## What problem does it solve?

If a website sends work directly to a back-end server and that server is busy or down, the request fails. With a queue in between, the website just drops a message in the queue and moves on. The back end processes messages at its own pace, and nothing is lost.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Queue** | The waiting line for messages. |
| **Message** | One piece of data (up to 256 KB), e.g. an order in JSON. |
| **Producer** | The part that sends messages. |
| **Consumer** | The part that receives and processes messages. |
| **Standard queue** | Very high throughput; messages may occasionally arrive twice or out of order. |
| **FIFO queue** | First-in, first-out: strict order and no duplicates, with lower throughput. |
| **Visibility timeout** | How long a message is hidden after a consumer picks it up, so others don't take it too. |
| **Dead-letter queue (DLQ)** | Where messages go if they keep failing, so you can inspect them. |

## How it works (step by step)

1. You create a **queue**.
2. A **producer** sends a message.
3. SQS stores it safely across several servers.
4. A **consumer** asks for messages (polls) and receives one.
5. The message is hidden for the **visibility timeout**.
6. If the consumer finishes, it **deletes** the message.
7. If it fails, the message becomes visible again for another try. After too many tries, it moves to the **dead-letter queue**.

## When to use it

- Smoothing out traffic spikes (e.g. order processing).
- Background jobs: sending emails, resizing images, generating reports.
- Decoupling microservices.

## When NOT to use it (and what to use instead)

- **Several systems all need a copy of the same message.** → [SNS](sns.md) (or SNS + SQS together).
- **Routing events based on their content, or reacting to AWS events.** → [EventBridge](eventbridge.md).
- **Real-time streams that many consumers replay.** → [Kinesis](../analytics/kinesis.md).

## Real-world example

**Scenario:** Ben runs an online gift shop. Each order triggers a confirmation email, a stock update and a label print.

**The problem:** On busy days the website freezes while all that work happens, and orders fail.

**How SQS helps:** The website puts each order in an SQS queue and immediately shows "Thanks for your order!". A Lambda function reads from the queue and does the slower work. On a busy day, messages wait a little longer – but no order is lost.

**What it looks like:**

```
 Website ──send──► [ SQS queue: orders ] ──poll──► Lambda (process order)
                         │ fails 3 times
                         ▼
                 [ Dead-letter queue ]
```

## Try it yourself

> ⚠️ **Cost warning:** SQS has an always-free allowance of requests each month. A test queue costs nothing. Delete it at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Open **SQS** → **Create queue**.
2. Type **Standard**, name `demo-orders`. Click **Create queue**.
3. Click **Send and receive messages**.
4. Type `{"orderId": 1, "item": "mug"}` in the message body → **Send message**.
5. Under **Receive messages**, click **Poll for messages**.
6. Click the message to read it, then tick it and click **Delete**.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create a queue and save its URL
QUEUE_URL=$(aws sqs create-queue --queue-name demo-orders --query QueueUrl --output text)

# Send a message
aws sqs send-message --queue-url $QUEUE_URL --message-body '{"orderId":1,"item":"mug"}'

# Receive it (shows the ReceiptHandle needed to delete it)
aws sqs receive-message --queue-url $QUEUE_URL

# Delete it after processing (paste the ReceiptHandle from above)
aws sqs delete-message --queue-url $QUEUE_URL --receipt-handle "PASTE-RECEIPT-HANDLE"
```

### Option C – Using Terraform (infrastructure as code)

Written for the AWS provider `~> 6.0`.

```hcl
# Queue for messages that keep failing
resource "aws_sqs_queue" "orders_dlq" {
  name = "demo-orders-dlq"
}

# Main queue: after 3 failed attempts, move the message to the DLQ
resource "aws_sqs_queue" "orders" {
  name                       = "demo-orders"
  visibility_timeout_seconds = 60
  sqs_managed_sse_enabled    = true
  redrive_policy = jsonencode({
    deadLetterTargetArn = aws_sqs_queue.orders_dlq.arn
    maxReceiveCount     = 3
  })
}
```

### Clean up (delete what you made)

1. **SQS** → tick `demo-orders` (and any DLQ) → **Delete** → type `confirm`.
2. CLI: `aws sqs delete-queue --queue-url $QUEUE_URL`

## How much does it cost?

Per million requests (FIFO costs a little more than standard), plus data transfer out. A large monthly free allowance covers most learning.

Official pricing: <https://aws.amazon.com/sqs/pricing/>

## Security tips

- Turn on server-side encryption (SSE-SQS or KMS).
- Use queue policies to allow only specific senders.

## Common mistakes

- **Visibility timeout shorter than the processing time**, so messages are processed twice.
- **No dead-letter queue**, so a bad message retries forever.
- **Not deleting messages** after processing.
- Forgetting standard queues can deliver a message more than once – make processing safe to repeat.

## Works well with

- [Lambda](../compute/lambda.md) – process messages automatically.
- [SNS](sns.md) – fan out one message to several queues.
- [Auto Scaling](../compute/auto-scaling.md) – scale workers by queue length.

## Quick check (test yourself)

1. Which queue type guarantees order?
   <details><summary>Answer</summary>FIFO.</details>
2. What happens if a consumer crashes before deleting a message?
   <details><summary>Answer</summary>After the visibility timeout, the message becomes visible again for another try.</details>
3. What is a dead-letter queue for?
   <details><summary>Answer</summary>Holding messages that failed too many times, so you can inspect them.</details>

## Learn more

- [Amazon SQS Developer Guide](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html)
- [Amazon SQS pricing](https://aws.amazon.com/sqs/pricing/)
