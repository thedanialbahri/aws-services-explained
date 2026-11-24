# AWS IAM Identity Center

**Category:** Security, identity & compliance  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

IAM Identity Center gives people one login and a portal to reach all the AWS accounts and apps they're allowed to use, with short-lived credentials.

## Real-life comparison

It's like a hotel key card. You check in once at reception, and the card opens your room, the gym and the pool – but only for the length of your stay. You don't carry a separate metal key for every door.

## What problem does it solve?

Creating IAM users in every account means many passwords and long-lived access keys. Identity Center gives each person one identity (or links to your company's existing one, like Microsoft Entra ID), with temporary credentials that expire automatically.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Identity source** | Where users live: Identity Center's own directory, Active Directory, or an external provider. |
| **Permission set** | A template of permissions, e.g. "ReadOnly" or "Developer". |
| **Assignment** | Giving a user or group a permission set in a specific account. |
| **AWS access portal** | The web page where users sign in and pick an account. |
| **SSO** (single sign-on) | One login that works for many systems. |

## How it works (step by step)

1. You enable Identity Center (ideally in your [Organizations](organizations.md) management account).
2. You choose an identity source.
3. You create users and groups.
4. You create permission sets.
5. You assign groups + permission sets to accounts.
6. Users sign in to the access portal and get temporary credentials for the Console or CLI (`aws configure sso`).

## When to use it

- Logins for all humans using AWS – even in a single learning account.
- Companies with many AWS accounts.

## When NOT to use it (and what to use instead)

- **Permissions for programs running in AWS.** → [IAM roles](iam.md).
- **Your app's customers.** → [Cognito](cognito.md).

## Real-world example

**Scenario:** A charity has three AWS accounts (dev, test, live) and six staff.

**The problem:** Each person had an IAM user in each account – 18 passwords.

**How it helps:** Staff sign in once with their Microsoft 365 login. Developers get full access to dev and read-only to live.

**What it looks like:**

```
 Staff ──► Access portal ──► dev account (Developer)
                         └─► live account (ReadOnly)
```

## Try it yourself

> ⚠️ **Cost warning:** Identity Center is free.

### Option A – Using the AWS Console (clicking in the website)

Follow **Step 4** of [START-HERE.md](../../START-HERE.md#step-4--dont-use-the-root-user-day-to-day) – it walks through this exactly.

### Option B – Using the AWS CLI (typing commands)

```bash
# Set up a CLI profile that signs in through Identity Center
aws configure sso

# Sign in again later (opens your browser)
aws sso login --profile my-profile
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_ssoadmin_permission_set` and related resources, but best done by hand the first time.

### Clean up (delete what you made)

Keep it – this is how you should sign in. To remove a test user, open **Users** → tick it → **Delete users**.

## How much does it cost?

Free.

Official info: <https://aws.amazon.com/iam/identity-center/>

## Security tips

- Turn on MFA for all users.
- Use groups, not individual assignments.
- Keep session lengths short for powerful permission sets.

## Common mistakes

- Still creating IAM users for people out of habit.

## Works well with

- [Organizations](organizations.md), [IAM](iam.md), [Control Tower](../management-governance/control-tower.md).

## Quick check (test yourself)

1. What is a permission set?
   <details><summary>Answer</summary>A reusable template of permissions assigned to users in accounts.</details>
2. Are the credentials long-lived?
   <details><summary>Answer</summary>No, they're temporary and expire.</details>
3. Which CLI command sets up an SSO profile?
   <details><summary>Answer</summary>aws configure sso</details>

## Learn more

- [IAM Identity Center User Guide](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html)
