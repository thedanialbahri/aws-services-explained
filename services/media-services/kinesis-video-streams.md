# Amazon Kinesis Video Streams

**Category:** Media services  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Kinesis Video Streams receives and stores video from cameras and devices so you can play it back or analyse it.

## Real-life comparison

It's like a CCTV recorder in the cloud that many cameras can send to, and that computers can watch and analyse.

## What problem does it solve?

Handling live feeds from many cameras securely, storing them and feeding them to AI is complex. KVS manages ingestion and storage.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Stream** | One camera's video feed. |
| **Producer SDK** | Software on the camera that sends video. |
| **Retention** | How long video is kept. |
| **WebRTC** | Real-time two-way video (e.g. doorbells). |

## How it works (step by step)

1. Create a stream.
2. The camera sends video using the producer SDK.
3. Play back with HLS or process with Rekognition or your own code.

## When to use it

- Smart cameras, doorbells, video analytics.

## When NOT to use it (and what to use instead)

- **Broadcasting to viewers.** → [IVS](ivs.md).

## Real-world example

**Scenario:** A retailer wants to count shoppers entering each store.

**How it helps:** Door cameras stream to KVS; a model counts people.

**What it looks like:**

```
 Cameras ──► Kinesis Video Streams ──► analysis ──► footfall dashboard
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per GB ingested, stored and consumed. Delete streams afterwards.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Kinesis Video Streams** → **Create video stream** and view its settings.

### Option B – Using the AWS CLI (typing commands)

```bash
aws kinesisvideo create-stream --stream-name demo-camera --data-retention-in-hours 1
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_kinesis_video_stream`.

### Clean up (delete what you made)

Delete the stream.

## How much does it cost?

Per GB ingested, per GB-month stored and per GB consumed.

Official pricing: <https://aws.amazon.com/kinesis/video-streams/pricing/>

## Security tips

- Video can contain personal data – follow UK GDPR and CCTV rules.

## Common mistakes

- Keeping footage longer than needed.

## Works well with

- [Rekognition](../machine-learning-ai/rekognition.md), [SageMaker](../machine-learning-ai/sagemaker.md).

## Quick check (test yourself)

1. What sends video to KVS?
   <details><summary>Answer</summary>A camera or device using the producer SDK.</details>
2. What is retention?
   <details><summary>Answer</summary>How long video is kept.</details>
3. For broadcasting live to viewers, which service?
   <details><summary>Answer</summary>Amazon IVS.</details>

## Learn more

- [Kinesis Video Streams Developer Guide](https://docs.aws.amazon.com/kinesisvideostreams/latest/dg/what-is-kinesis-video.html)
