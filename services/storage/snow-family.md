# AWS Snow Family (Snowball Edge)

**Category:** Storage  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ⛔ **No longer available to new customers.** AWS has stopped offering Snowball Edge devices to new customers. Use [AWS DataSync](../migration-transfer/datasync.md) or AWS Data Transfer Terminal instead. <!-- TODO: verify exact date and recommended alternatives -->

## In one sentence

The Snow Family is a set of rugged physical devices that AWS posts to you, so you can copy huge amounts of data onto them and ship it back.

## Real-life comparison

It's like moving house with a removal van instead of posting your belongings one parcel at a time. When you have a huge amount of stuff, a van is faster.

## What problem does it solve?

Uploading hundreds of terabytes over a normal internet connection could take months. A Snowball device is posted to you, you copy data onto it locally (fast), post it back, and AWS loads it into S3.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Snowball Edge** | A suitcase-sized device with storage and some computing power. |
| **Job** | Your order for a device, saying what to load and where. |
| **Edge computing** | Running programs close to where data is made, e.g. on a ship, without the cloud. |

## How it works (step by step)

1. You create a **job** in the Console.
2. AWS posts you the device.
3. You connect it to your network and copy data on.
4. You post it back.
5. AWS copies the data into your S3 bucket and wipes the device.

## When to use it

- Existing customers moving very large data sets with slow or no internet.
- Collecting data in remote places (ships, field sites).

## When NOT to use it (and what to use instead)

- **New customers.** → Use [DataSync](../migration-transfer/datasync.md) over the network, or [Direct Connect](../networking/direct-connect.md) for a fast private link.
- **Small amounts of data.** → Just upload to [S3](s3.md).

## Real-world example

**Scenario:** A film studio has 300 TB of raw footage on local disks.

**The problem:** Its internet connection would take months to upload it.

**How Snow helps:** The studio orders several devices, copies the footage on in a few days, and posts them back. AWS loads the footage into S3.

**What it looks like:**

```
 Studio disks ─► Snowball Edge ─(courier)─► AWS data centre ─► S3 bucket
```

## Try it yourself

> ⚠️ **Cost warning:** Snow jobs are charged per job and per day on site. Not suitable for a test.

### Option A – Using the AWS Console (clicking in the website)

Not applicable – the service is closed to new customers.

### Option B – Using the AWS CLI (typing commands)

Not applicable – the service is closed to new customers.

### Option C – Using Terraform (infrastructure as code)

Not applicable – physical devices are ordered as jobs.

### Clean up (delete what you made)

Not applicable.

## How much does it cost?

A fee per job, plus charges per extra day you keep the device, plus shipping. Data loaded into S3 is then charged at normal S3 prices.

Official pricing: <https://aws.amazon.com/snowball/pricing/>

## Security tips

- Data on devices is encrypted automatically; keys are held in KMS, not on the device.
- AWS wipes devices after loading your data.

## Common mistakes

- Underestimating how long copying data onto the device takes on a slow local network.

## Works well with

- [S3](s3.md) – where the data ends up.
- [DataSync](../migration-transfer/datasync.md) – the network-based alternative.

## Quick check (test yourself)

1. Why ship data instead of uploading it?
   <details><summary>Answer</summary>For very large amounts, a slow internet connection could take months.</details>
2. Can new customers still order Snowball Edge devices?
   <details><summary>Answer</summary>No – it's closed to new customers.</details>
3. What's a network-based alternative?
   <details><summary>Answer</summary>AWS DataSync.</details>

## Learn more

- [AWS Snowball Edge documentation](https://docs.aws.amazon.com/snowball/)
- [AWS Snowball pricing](https://aws.amazon.com/snowball/pricing/)
