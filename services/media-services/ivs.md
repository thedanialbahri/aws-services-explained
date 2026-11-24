# Amazon Interactive Video Service (IVS)

**Category:** Media services  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

IVS lets you add low-delay live video streaming to your website or app – the same technology behind Twitch.

## Real-life comparison

It's like hiring a TV broadcast van: you point your camera, and it handles getting the live picture to thousands of viewers.

## What problem does it solve?

Building live streaming infrastructure is very hard. IVS gives you a stream key and a player.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Channel** | Your live stream. |
| **Ingest server / stream key** | Where and how your broadcast software sends video. |
| **Playback URL** | What viewers' players load. |
| **Real-time stage** | Very low-delay multi-person streams. |

## How it works (step by step)

1. Create a channel.
2. Put the ingest server and stream key into OBS (broadcast software).
3. Start streaming.
4. Viewers watch via the IVS player using the playback URL.

## When to use it

- Live events, classes, auctions, gaming.

## When NOT to use it (and what to use instead)

- **Pre-recorded video.** → [MediaConvert](mediaconvert.md) + CloudFront.

## Real-world example

**Scenario:** A yoga teacher wants to stream live classes on her website.

**How it helps:** She streams from OBS to IVS; students watch in an embedded player.

**What it looks like:**

```
 OBS ──stream key──► IVS channel ──► player on website ──► viewers
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per hour of video input and per hour of video watched. A short test costs little. Delete the channel afterwards.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon IVS** → **Create channel**.
2. Copy the ingest server and stream key into OBS and start streaming.
3. Watch it in the Console's **Live stream** preview.

### Option B – Using the AWS CLI (typing commands)

```bash
aws ivs create-channel --name demo-channel
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_ivs_channel`.

### Clean up (delete what you made)

Delete the channel.

## How much does it cost?

Per hour of input and per hour of output (viewer hours), by quality.

Official pricing: <https://aws.amazon.com/ivs/pricing/>

## Security tips

- Keep stream keys secret; use private channels with playback tokens if needed.

## Common mistakes

- Sharing the stream key on screen.

## Works well with

- [Lambda](../compute/lambda.md), [S3](../storage/s3.md) (record to S3).

## Quick check (test yourself)

1. What do you put into OBS?
   <details><summary>Answer</summary>The ingest server and stream key.</details>
2. What do viewers use?
   <details><summary>Answer</summary>The playback URL in a player.</details>
3. Is IVS for pre-recorded video?
   <details><summary>Answer</summary>No, it's for live streaming.</details>

## Learn more

- [Amazon IVS User Guide](https://docs.aws.amazon.com/ivs/latest/LowLatencyUserGuide/what-is.html)
