# AWS SDKs (Software Development Kits)

**Category:** Developer tools  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

The AWS SDKs are code libraries that let your own programs (in Python, JavaScript, Java and more) use AWS services.

## Real-life comparison

The SDK is like a phrasebook for talking to AWS in your programming language – you don't have to learn AWS's raw API "language" yourself.

## What problem does it solve?

Calling AWS's web APIs directly means handling signatures, retries and errors yourself. SDKs do this for you.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Boto3** | The AWS SDK for Python. |
| **Client** | An object that talks to one service. |
| **Credentials chain** | The order the SDK looks for credentials (environment, profile, role). |

## How it works (step by step)

1. Install the SDK (e.g. `pip install boto3`).
2. Create a client for a service.
3. Call methods, e.g. `list_buckets()`.
4. The SDK finds credentials automatically (in AWS, from the role).

## When to use it

- Any app or script that uses AWS from code.

## When NOT to use it (and what to use instead)

- **One-off commands.** → [CLI](cli.md).
- **Creating infrastructure.** → [CDK](cdk.md), Terraform or CloudFormation.

## Real-world example

**Scenario:** A Python script makes a daily list of large files in S3.

**What it looks like:**

```python
# List all buckets using Boto3 (credentials come from your profile or role)
import boto3

s3 = boto3.client("s3")
for bucket in s3.list_buckets()["Buckets"]:
    print(bucket["Name"])
```

## Try it yourself

> ⚠️ **Cost warning:** Free; listing buckets costs nothing meaningful.

### Option A – Using the AWS Console (clicking in the website)

Not applicable – SDKs are used in code. Try it in [CloudShell](cloudshell.md), where Python and Boto3 are usually available.

### Option B – Using the AWS CLI (typing commands)

```bash
# In CloudShell: save the code above as list.py, then run it
python3 list.py
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Delete `list.py`.

## How much does it cost?

Free.

## Security tips

- Never hard-code access keys; let the SDK pick up roles automatically.

## Common mistakes

- Not handling errors and throttling (the SDK retries some, but not all).

## Works well with

- [Lambda](../compute/lambda.md), [EC2](../compute/ec2.md).

## Quick check (test yourself)

1. What is the Python SDK called?
   <details><summary>Answer</summary>Boto3.</details>
2. Where should credentials come from inside AWS?
   <details><summary>Answer</summary>An IAM role.</details>
3. When is the CLI better?
   <details><summary>Answer</summary>For quick, one-off commands.</details>

## Learn more

- [Tools to build on AWS (SDK list)](https://aws.amazon.com/developer/tools/)
