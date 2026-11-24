# AWS Control Tower

**Category:** Management & governance  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Control Tower sets up a well-organised, secure multi-account AWS environment (a "landing zone") for you, with guardrails already in place.

## Real-life comparison

It's like buying a new-build housing estate with roads, street lights and rules already in place, instead of building each house and road yourself.

## What problem does it solve?

Setting up Organizations, logging accounts, security accounts, Identity Center and rules by hand takes weeks. Control Tower does it in about an hour following AWS best practices.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Landing zone** | A ready-made multi-account setup. |
| **Controls (guardrails)** | Rules – preventive (block) or detective (report). |
| **Account Factory** | A way to create new accounts with the standard setup. |
| **Log archive / Audit accounts** | Special accounts for central logs and security. |

## How it works (step by step)

1. Run Control Tower setup from your management account.
2. It creates Organizations OUs, log and audit accounts, CloudTrail and Config.
3. You turn on controls.
4. You create new accounts through Account Factory.

## When to use it

- Organisations starting or tidying up a multi-account setup.

## When NOT to use it (and what to use instead)

- **A single personal learning account.** Overkill.

## Real-world example

**Scenario:** A growing start-up is about to go from 2 to 15 accounts.

**How it helps:** Control Tower creates the structure, central logging and guardrails, and every new account starts secure.

**What it looks like:**

```
 Management account
   ├── Security OU: Log Archive, Audit
   └── Workloads OU: dev, test, prod (created via Account Factory)
```

## Try it yourself

> ⚠️ **Cost warning:** Control Tower is free, but it switches on CloudTrail, Config and other services across accounts, which cost money. Not recommended in a personal account.

### Option A – Using the AWS Console (clicking in the website)

Read through the **Control Tower** landing page only.

### Option B – Using the AWS CLI (typing commands)

```bash
aws controltower list-landing-zones
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning (see AWS's "Account Factory for Terraform" for real projects).

### Clean up (delete what you made)

Decommissioning a landing zone is a multi-step process – see the docs.

## How much does it cost?

No charge for Control Tower itself; you pay for the services it enables.

Official pricing: <https://aws.amazon.com/controltower/pricing/>

## Security tips

- Don't disable the mandatory controls.

## Common mistakes

- Setting it up in an account that already has a messy Organizations structure without planning.

## Works well with

- [Organizations](../security-identity-compliance/organizations.md), [IAM Identity Center](../security-identity-compliance/iam-identity-center.md), [Config](config.md).

## Quick check (test yourself)

1. What is a landing zone?
   <details><summary>Answer</summary>A ready-made, secure multi-account AWS setup.</details>
2. What creates new accounts with the standard setup?
   <details><summary>Answer</summary>Account Factory.</details>
3. Is it useful for one personal account?
   <details><summary>Answer</summary>Not really.</details>

## Learn more

- [AWS Control Tower User Guide](https://docs.aws.amazon.com/controltower/latest/userguide/what-is-control-tower.html)
