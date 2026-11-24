# AWS Elemental MediaConvert

**Category:** Media services  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

MediaConvert converts video files into the formats and sizes needed for phones, TVs and websites.

## Real-life comparison

It's like a print shop that takes one big poster and makes copies in every size you need – A1 for billboards, A5 for flyers.

## What problem does it solve?

Different devices need different video formats and qualities. Converting (transcoding) yourself needs powerful machines. MediaConvert does it on demand.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Transcoding** | Converting video from one format or size to another. |
| **Job** | One conversion task. |
| **Output group** | A set of outputs, e.g. HLS for streaming. |
| **HLS / DASH** | Formats for adaptive streaming (quality adjusts to the connection). |

## How it works (step by step)

1. Upload a video to S3.
2. Create a job with outputs (e.g. 1080p, 720p, 480p HLS).
3. MediaConvert writes the results back to S3.
4. Serve them via [CloudFront](../networking/cloudfront.md).

## When to use it

- Video-on-demand: courses, marketing videos, user uploads.

## When NOT to use it (and what to use instead)

- **Live streaming.** → [IVS](ivs.md) or AWS Elemental MediaLive.

## Real-world example

**Scenario:** An online cookery school uploads lessons in 4K.

**How it helps:** Each upload triggers a MediaConvert job producing streaming versions for all devices.

**What it looks like:**

```
 S3 upload ──► Lambda ──► MediaConvert job ──► S3 (HLS) ──► CloudFront ──► viewers
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per minute of output video, by resolution and features. A short test clip costs very little.

### Option A – Using the AWS Console (clicking in the website)

1. Upload a short MP4 to S3.
2. Open **MediaConvert** → **Create job**, set the input, add an **MP4** output group at 720p, and choose an S3 destination.
3. Create the job and check the output.

### Option B – Using the AWS CLI (typing commands)

```bash
aws mediaconvert list-jobs --max-results 5
```

### Option C – Using Terraform (infrastructure as code)

Not applicable – jobs are created on demand.

### Clean up (delete what you made)

Delete the input and output files from S3.

## How much does it cost?

Per minute of output, by resolution, codec and tier.

Official pricing: <https://aws.amazon.com/mediaconvert/pricing/>

## Security tips

- Keep source buckets private; serve outputs through CloudFront.

## Common mistakes

- Creating far more output sizes than you need.

## Works well with

- [S3](../storage/s3.md), [CloudFront](../networking/cloudfront.md), [Lambda](../compute/lambda.md).

## Quick check (test yourself)

1. What is transcoding?
   <details><summary>Answer</summary>Converting video from one format or size to another.</details>
2. Where do outputs go?
   <details><summary>Answer</summary>S3.</details>
3. For live streaming, what's better?
   <details><summary>Answer</summary>Amazon IVS or MediaLive.</details>

## Learn more

- [AWS Elemental MediaConvert User Guide](https://docs.aws.amazon.com/mediaconvert/latest/ug/what-is.html)
