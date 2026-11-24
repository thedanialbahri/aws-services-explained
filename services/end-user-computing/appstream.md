# Amazon AppStream 2.0

**Category:** End-user computing  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

AppStream 2.0 streams individual desktop applications to a user's web browser, without installing them on the user's device.

## Real-life comparison

If WorkSpaces gives you the whole office, AppStream gives you just the one tool you need, delivered to your desk.

## What problem does it solve?

Some software is heavy, Windows-only or hard to install (e.g. engineering or design tools). AppStream runs it in AWS and streams it to any browser.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Image** | The server image with your apps installed. |
| **Fleet** | The servers that stream apps. |
| **Stack** | Settings that connect users to a fleet. |

## How it works (step by step)

1. Build an image with your apps.
2. Create a fleet from it.
3. Create a stack and add users.
4. Users open a link and use the app in their browser.

## When to use it

- Software for students, trainees, or customers' trial access.

## When NOT to use it (and what to use instead)

- **Users need a full desktop.** → [WorkSpaces](workspaces.md).

## Real-world example

**Scenario:** A college teaches CAD software that only runs on powerful Windows PCs.

**How it helps:** Students use it through a browser on Chromebooks.

**What it looks like:**

```
 Student's browser ══stream══► AppStream fleet (CAD app)
```

## Try it yourself

> ⚠️ **Cost warning:** Fleet instances are charged per hour while running, plus user fees for some licences. Only browse unless you're prepared to pay.

### Option A – Using the AWS Console (clicking in the website)

1. Open **AppStream 2.0** → **Get started** and try a sample application if offered.

### Option B – Using the AWS CLI (typing commands)

```bash
aws appstream describe-fleets
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Stop and delete fleets, stacks and images.

## How much does it cost?

Per instance-hour for fleets, plus per-user licence fees for Windows apps.

Official pricing: <https://aws.amazon.com/appstream2/pricing/>

## Security tips

- Control clipboard, file transfer and printing per stack.

## Common mistakes

- Leaving "always-on" fleets running overnight.

## Works well with

- [S3](../storage/s3.md) (home folders), [WorkSpaces](workspaces.md).

## Quick check (test yourself)

1. What does AppStream stream?
   <details><summary>Answer</summary>Individual applications.</details>
2. Where do users run the app?
   <details><summary>Answer</summary>In their web browser.</details>
3. What is a fleet?
   <details><summary>Answer</summary>The servers that stream the apps.</details>

## Learn more

- [Amazon AppStream 2.0 Administration Guide](https://docs.aws.amazon.com/appstream2/latest/developerguide/what-is-appstream.html)
