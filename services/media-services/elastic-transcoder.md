# Amazon Elastic Transcoder

**Category:** Media services  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ⛔ **No longer available.** Amazon Elastic Transcoder was discontinued on 13 November 2025. Use [AWS Elemental MediaConvert](mediaconvert.md) instead.

## In one sentence

Elastic Transcoder was an older AWS service for converting video files into other formats.

## Real-life comparison

It was the older model of a photocopier, replaced by a newer one (MediaConvert) that does more for less.

## What problem does it solve?

It converted videos for different devices.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Pipeline** | A queue of conversion jobs. |
| **Preset** | Output settings. |

## How it works (step by step)

1. Jobs were added to a pipeline.
2. Files were converted using presets.

## When to use it

- No longer possible.

## When NOT to use it (and what to use instead)

- **All cases.** → [MediaConvert](mediaconvert.md).

## Real-world example

**Scenario:** A training company converted videos with Elastic Transcoder.

**Today:** It uses MediaConvert, which offers more formats.

**What it looks like:**

```
 (old) S3 ──► Elastic Transcoder ✗     (new) S3 ──► MediaConvert ✓
```

## Try it yourself

> ⚠️ **Cost warning:** Not applicable.

### Option A – Using the AWS Console (clicking in the website)

Not applicable – service shut down.

### Option B – Using the AWS CLI (typing commands)

Not applicable.

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Not applicable.

## How much does it cost?

Not applicable.

## Security tips

- Not applicable.

## Common mistakes

- Following old tutorials that use Elastic Transcoder.

## Works well with

- [MediaConvert](mediaconvert.md) (its replacement).

## Quick check (test yourself)

1. Is Elastic Transcoder available?
   <details><summary>Answer</summary>No, it was discontinued on 13 November 2025.</details>
2. What replaces it?
   <details><summary>Answer</summary>AWS Elemental MediaConvert.</details>
3. What did it do?
   <details><summary>Answer</summary>Converted video files into other formats.</details>

## Learn more

- [Support for Amazon Elastic Transcoder ending soon (AWS blog)](https://aws.amazon.com/blogs/media/support-for-amazon-elastic-transcoder-ending-soon/)
