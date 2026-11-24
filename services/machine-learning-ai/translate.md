# Amazon Translate

**Category:** Machine learning & AI  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Translate converts text from one language to another using machine translation.

## Real-life comparison

It's like a fast interpreter who works on written text, any time of day.

## What problem does it solve?

Translating websites, support tickets or product descriptions by hand is slow and costly. Translate does it instantly at scale.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Real-time translation** | Translate text immediately via the API. |
| **Batch translation** | Translate many documents in S3. |
| **Custom terminology** | Make sure brand names are translated your way. |

## How it works (step by step)

1. Send text with source and target languages (or auto-detect).
2. Get the translation back.

## When to use it

- Multilingual websites, chat, reviews, documents.

## When NOT to use it (and what to use instead)

- **Legal or medical documents needing guaranteed accuracy.** Use a professional translator to check.

## Real-world example

**Scenario:** A UK shop gets reviews in Polish and Spanish.

**How it helps:** Reviews are translated to English automatically for the support team.

**What it looks like:**

```
 Review (pl) ──► Translate ──► Review (en)
```

## Try it yourself

> ⚠️ **Cost warning:** Free Tier for some characters per month for new accounts; then per million characters.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Translate** → **Real-time translation**.
2. Source **Auto**, target **Welsh**, type "Good morning, how are you?"

### Option B – Using the AWS CLI (typing commands)

```bash
aws translate translate-text --source-language-code en --target-language-code fr \
  --text "Where is the train station?"
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Nothing to clean up.

## How much does it cost?

Per million characters translated.

Official pricing: <https://aws.amazon.com/translate/pricing/>

## Security tips

- Avoid sending unnecessary personal data.

## Common mistakes

- Assuming translations are perfect.

## Works well with

- [Transcribe](transcribe.md), [Comprehend](comprehend.md), [Polly](polly.md).

## Quick check (test yourself)

1. What is custom terminology for?
   <details><summary>Answer</summary>Controlling how specific terms are translated.</details>
2. Can it detect the source language?
   <details><summary>Answer</summary>Yes, with auto-detect.</details>
3. How is it charged?
   <details><summary>Answer</summary>Per character.</details>

## Learn more

- [Amazon Translate Developer Guide](https://docs.aws.amazon.com/translate/latest/dg/what-is.html)
