# AWS Ground Station

**Category:** Specialist  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Ground Station lets satellite operators talk to their satellites and download data using AWS-run antennas around the world.

## Real-life comparison

It's like renting time on a radio telescope instead of building your own – pay for each time you use it.

## What problem does it solve?

Building ground stations (antennas) is extremely expensive. Ground Station lets you book antenna time and send the data straight into AWS.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Contact** | A scheduled time when a satellite passes over an antenna. |
| **Mission profile** | Settings for how to communicate with your satellite. |

## How it works (step by step)

1. Onboard your satellite.
2. Schedule contacts.
3. Data is downloaded into your VPC/S3 for processing.

## When to use it

- Satellite companies, universities and research groups.

## When NOT to use it (and what to use instead)

- **Using satellite images from others.** → Buy data through [Data Exchange](../analytics/data-exchange.md) or open data sets.

## Real-world example

**Scenario:** A small university satellite team needs to download images daily.

**How it helps:** They book contacts and process the images in AWS.

**What it looks like:**

```
 Satellite ──radio──► AWS antenna ──► your VPC / S3 ──► processing
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per minute of antenna time. Requires a licensed satellite – not for personal learning.

### Option A – Using the AWS Console (clicking in the website)

Not applicable without a satellite.

### Option B – Using the AWS CLI (typing commands)

```bash
aws groundstation list-ground-stations
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Nothing to clean up.

## How much does it cost?

Per minute of antenna access (on-demand or reserved).

Official pricing: <https://aws.amazon.com/ground-station/pricing/>

## Security tips

- Data is encrypted in transit; protect satellite command access tightly.

## Common mistakes

- Not applicable for most readers.

## Works well with

- [S3](../storage/s3.md), [EC2](../compute/ec2.md).

## Quick check (test yourself)

1. What is a contact?
   <details><summary>Answer</summary>A scheduled time a satellite passes over an antenna.</details>
2. Who uses Ground Station?
   <details><summary>Answer</summary>Satellite operators and researchers.</details>
3. How is it charged?
   <details><summary>Answer</summary>Per minute of antenna time.</details>

## Learn more

- [AWS Ground Station User Guide](https://docs.aws.amazon.com/ground-station/latest/ug/what-is-aws-ground-station.html)
