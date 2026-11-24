# AWS Wavelength

**Category:** Compute  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Wavelength runs AWS compute inside mobile phone companies' 5G networks, so apps on phones get very fast responses.

## Real-life comparison

It's like putting a snack bar on the train instead of at the station. Passengers (phone users) don't have to get off to get what they need.

## What problem does it solve?

Data from a phone normally travels through the mobile network and across the internet to an AWS Region. For things like live game streaming or connected cars, that trip adds delay. Wavelength keeps the trip inside the mobile network.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Wavelength Zone** | AWS compute inside a mobile carrier's network. |
| **Carrier gateway** | Connects your app to the mobile network. |
| **Latency** | Delay – the time data takes to travel. |

## How it works (step by step)

1. You opt in to a Wavelength Zone in the Console.
2. You extend your VPC with a subnet in that zone.
3. You launch EC2 servers there.
4. Phones on that carrier's 5G network reach your app with very low delay.

## When to use it

- Live video, AR/VR, multiplayer games, connected vehicles on mobile networks.

## When NOT to use it (and what to use instead)

- **Normal web or mobile apps.** A Region is fine.
- **Low delay for users in a city (not just mobile).** → [Local Zones](local-zones.md).

## Real-world example

**Scenario:** A company streams a cloud game to phones.

**The problem:** Players notice lag.

**How Wavelength helps:** The game servers run in a Wavelength Zone inside the carrier's network, cutting the delay.

**What it looks like:**

```
 Phone ──5G──► Carrier network [Wavelength Zone: EC2] ──► Parent Region (other services)
```

## Try it yourself

> ⚠️ **Cost warning:** Wavelength servers are charged per hour, usually more than in a Region, and are only available in certain carrier locations.

Not applicable for most learners – availability depends on specific mobile carriers and locations.

### Option A – Using the AWS Console (clicking in the website)

1. Open **EC2** → **Settings** → **Zones** to see if any Wavelength Zones are available in your Region. Don't opt in unless you intend to use one.

### Option B – Using the AWS CLI (typing commands)

```bash
# List Wavelength Zones in a Region
aws ec2 describe-availability-zones --all-availability-zones \
  --filters Name=zone-type,Values=wavelength-zone
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Nothing to clean up if you only listed zones.

## How much does it cost?

Per hour for EC2 instances in the zone, plus data transfer.

Official pricing: <https://aws.amazon.com/wavelength/pricing/>

## Security tips

- Expose only the ports your app needs to the carrier network.

## Common mistakes

- Expecting every AWS service to be available in a Wavelength Zone – only a few are.

## Works well with

- [EC2](ec2.md) and [VPC](../networking/vpc.md).

## Quick check (test yourself)

1. Where is Wavelength compute located?
   <details><summary>Answer</summary>Inside mobile carriers' 5G networks.</details>
2. What does it reduce?
   <details><summary>Answer</summary>Latency (delay) for mobile users.</details>
3. Which service gets you closer to users in a city in general?
   <details><summary>Answer</summary>Local Zones.</details>

## Learn more

- [AWS Wavelength documentation](https://docs.aws.amazon.com/wavelength/)
- [AWS Wavelength pricing](https://aws.amazon.com/wavelength/pricing/)
