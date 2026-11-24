# Amazon Polly

**Category:** Machine learning & AI  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Polly turns written text into natural-sounding speech in many languages and voices.

## Real-life comparison

Polly is like having a professional voice actor on call who'll read any text out loud instantly, in many accents.

## What problem does it solve?

Recording audio for every piece of text (announcements, articles, app messages) is slow and expensive. Polly generates it on demand.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Voice** | A particular speaker, e.g. "Amy" (British English). |
| **Engine** | Voice quality type: standard, neural, long-form, generative. |
| **SSML** | Tags that control pauses, emphasis and pronunciation. |

## How it works (step by step)

1. Send text and choose a voice.
2. Polly returns an audio file (e.g. MP3) or stream.

## When to use it

- Accessibility (reading articles aloud), e-learning, phone systems.

## When NOT to use it (and what to use instead)

- **Speech to text.** → [Transcribe](transcribe.md).

## Real-world example

**Scenario:** A news site wants a "listen to this article" button.

**How it helps:** Lambda sends each new article to Polly and saves the MP3 in S3.

**What it looks like:**

```
 New article ──► Lambda ──► Polly ──► MP3 in S3 ──► play button
```

## Try it yourself

> ⚠️ **Cost warning:** Free Tier for a number of characters per month for new accounts; then per million characters.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Polly**.
2. Type a sentence, choose **Neural** and a British English voice.
3. Click **Listen**, then **Download**.

### Option B – Using the AWS CLI (typing commands)

```bash
# Turn text into an MP3 using a British English neural voice
aws polly synthesize-speech --engine neural --voice-id Amy --output-format mp3 \
  --text "Hello from Amazon Polly" hello.mp3
```

### Option C – Using Terraform (infrastructure as code)

Not applicable – Polly is called on demand.

### Clean up (delete what you made)

Delete the MP3 file.

## How much does it cost?

Per million characters, by engine.

Official pricing: <https://aws.amazon.com/polly/pricing/>

## Security tips

- Give apps permission for `polly:SynthesizeSpeech` only.

## Common mistakes

- Regenerating the same audio repeatedly – save and reuse it.

## Works well with

- [Lambda](../compute/lambda.md), [S3](../storage/s3.md).

## Quick check (test yourself)

1. What does Polly do?
   <details><summary>Answer</summary>Turns text into speech.</details>
2. What is SSML for?
   <details><summary>Answer</summary>Controlling how text is spoken (pauses, emphasis).</details>
3. Which service does the opposite?
   <details><summary>Answer</summary>Amazon Transcribe.</details>

## Learn more

- [Amazon Polly Developer Guide](https://docs.aws.amazon.com/polly/latest/dg/what-is.html)
