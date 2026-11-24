# AWS Device Farm

**Category:** Front-end web & mobile  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Device Farm tests your mobile apps and websites on real phones, tablets and browsers hosted by AWS.

## Real-life comparison

It's like a shop with every phone model on display that you can borrow to see how your app looks and works on each one.

## What problem does it solve?

Owning dozens of devices to test on is expensive. Device Farm gives you access to real hardware on demand.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Automated tests** | Scripts that tap and check your app automatically. |
| **Remote access** | Controlling a real device from your browser. |
| **Device pool** | The set of devices to test on. |

## How it works (step by step)

1. Upload your app (APK/IPA) and tests.
2. Choose a device pool.
3. Device Farm runs tests and gives you logs, screenshots and videos.

## When to use it

- Testing apps across many devices before release.

## When NOT to use it (and what to use instead)

- **Early development.** Use emulators on your own computer first.

## Real-world example

**Scenario:** A banking app must work on older Android phones.

**How it helps:** Tests run on 20 real devices; a crash on one model is found before release.

**What it looks like:**

```
 App + tests ──► Device Farm ──► results from real phones
```

## Try it yourself

> ⚠️ **Cost warning:** Some free device minutes for new users; then per device minute or a monthly slot.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Device Farm** (in `us-west-2`) → **Mobile device testing** → **Create project** and explore.

### Option B – Using the AWS CLI (typing commands)

```bash
aws devicefarm list-projects --region us-west-2
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Delete the project.

## How much does it cost?

Per device minute, or flat monthly per device slot.

Official pricing: <https://aws.amazon.com/device-farm/pricing/>

## Security tips

- Don't use real customer accounts in tests.

## Common mistakes

- Testing only on the newest devices.

## Works well with

- [CodePipeline](../developer-tools/codepipeline.md).

## Quick check (test yourself)

1. Are the devices real or simulated?
   <details><summary>Answer</summary>Real.</details>
2. What is a device pool?
   <details><summary>Answer</summary>The set of devices to test on.</details>
3. What do you get back?
   <details><summary>Answer</summary>Logs, screenshots and videos.</details>

## Learn more

- [AWS Device Farm Developer Guide](https://docs.aws.amazon.com/devicefarm/latest/developerguide/welcome.html)
