# Amazon Transcribe

**Category:** Machine learning & AI  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Transcribe turns speech in audio or video into written text.

## Real-life comparison

It's like a fast typist who listens to recordings and writes down everything that's said, including who said it.

## What problem does it solve?

Typing up meetings, calls or videos by hand takes hours. Transcribe does it automatically.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Transcription job** | One audio file being converted. |
| **Speaker diarisation** | Labelling who spoke when. |
| **Custom vocabulary** | Teaching it special words (product names). |
| **Streaming** | Live transcription as people talk. |

## How it works (step by step)

1. Upload audio to S3.
2. Start a transcription job.
3. Download the text result (JSON, or subtitles).

## When to use it

- Meeting notes, subtitles, call analysis.

## When NOT to use it (and what to use instead)

- **Text to speech.** → [Polly](polly.md).

## Real-world example

**Scenario:** A podcast wants transcripts for every episode.

**How it helps:** New episodes in S3 trigger a Transcribe job; the text is published with the episode.

**What it looks like:**

```
 Audio in S3 ──► Transcribe ──► transcript in S3
```

## Try it yourself

> ⚠️ **Cost warning:** Free Tier for some minutes per month for new accounts; then per second of audio.

### Option A – Using the AWS Console (clicking in the website)

1. Upload a short MP3 to S3.
2. Open **Amazon Transcribe** → **Create job** → choose the file and **English, British**.
3. When complete, read the transcript.

### Option B – Using the AWS CLI (typing commands)

```bash
aws transcribe start-transcription-job --transcription-job-name demo1 \
  --language-code en-GB --media MediaFileUri=s3://my-example-bucket-12345/talk.mp3
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Delete the job and audio file.

## How much does it cost?

Per second of audio processed (minimum per request).

Official pricing: <https://aws.amazon.com/transcribe/pricing/>

## Security tips

- Recordings may contain personal data – encrypt and delete when done.

## Common mistakes

- Choosing the wrong language code (e.g. en-US for British speakers).

## Works well with

- [S3](../storage/s3.md), [Comprehend](comprehend.md), [Translate](translate.md).

## Quick check (test yourself)

1. What does Transcribe produce?
   <details><summary>Answer</summary>Text from speech.</details>
2. What is speaker diarisation?
   <details><summary>Answer</summary>Labelling who spoke when.</details>
3. How do you add special words?
   <details><summary>Answer</summary>A custom vocabulary.</details>

## Learn more

- [Amazon Transcribe Developer Guide](https://docs.aws.amazon.com/transcribe/latest/dg/what-is.html)
