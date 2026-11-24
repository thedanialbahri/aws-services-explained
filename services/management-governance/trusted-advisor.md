# AWS Trusted Advisor

**Category:** Management & governance  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Trusted Advisor checks your AWS account against best practices and suggests ways to save money, improve security and avoid problems.

## Real-life comparison

It's like a home energy and safety inspection. The inspector walks round and gives you a list: "this window doesn't lock", "you're paying for a room you never use", "your smoke alarm battery is low".

## What problem does it solve?

It's easy to miss things like an open security group or idle servers. Trusted Advisor finds them for you.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Check** | One automated test. |
| **Categories** | Cost optimisation, performance, security, fault tolerance, service limits, operational excellence. |
| **Support plan** | Basic/Developer plans get a small set of checks; Business and higher get all of them. |

## How it works (step by step)

1. Open Trusted Advisor.
2. It runs checks against your account.
3. Each check shows green, yellow (investigate) or red (action needed).
4. You fix the problems it lists.

## When to use it

- Regular account health checks.

## When NOT to use it (and what to use instead)

- **Detailed security checks across standards.** → [Security Hub](../security-identity-compliance/security-hub.md).
- **Detailed cost analysis.** → [Cost Explorer](../cost-management/cost-explorer.md).

## Real-world example

**Scenario:** Lucy inherits an AWS account from a previous contractor.

**How it helps:** Trusted Advisor flags root without MFA, a public S3 bucket and security groups open to the world. She fixes them on day one.

**What it looks like:**

```
 Your account ──checks──► Trusted Advisor ──► 🔴 fix / 🟡 investigate / 🟢 OK
```

## Try it yourself

> ⚠️ **Cost warning:** Free with any support plan (more checks need a paid plan).

### Option A – Using the AWS Console (clicking in the website)

1. Search for **Trusted Advisor** and open it.
2. Click **Security** and read each check.
3. Click **Refresh all checks**.

### Option B – Using the AWS CLI (typing commands)

The Trusted Advisor API needs a Business support plan or higher, so use the Console.

### Option C – Using Terraform (infrastructure as code)

Not applicable – there's nothing to build.

### Clean up (delete what you made)

Nothing to clean up.

## How much does it cost?

Free core checks; full checks come with Business, Enterprise On-Ramp or Enterprise support.

Official info: <https://aws.amazon.com/premiumsupport/technology/trusted-advisor/>

## Security tips

- Fix red security checks first.

## Common mistakes

- Never looking at it after the first visit.

## Works well with

- [Security Hub](../security-identity-compliance/security-hub.md), [Cost Explorer](../cost-management/cost-explorer.md).

## Quick check (test yourself)

1. Name two Trusted Advisor categories.
   <details><summary>Answer</summary>For example: cost optimisation and security.</details>
2. Do all support plans get every check?
   <details><summary>Answer</summary>No, full checks need Business support or higher.</details>
3. What does a red result mean?
   <details><summary>Answer</summary>Action is recommended.</details>

## Learn more

- [Trusted Advisor documentation](https://docs.aws.amazon.com/awssupport/latest/user/trusted-advisor.html)
