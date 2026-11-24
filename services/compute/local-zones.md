# AWS Local Zones

**Category:** Compute  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Local Zones are small AWS locations in big cities, so you can run servers very close to the people using them.

## Real-life comparison

A Region is a big out-of-town supermarket. A Local Zone is a small local store of the same chain in the city centre – fewer products, but much closer.

## What problem does it solve?

If your users are in a city far from the nearest Region, every action has a small delay. For video editing, gaming or live trading, that matters. Local Zones put AWS compute and storage in the city itself.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Local Zone** | A small AWS site in a city, linked to a parent Region. |
| **Opt in** | Local Zones are off by default; you choose to turn one on. |
| **Parent Region** | The full Region the Local Zone connects to. |

## How it works (step by step)

1. You **opt in** to a Local Zone in the EC2 settings.
2. You add a subnet in that zone to your VPC.
3. You launch supported services (e.g. EC2, EBS) there.
4. Your app talks to the parent Region for other services.

## When to use it

- Apps needing single-digit millisecond delay for users in a particular city.
- Data that must stay in a particular city or country where there's no Region.

## When NOT to use it (and what to use instead)

- **Most apps.** A Region is close enough.
- **Mobile 5G users specifically.** → [Wavelength](wavelength.md).
- **Hardware in your own building.** → [Outposts](outposts.md).

## Real-world example

**Scenario:** A film studio edits video on cloud workstations.

**The problem:** Editors feel lag because the nearest Region is far away.

**How Local Zones help:** The studio runs workstations in a Local Zone in its city, so editing feels instant.

**What it looks like:**

```
 Editors (city) ──► Local Zone (EC2 workstations) ──► Parent Region (S3, databases)
```

## Try it yourself

> ⚠️ **Cost warning:** Servers in Local Zones usually cost more than in the parent Region. Only browse unless you plan to use one.

### Option A – Using the AWS Console (clicking in the website)

1. Open **EC2** → **Settings** → **Zones** to see which Local Zones your Region offers.

### Option B – Using the AWS CLI (typing commands)

```bash
# List Local Zones and whether you've opted in
aws ec2 describe-availability-zones --all-availability-zones \
  --filters Name=zone-type,Values=local-zone \
  --query 'AvailabilityZones[].[ZoneName,OptInStatus]' --output table
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Nothing to clean up if you only listed zones.

## How much does it cost?

Per hour for resources in the zone (often higher than the parent Region), plus data transfer.

Official pricing: <https://aws.amazon.com/about-aws/global-infrastructure/localzones/pricing/>

## Security tips

- Same as any VPC subnet: tight security groups and private subnets where possible.

## Common mistakes

- Assuming every service exists in a Local Zone – only a subset does.

## Works well with

- [EC2](ec2.md), [EBS](../storage/ebs.md), [VPC](../networking/vpc.md).

## Quick check (test yourself)

1. Are Local Zones on by default?
   <details><summary>Answer</summary>No, you must opt in.</details>
2. What is a parent Region?
   <details><summary>Answer</summary>The full Region a Local Zone connects back to.</details>
3. Why use a Local Zone?
   <details><summary>Answer</summary>To get very low delay for users in a specific city.</details>

## Learn more

- [AWS Local Zones documentation](https://docs.aws.amazon.com/local-zones/latest/ug/what-is-aws-local-zones.html)
- [AWS Local Zones features](https://aws.amazon.com/about-aws/global-infrastructure/localzones/)
