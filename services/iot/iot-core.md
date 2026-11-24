# AWS IoT Core

**Category:** Internet of Things (IoT)  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

IoT Core securely connects devices to AWS so they can send data and receive commands, and routes their messages to other AWS services.

## Real-life comparison

IoT Core is like a building's post room for thousands of smart gadgets: it checks each gadget's ID, receives their messages and forwards them to the right departments.

## What problem does it solve?

Connecting many devices securely – each with its own identity – and handling millions of messages is hard. IoT Core does it with a lightweight protocol called MQTT.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Thing** | A device registered in IoT Core. |
| **MQTT** | A lightweight messaging protocol for devices. |
| **Topic** | A message channel, e.g. `greenhouse/1/temp`. |
| **Certificate** | The device's digital ID. |
| **Rule** | Sends matching messages to services like DynamoDB or Lambda. |
| **Device shadow** | A stored copy of a device's last known state. |

## How it works (step by step)

1. Register a **thing** and give it a certificate.
2. The device connects over MQTT with TLS.
3. It publishes messages to topics.
4. **Rules** forward messages to AWS services.

## When to use it

- Sensors, smart devices, connected products.

## When NOT to use it (and what to use instead)

- **Industrial plant data modelling.** → [IoT SiteWise](iot-sitewise.md) (often alongside IoT Core).

## Real-world example

**Scenario:** A farm has soil moisture sensors in each field.

**How it helps:** Sensors publish readings; a rule stores them in DynamoDB and another alerts the farmer via SNS when soil is too dry.

**What it looks like:**

```
 Sensors ──MQTT──► IoT Core ──rule──► DynamoDB
                           └─rule──► SNS (dry soil alert)
```

## Try it yourself

> ⚠️ **Cost warning:** Free Tier for connectivity and messages for new accounts; then per million messages and connection minutes.

### Option A – Using the AWS Console (clicking in the website)

1. Open **AWS IoT Core** → **MQTT test client**.
2. Subscribe to `test/#`.
3. Publish a message to `test/hello` and watch it arrive.

### Option B – Using the AWS CLI (typing commands)

```bash
# Publish a test message to a topic
aws iot-data publish --topic test/hello --cli-binary-format raw-in-base64-out \
  --payload '{"temp": 21}'
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_iot_thing`, `aws_iot_certificate` and `aws_iot_topic_rule`.

### Clean up (delete what you made)

Delete test things, certificates and rules.

## How much does it cost?

Per million messages, per connection minute, plus rules and shadow operations.

Official pricing: <https://aws.amazon.com/iot-core/pricing/>

## Security tips

- One certificate per device; least-privilege IoT policies.

## Common mistakes

- Sharing one certificate across all devices.

## Works well with

- [Lambda](../compute/lambda.md), [DynamoDB](../databases/dynamodb.md), [Timestream](../databases/timestream.md).

## Quick check (test yourself)

1. What protocol do devices usually use?
   <details><summary>Answer</summary>MQTT.</details>
2. What is a device shadow?
   <details><summary>Answer</summary>A stored copy of a device's last known state.</details>
3. What sends messages to other services?
   <details><summary>Answer</summary>Rules.</details>

## Learn more

- [AWS IoT Core Developer Guide](https://docs.aws.amazon.com/iot/latest/developerguide/what-is-aws-iot.html)
