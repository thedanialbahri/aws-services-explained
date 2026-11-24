# Amazon Q

**Category:** Machine learning & AI  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check) <!-- TODO: verify current Amazon Q product names and packaging -->

## In one sentence

Amazon Q is a family of AI assistants: Q Developer helps with code and AWS questions, and Q Business answers questions using your company's data.

## Real-life comparison

Amazon Q is like a knowledgeable colleague who's read all the AWS manuals (Q Developer) or all your company's documents (Q Business), and answers questions instantly.

## What problem does it solve?

Finding answers in documentation, writing boilerplate code or searching internal wikis takes time. Q answers in plain English inside the tools you already use.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Q Developer** | Coding and AWS assistant in the Console, IDEs and command line. |
| **Q Business** | Assistant connected to company data sources. |
| **Free / Pro tier** | Usage levels with different limits. |

## How it works (step by step)

1. Open Q in the AWS Console (chat icon) or install the IDE extension.
2. Ask a question or request code.
3. Review and use the answer.

## When to use it

- Learning AWS, writing and explaining code, troubleshooting.

## When NOT to use it (and what to use instead)

- **Building your own AI product.** → [Bedrock](bedrock.md).

## Real-world example

**Scenario:** A junior engineer doesn't understand an IAM error.

**How it helps:** They ask Q Developer in the Console, which explains the missing permission.

**What it looks like:**

```
 You ──question──► Amazon Q ──► explanation + suggested fix
```

## Try it yourself

> ⚠️ **Cost warning:** Q Developer has a free tier with monthly limits; Pro and Q Business are charged per user.

### Option A – Using the AWS Console (clicking in the website)

1. Click the Amazon Q icon in the Console.
2. Ask: "What's the difference between a security group and a network ACL?"

### Option B – Using the AWS CLI (typing commands)

Not applicable – use the Console chat or the IDE/CLI tooling from the Q Developer docs.

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Nothing to clean up.

## How much does it cost?

Free tier for Q Developer; per-user subscriptions for Pro and Business.

Official pricing: <https://aws.amazon.com/q/pricing/>

## Security tips

- Don't paste secrets into chats.

## Common mistakes

- Copying code without understanding or testing it.

## Works well with

- [IAM](../security-identity-compliance/iam.md), [CloudShell](../developer-tools/cloudshell.md).

## Quick check (test yourself)

1. Which Q helps with code?
   <details><summary>Answer</summary>Amazon Q Developer.</details>
2. Which Q uses company data?
   <details><summary>Answer</summary>Amazon Q Business.</details>
3. Should you trust its code without testing?
   <details><summary>Answer</summary>No.</details>

## Learn more

- [Amazon Q Developer User Guide](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/what-is.html)
