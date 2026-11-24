# AWS IoT SiteWise

**Category:** Internet of Things (IoT)  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

IoT SiteWise collects, organises and monitors data from industrial equipment like pumps, turbines and production lines.

## Real-life comparison

It's like a factory's control room wall of dials, but in the cloud and organised by site, line and machine.

## What problem does it solve?

Industrial data comes from many machines in different formats. SiteWise models the equipment and calculates measures like efficiency automatically.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Asset** | A machine or piece of equipment. |
| **Asset model** | A template for a type of machine. |
| **Gateway** | Collects data from equipment on site. |
| **Metric** | A calculated value, e.g. hourly output. |

## How it works (step by step)

1. Create asset models and assets.
2. Send data via a SiteWise gateway or IoT Core.
3. View dashboards and set alarms.

## When to use it

- Manufacturing, energy, utilities.

## When NOT to use it (and what to use instead)

- **Consumer gadgets.** → [IoT Core](iot-core.md).

## Real-world example

**Scenario:** A bottling plant wants to track machine downtime.

**How it helps:** SiteWise collects line data and shows overall equipment effectiveness per line.

**What it looks like:**

```
 Machines ──► SiteWise Edge gateway ──► SiteWise (assets, metrics) ──► dashboards
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per data ingested, stored and calculated. Use the demo only.

### Option A – Using the AWS Console (clicking in the website)

1. Open **IoT SiteWise** and create the **demo** (it creates sample wind farm data – delete it afterwards).

### Option B – Using the AWS CLI (typing commands)

```bash
aws iotsitewise list-assets --filter TOP_LEVEL
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete the demo (it's a CloudFormation stack).

## How much does it cost?

Per message ingested, data stored and metrics computed.

Official pricing: <https://aws.amazon.com/iot-sitewise/pricing/>

## Security tips

- Separate industrial networks from office networks.

## Common mistakes

- Leaving the demo running.

## Works well with

- [IoT Core](iot-core.md), [IoT Greengrass](iot-greengrass.md).

## Quick check (test yourself)

1. What is an asset?
   <details><summary>Answer</summary>A machine or piece of equipment.</details>
2. What collects data on site?
   <details><summary>Answer</summary>A SiteWise gateway.</details>
3. Who uses SiteWise?
   <details><summary>Answer</summary>Industrial companies like manufacturers and utilities.</details>

## Learn more

- [AWS IoT SiteWise User Guide](https://docs.aws.amazon.com/iot-sitewise/latest/userguide/what-is-sitewise.html)
