# Amazon Simple Notification Service (SNS)

**Category:** Application integration  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

SNS sends one message to many subscribers at once – email addresses, phone numbers, queues, Lambda functions or web addresses.

## Real-life comparison

SNS is like a school's text alert system. The office sends one message ("school closed due to snow") and every parent who signed up gets it at the same moment, whether by text or email.

## What problem does it solve?

When something happens, several people or systems often need to know. Sending to each one separately is messy. With SNS, you publish once to a **topic**, and SNS delivers to everyone subscribed.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Topic** | A named channel that messages are published to. |
| **Publisher** | Whatever sends the message, e.g. a CloudWatch alarm. |
| **Subscriber** | Whoever receives it: email, SMS, SQS, Lambda, HTTPS, mobile push. |
| **Fan-out** | One message going out to many places. |
| **Filter policy** | Lets a subscriber receive only messages it cares about. |
| **FIFO topic** | Keeps strict order (only to SQS FIFO subscribers). |

## How it works (step by step)

1. You create a **topic**.
2. You add **subscriptions** (e.g. an email address). Email subscribers must click a confirmation link.
3. A **publisher** sends a message to the topic.
4. SNS immediately pushes a copy to every confirmed subscriber.

## When to use it

- Alerts from CloudWatch alarms, Budgets and EventBridge rules.
- Fan-out: one order event sent to several SQS queues.
- Text or email notifications to users.

## When NOT to use it (and what to use instead)

- **Messages must wait until a worker is ready.** SNS doesn't store messages. → [SQS](sqs.md) (or SNS → SQS).
- **Complex routing based on event content from many sources.** → [EventBridge](eventbridge.md).
- **Marketing or bulk email.** → [SES](../business-applications/ses.md).

## Real-world example

**Scenario:** An online shop wants three things to happen when an order is placed: send a confirmation, update stock and alert the warehouse.

**The problem:** The website code calls all three directly; if one is slow, checkout is slow.

**How SNS helps:** The website publishes one "order placed" message to an SNS topic. Three SQS queues are subscribed, each feeding a separate worker.

**What it looks like:**

```
                        ┌──► SQS: emails    ──► Lambda (send confirmation)
 Website ──► SNS topic ─┼──► SQS: stock     ──► Lambda (update stock)
                        └──► SQS: warehouse ──► Lambda (print label)
```

## Try it yourself

> ⚠️ **Cost warning:** SNS has a monthly free allowance for publishes and email deliveries. SMS messages cost money and need extra setup – stick to email for testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **SNS** → **Topics** → **Create topic**.
2. Type **Standard**, name `alerts` → **Create topic**.
3. Click **Create subscription** → protocol **Email** → enter your email → **Create subscription**.
4. Open the email from AWS and click **Confirm subscription**.
5. Back in the topic, click **Publish message**, type a subject and body → **Publish message**.
6. Check your inbox.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create a topic and save its ARN
TOPIC_ARN=$(aws sns create-topic --name alerts --query TopicArn --output text)

# Subscribe your email (then confirm via the email AWS sends)
aws sns subscribe --topic-arn $TOPIC_ARN --protocol email --notification-endpoint you@example.com

# Publish a test message
aws sns publish --topic-arn $TOPIC_ARN --subject "Test" --message "Hello from SNS"
```

### Option C – Using Terraform (infrastructure as code)

Written for the AWS provider `~> 6.0`.

```hcl
# A topic for alerts
resource "aws_sns_topic" "alerts" {
  name = "alerts"
}

# Email subscription (you still need to click the confirmation link)
resource "aws_sns_topic_subscription" "me" {
  topic_arn = aws_sns_topic.alerts.arn
  protocol  = "email"
  endpoint  = "you@example.com"
}
```

### Clean up (delete what you made)

1. **SNS** → **Topics** → tick `alerts` → **Delete** → type `delete me`.
2. (Keep it if you use it for budget or CloudWatch alarms.)

## How much does it cost?

Per million publishes, plus per delivery depending on type (HTTP, email, SMS, mobile push). SMS prices vary by country.

Official pricing: <https://aws.amazon.com/sns/pricing/>

## Security tips

- Use topic policies to control who can publish.
- Turn on encryption with KMS for sensitive messages.

## Common mistakes

- Forgetting to confirm email subscriptions.
- Expecting SNS to keep messages if a subscriber is down – use SQS for that.

## Works well with

- [CloudWatch](../management-governance/cloudwatch.md) and [Budgets](../cost-management/budgets.md) – alarms publish to SNS.
- [SQS](sqs.md) – SNS + SQS fan-out.
- [Lambda](../compute/lambda.md) – run code for each message.

## Quick check (test yourself)

1. What is a topic?
   <details><summary>Answer</summary>A named channel that messages are published to and subscribers listen on.</details>
2. Does SNS store messages for later?
   <details><summary>Answer</summary>No. Use SQS if messages need to wait.</details>
3. What does "fan-out" mean?
   <details><summary>Answer</summary>One message being delivered to many subscribers.</details>

## Learn more

- [Amazon SNS Developer Guide](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)
- [Amazon SNS pricing](https://aws.amazon.com/sns/pricing/)
