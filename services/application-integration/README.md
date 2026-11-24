# Application integration

These services let different parts of an app – or different apps – **send messages and events to each other** without being tightly joined together.

**Real-life comparison:** In a restaurant, waiters don't walk into the kitchen and wait beside the chef. They pin order tickets on a rail (a **queue** – SQS), the head waiter announces "table 5's food is ready" to everyone who needs to know (a **notification** – SNS), and a manager follows a checklist for big events like weddings (a **workflow** – Step Functions).

Joining parts loosely like this (called **decoupling**) means one part can be slow or broken without bringing down the rest.

## Services in this category

| Service | Level | What it does |
|---------|-------|--------------|
| [Amazon SQS](sqs.md) | 🟢 | A queue that holds messages until a program is ready for them |
| [Amazon SNS](sns.md) | 🟢 | Sends one message to many subscribers (email, SMS, apps) |
| [Amazon EventBridge](eventbridge.md) | 🟡 | Routes events between services based on rules, and runs schedules |
| [AWS Step Functions](step-functions.md) | 🟡 | Joins steps into a visual workflow |
| [Amazon MQ](mq.md) | 🔴 | Managed message brokers (ActiveMQ and RabbitMQ) |
| [AWS AppSync](appsync.md) | 🔴 | Managed GraphQL APIs for apps |

## SQS vs SNS vs EventBridge

| | SQS | SNS | EventBridge |
|---|---|---|---|
| **Pattern** | Queue (one consumer takes each message) | Publish/subscribe (everyone gets a copy) | Event bus with rules |
| **Holds messages?** | Yes, up to 14 days | No | No (can archive and replay) |
| **Good for** | Spreading work, smoothing spikes | Alerts, fan-out | Reacting to AWS and app events, schedules |

[← Back to the main index](../../README.md)
