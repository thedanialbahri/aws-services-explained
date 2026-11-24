# AWS CloudShell

**Category:** Developer tools  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

CloudShell is a terminal inside the AWS Console, already signed in as you, with the AWS CLI and common tools pre-installed.

## Real-life comparison

It's like a hotel room with a kettle, tea and milk already waiting – you don't have to bring your own.

## What problem does it solve?

Installing and configuring the CLI on your computer takes time (and work laptops may block it). CloudShell is ready in seconds.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Home directory** | 1 GB of storage per Region that's kept between sessions. |
| **Environment** | Your personal CloudShell machine. |

## How it works (step by step)

1. Click the CloudShell icon (`>_`) in the Console's top bar.
2. A terminal opens, signed in with your Console permissions.
3. Run AWS CLI commands, Python, git and more.

## When to use it

- Quick commands and learning the CLI.

## When NOT to use it (and what to use instead)

- **Long-running jobs or heavy work.** → [EC2](../compute/ec2.md).

## Real-world example

**Scenario:** An engineer on a locked-down work laptop needs to list S3 buckets.

**How it helps:** They open CloudShell and run `aws s3 ls` immediately.

**What it looks like:**

```
 Browser ──► AWS Console ──► CloudShell terminal (already signed in)
```

## Try it yourself

> ⚠️ **Cost warning:** Free (you pay for resources your commands create).

### Option A – Using the AWS Console (clicking in the website)

1. Sign in to the Console (Region **eu-west-2**).
2. Click the `>_` icon at the top.
3. Type `aws sts get-caller-identity` and press Enter.
4. Type `echo "hello" > notes.txt`, close CloudShell, open it again, then `cat notes.txt` – your file is still there.

### Option B – Using the AWS CLI (typing commands)

CloudShell *is* where you type CLI commands – see the [CLI page](cli.md).

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

1. In CloudShell, type `rm notes.txt`.

## How much does it cost?

Free.

## Security tips

- CloudShell has your permissions – be careful with delete commands.

## Common mistakes

- Storing important files there – home directories can be deleted after long inactivity.

## Works well with

- [AWS CLI](cli.md).

## Quick check (test yourself)

1. Do you need to set up credentials in CloudShell?
   <details><summary>Answer</summary>No, it uses your Console sign-in.</details>
2. How much persistent storage do you get?
   <details><summary>Answer</summary>1 GB per Region.</details>
3. Is it good for long jobs?
   <details><summary>Answer</summary>No – use EC2.</details>

## Learn more

- [AWS CloudShell User Guide](https://docs.aws.amazon.com/cloudshell/latest/userguide/welcome.html)
