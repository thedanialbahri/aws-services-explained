# Amazon Lex

**Category:** Machine learning & AI  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Lex lets you build chatbots and voice bots that understand what people say or type and respond.

## Real-life comparison

Lex is like training a receptionist with a script: "If someone wants to book an appointment, ask which day and what time."

## What problem does it solve?

Customers ask the same simple questions repeatedly. A bot handles them 24/7, passing harder ones to people.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Bot** | Your chatbot. |
| **Intent** | What the user wants, e.g. `BookAppointment`. |
| **Utterance** | Example phrases, e.g. "I'd like to book". |
| **Slot** | A detail to collect, e.g. date. |

## How it works (step by step)

1. Create a bot and intents.
2. Add sample utterances and slots.
3. Build and test.
4. Connect to a website, app or [Amazon Connect](../business-applications/connect.md) phone line; use Lambda for logic.

## When to use it

- Booking, FAQs, simple support.

## When NOT to use it (and what to use instead)

- **Open-ended conversations or answering from documents.** → [Bedrock](bedrock.md) (Lex can also use generative AI features).

## Real-world example

**Scenario:** A GP surgery wants to handle repeat appointment requests by phone.

**How it helps:** A Lex bot on Amazon Connect collects the patient's preferred day and books it.

**What it looks like:**

```
 Caller ──► Amazon Connect ──► Lex bot (BookAppointment) ──► Lambda ──► booking system
```

## Try it yourself

> ⚠️ **Cost warning:** Free Tier for some requests in the first year for new accounts; then per request.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Lex** → **Create bot** → **Create example bot** → **BookTrip**.
2. Build it and test in the chat window.

### Option B – Using the AWS CLI (typing commands)

```bash
aws lexv2-models list-bots
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete the bot.

## How much does it cost?

Per text or speech request.

Official pricing: <https://aws.amazon.com/lex/pricing/>

## Security tips

- Don't collect more personal data than needed.

## Common mistakes

- Too few sample utterances, so the bot misunderstands people.

## Works well with

- [Amazon Connect](../business-applications/connect.md), [Lambda](../compute/lambda.md).

## Quick check (test yourself)

1. What is an intent?
   <details><summary>Answer</summary>What the user wants to do.</details>
2. What is a slot?
   <details><summary>Answer</summary>A detail the bot collects, like a date.</details>
3. Where does business logic usually run?
   <details><summary>Answer</summary>In a Lambda function.</details>

## Learn more

- [Amazon Lex V2 Developer Guide](https://docs.aws.amazon.com/lexv2/latest/dg/what-is.html)
