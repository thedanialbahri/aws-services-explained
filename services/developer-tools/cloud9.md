# AWS Cloud9

**Category:** Developer tools  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ⛔ **No longer available to new customers.** Use [CloudShell](cloudshell.md), VS Code with the AWS Toolkit, or a code editor on an EC2 instance instead. <!-- TODO: verify current status -->

## In one sentence

Cloud9 was a code editor that ran in your web browser, connected to an EC2 server.

## Real-life comparison

It was like a desk with a computer that you could reach from any internet café.

## What problem does it solve?

It gave developers a ready-made coding setup without installing anything locally.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **IDE** | Integrated Development Environment – a code editor with extra tools. |
| **Environment** | A Cloud9 workspace backed by an EC2 instance. |

## How it works (step by step)

1. An environment ran on an EC2 instance.
2. You opened the IDE in your browser.
3. It stopped the instance automatically when idle.

## When to use it

- Existing customers only.

## When NOT to use it (and what to use instead)

- **New users.** → [CloudShell](cloudshell.md) for commands, or VS Code with the AWS Toolkit.

## Real-world example

**Scenario:** A coding bootcamp used Cloud9 so students didn't need to install anything.

**Today:** New bootcamps use CloudShell or browser-based VS Code alternatives.

**What it looks like:**

```
 Browser ──► Cloud9 IDE ──► EC2 instance
```

## Try it yourself

> ⚠️ **Cost warning:** Not applicable for new customers.

### Option A – Using the AWS Console (clicking in the website)

Not applicable – closed to new customers.

### Option B – Using the AWS CLI (typing commands)

Not applicable.

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Existing users: delete environments you no longer need (this also deletes the EC2 instance).

## How much does it cost?

No charge for Cloud9 itself; existing users pay for the EC2 instance and storage.

## Security tips

- Existing users: don't store long-term credentials in environments.

## Common mistakes

- Following old tutorials that start with "Create a Cloud9 environment".

## Works well with

- [CloudShell](cloudshell.md), [EC2](../compute/ec2.md).

## Quick check (test yourself)

1. Can new customers use Cloud9?
   <details><summary>Answer</summary>No.</details>
2. What's a quick alternative for running AWS commands?
   <details><summary>Answer</summary>CloudShell.</details>
3. What was a Cloud9 environment backed by?
   <details><summary>Answer</summary>An EC2 instance.</details>

## Learn more

- [AWS Cloud9 documentation](https://docs.aws.amazon.com/cloud9/)
