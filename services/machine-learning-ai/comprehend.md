# Amazon Comprehend

**Category:** Machine learning & AI  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Comprehend reads text and finds meaning in it – the language, key phrases, people and places mentioned, sentiment (positive or negative) and personal data.

## Real-life comparison

It's like a speed-reader who skims thousands of customer emails and tells you which are angry, what they're about and which mention addresses or phone numbers.

## What problem does it solve?

Reading every review, ticket or survey response isn't possible at scale. Comprehend summarises the mood and topics automatically. This is called **NLP** (natural language processing).

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Sentiment** | Positive, negative, neutral or mixed. |
| **Entities** | People, places, organisations, dates. |
| **PII detection** | Finding personal information. |
| **Custom classification** | Training it on your own categories. |

## How it works (step by step)

1. Send text to an API (e.g. `DetectSentiment`).
2. Get structured results with scores.

## When to use it

- Analysing reviews, tickets, social posts; finding PII in text.

## When NOT to use it (and what to use instead)

- **Open-ended summarising or answering questions.** → [Bedrock](bedrock.md).

## Real-world example

**Scenario:** A broadband company gets 5,000 support emails a day.

**How it helps:** Comprehend flags very negative emails for priority handling.

**What it looks like:**

```
 Email ──► Comprehend (sentiment: NEGATIVE 0.97) ──► priority queue
```

## Try it yourself

> ⚠️ **Cost warning:** Free Tier for some text units per month for new accounts; then per unit (100 characters).

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Comprehend** → **Real-time analysis**.
2. Paste a review and click **Analyze**.

### Option B – Using the AWS CLI (typing commands)

```bash
aws comprehend detect-sentiment --language-code en \
  --text "The delivery was late and the box was damaged."
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Nothing to clean up.

## How much does it cost?

Per unit of 100 characters, by feature.

Official pricing: <https://aws.amazon.com/comprehend/pricing/>

## Security tips

- Use PII detection to redact personal data before storing text.

## Common mistakes

- Expecting it to understand sarcasm perfectly.

## Works well with

- [Transcribe](transcribe.md), [S3](../storage/s3.md).

## Quick check (test yourself)

1. What is sentiment?
   <details><summary>Answer</summary>Whether text is positive, negative, neutral or mixed.</details>
2. What is NLP?
   <details><summary>Answer</summary>Natural language processing – computers understanding human language.</details>
3. Can Comprehend find personal data?
   <details><summary>Answer</summary>Yes, with PII detection.</details>

## Learn more

- [Amazon Comprehend Developer Guide](https://docs.aws.amazon.com/comprehend/latest/dg/what-is.html)
