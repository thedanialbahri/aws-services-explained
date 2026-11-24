# AWS Outposts

**Category:** Compute  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Outposts puts real AWS hardware in your own building, so you can run AWS services on site with the same tools you use in the cloud.

## Real-life comparison

It's like having a branch of your bank inside your office. Same bank, same rules, same card – just in your building.

## What problem does it solve?

Some workloads must stay on site: data that legally can't leave a country, or factory systems that need very fast responses. Outposts lets these use AWS services and tools without moving to an AWS Region.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Outpost rack** | A full rack of AWS servers installed in your data centre. |
| **Outpost server** | A smaller version for sites with less space. |
| **Parent Region** | The AWS Region your Outpost connects back to. |
| **Hybrid cloud** | Using both your own site and the cloud together. |

## How it works (step by step)

1. You order an Outpost from AWS.
2. AWS delivers, installs and maintains the hardware.
3. It connects back to its parent Region.
4. You launch EC2, EBS, ECS and other supported services on it from the normal Console.

## When to use it

- Very low delay to on-site equipment (factories, hospitals).
- Data that must stay in a specific location.

## When NOT to use it (and what to use instead)

- **Most workloads.** A normal AWS Region is simpler and cheaper.
- **You just need to be closer to users in a city.** → [Local Zones](local-zones.md).

## Real-world example

**Scenario:** A car factory uses machines that must respond within milliseconds.

**The problem:** Sending data to a distant Region is too slow.

**How Outposts helps:** An Outpost rack in the factory runs the control software on EC2, using the same tools as the cloud.

**What it looks like:**

```
 Factory machines ──► Outpost rack (in factory) ──link──► Parent AWS Region
```

## Try it yourself

> ⚠️ **Cost warning:** Outposts is a long-term commitment, priced for businesses.

Not applicable for personal learning – it requires physical hardware installed by AWS. You can read about it in the Console under **AWS Outposts**.

### Option A – Using the AWS Console (clicking in the website)

Not applicable – needs a purchased Outpost.

### Option B – Using the AWS CLI (typing commands)

Not applicable – needs a purchased Outpost.

### Option C – Using Terraform (infrastructure as code)

Not applicable – needs a purchased Outpost.

### Clean up (delete what you made)

Not applicable.

## How much does it cost?

Paid as a term commitment (typically 3 years) for the hardware configuration you choose, upfront or monthly.

Official pricing: <https://aws.amazon.com/outposts/rack/pricing/>

## Security tips

- You are responsible for the physical security of the room the Outpost sits in.

## Common mistakes

- Choosing Outposts when a nearby Region or Local Zone would work.

## Works well with

- [EC2](ec2.md), [EBS](../storage/ebs.md), [ECS](../containers/ecs.md) – run on Outposts.

## Quick check (test yourself)

1. Where does an Outpost physically sit?
   <details><summary>Answer</summary>In your own building or data centre.</details>
2. Who maintains the hardware?
   <details><summary>Answer</summary>AWS.</details>
3. What's a lighter option for being close to users in a city?
   <details><summary>Answer</summary>AWS Local Zones.</details>

## Learn more

- [AWS Outposts documentation](https://docs.aws.amazon.com/outposts/)
- [AWS Outposts pricing](https://aws.amazon.com/outposts/rack/pricing/)
