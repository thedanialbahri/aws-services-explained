# Amazon Q (now AWS assistant, Kiro and AWS Quick)

**Category:** Machine learning & AI  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ⛔ **The Amazon Q name is being retired.** Here's where each part has gone:
> - **Amazon Q Developer in the Console and mobile app** → renamed **AWS assistant** (5 November 2026). Still available.
> - **Amazon Q Developer in your IDE (code editor)** → closed to new sign-ups on 15 May 2026, end of support 30 April 2027. Use **[Kiro](https://kiro.dev/)** instead.
> - **Amazon Q Business** → closed to new customers on 30–31 July 2026. Use **[AWS Quick](../analytics/quicksight.md)** instead.

## In one sentence

Amazon Q was AWS's family of AI assistants: one helped with code and AWS questions, the other answered questions from your company's data.

## Real-life comparison

Amazon Q was like a knowledgeable colleague who had read all the AWS manuals (Q Developer) or all your company's documents (Q Business). That colleague has now been split into separate, renamed helpers.

## What problem does it solve?

Finding answers in documentation, writing repetitive code or searching internal wikis takes time. An AI assistant answers in plain English inside the tools you already use.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **AWS assistant** | The new name for the AI chat in the AWS Console (was Amazon Q Developer in the Console). |
| **Kiro** | AWS's AI coding tool (IDE and CLI) that replaces Amazon Q Developer in code editors. |
| **AWS Quick** | AWS's AI workspace for business data and dashboards; the replacement for Q Business. |
| **IDE** | Integrated Development Environment – a code editor such as VS Code. |

## How it works (step by step)

Using the **AWS assistant** in the Console:
1. Sign in to the AWS Console.
2. Open the assistant from the Console's top bar.
3. Ask a question in plain English.
4. Read the answer and check it before acting on it.

## When to use it

- **AWS assistant:** learning AWS, understanding errors, finding the right Console page.
- **Kiro:** writing and explaining code in your editor.
- **AWS Quick:** asking questions of business data.

## When NOT to use it (and what to use instead)

- **Building your own AI app.** → [Bedrock](bedrock.md).
- **New coding projects in an IDE.** Don't start with Q Developer – it no longer takes new sign-ups. → Kiro.
- **New company knowledge assistants.** Don't start with Q Business. → [AWS Quick](../analytics/quicksight.md).

## Real-world example

**Scenario:** A junior engineer doesn't understand an IAM "Access Denied" error.

**How it helps:** They ask the AWS assistant in the Console, which explains which permission is missing and where to add it.

**What it looks like:**

```
 You ──question──► AWS assistant (in the Console) ──► explanation + suggested fix
```

## Try it yourself

> ⚠️ **Cost warning:** The AWS assistant has a free tier with monthly limits. Kiro and AWS Quick have their own pricing – check before subscribing.

### Option A – Using the AWS Console (clicking in the website)

1. Sign in to the Console.
2. Open the AWS assistant from the top bar.
3. Ask: "What's the difference between a security group and a network ACL?"

### Option B – Using the AWS CLI (typing commands)

Not applicable – the Amazon Q CLI has been replaced by the Kiro CLI. See the [Kiro website](https://kiro.dev/).

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Nothing to clean up.

## How much does it cost?

The AWS assistant has a free tier. Existing Amazon Q Developer Pro subscribers keep their Pro features until end of support. Kiro and AWS Quick are charged separately.

Official info: [Amazon Q pricing](https://aws.amazon.com/q/pricing/)

## Security tips

- Never paste passwords, access keys or customer data into an AI chat.
- Check what the assistant suggests before running it – especially delete commands.

## Common mistakes

- Following older tutorials that tell you to install the Amazon Q IDE plugin or sign up for Q Business.
- Copying AI-generated code without understanding or testing it.

## Works well with

- [IAM](../security-identity-compliance/iam.md), [CloudShell](../developer-tools/cloudshell.md), [AWS Quick](../analytics/quicksight.md).

## Quick check (test yourself)

1. What is Amazon Q Developer in the Console called now?
   <details><summary>Answer</summary>The AWS assistant.</details>
2. What replaces Amazon Q Developer in code editors?
   <details><summary>Answer</summary>Kiro.</details>
3. What should new customers use instead of Q Business?
   <details><summary>Answer</summary>AWS Quick.</details>

## Learn more

- [Amazon Q Developer renamed AWS assistant (What's New)](https://aws.amazon.com/about-aws/whats-new/2026/11/q-developer-renamed-aws-assistant/)
- [Amazon Q Developer end-of-support announcement](https://aws.amazon.com/blogs/devops/amazon-q-developer-end-of-support-announcement/)
- [Amazon Q Business availability change](https://docs.aws.amazon.com/amazonq/latest/qbusiness-ug/qbusiness-availability-change.html)
