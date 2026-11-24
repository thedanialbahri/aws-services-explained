# AWS IoT Greengrass

**Category:** Internet of Things (IoT)  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Greengrass runs your code and AWS features on devices at the edge (on site), so they can act locally even when the internet is down.

## Real-life comparison

It's like giving a shop's manager authority to make decisions on the spot, instead of phoning head office every time.

## What problem does it solve?

Some decisions must happen instantly or work offline (a factory safety stop). Greengrass runs logic on the device and syncs with the cloud when it can.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Core device** | A device running Greengrass software. |
| **Component** | A piece of software deployed to devices. |
| **Edge** | Computing close to where data is created. |

## How it works (step by step)

1. Install Greengrass on a Linux or Windows device.
2. Deploy components from the cloud.
3. Devices run them locally and talk to IoT Core.

## When to use it

- Factories, shops, vehicles – local processing and offline operation.

## When NOT to use it (and what to use instead)

- **Simple sensors that just send data.** → [IoT Core](iot-core.md).

## Real-world example

**Scenario:** A warehouse camera must spot blocked fire exits instantly.

**How it helps:** A model runs on a Greengrass device next to the camera and raises a local alarm.

**What it looks like:**

```
 Camera ──► Greengrass device (local model) ──alarm──► sends summary to IoT Core
```

## Try it yourself

> ⚠️ **Cost warning:** Small charge per active core device per month after any free tier.

### Option A – Using the AWS Console (clicking in the website)

1. Open **IoT Greengrass** → **Set up one core device** to see the install steps (a Raspberry Pi or Linux VM works).

### Option B – Using the AWS CLI (typing commands)

```bash
aws greengrassv2 list-core-devices
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete the core device and its thing in IoT Core; uninstall the software.

## How much does it cost?

Per active core device per month.

Official pricing: <https://aws.amazon.com/greengrass/pricing/>

## Security tips

- Keep device software updated; protect device certificates.

## Common mistakes

- Running heavy models on underpowered devices.

## Works well with

- [IoT Core](iot-core.md), [SageMaker](../machine-learning-ai/sagemaker.md).

## Quick check (test yourself)

1. What is the edge?
   <details><summary>Answer</summary>Computing close to where data is created.</details>
2. Can Greengrass work offline?
   <details><summary>Answer</summary>Yes.</details>
3. What is a component?
   <details><summary>Answer</summary>Software deployed to devices.</details>

## Learn more

- [AWS IoT Greengrass V2 Developer Guide](https://docs.aws.amazon.com/greengrass/v2/developerguide/what-is-iot-greengrass.html)
