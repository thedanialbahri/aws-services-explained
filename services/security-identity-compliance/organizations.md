# AWS Organizations

**Category:** Security, identity & compliance  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Organizations lets you group many AWS accounts, pay for them with one bill, and set rules that apply to all of them.

## Real-life comparison

It's like a company with several branches. Head office pays all the bills and sets company-wide rules ("no branch may sell alcohol"), while each branch runs its own shop.

## What problem does it solve?

Good practice is to use separate accounts for different teams and environments. Without Organizations, each account has its own bill and nobody can set rules across them.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Management account** | The account that creates and pays for the organisation. |
| **Member account** | Any other account in it. |
| **OU** (organisational unit) | A folder of accounts, e.g. "Production". |
| **SCP** (service control policy) | A rule setting the maximum permissions for accounts in an OU. |
| **Consolidated billing** | One bill for all accounts, with combined discounts. |

## How it works (step by step)

1. You create an organisation from one account (it becomes the management account).
2. You create new accounts or invite existing ones.
3. You arrange them into OUs.
4. You attach SCPs, e.g. "deny leaving the London and Ireland Regions".
5. All usage appears on one bill.

## When to use it

- As soon as you have more than one account.
- Setting guardrails for teams.

## When NOT to use it (and what to use instead)

- **Setting up many accounts with best practices automatically.** → [Control Tower](../management-governance/control-tower.md) (built on Organizations).

## Real-world example

**Scenario:** A software company has separate accounts for dev, test and live.

**The problem:** Three bills, and a developer accidentally launched servers in Brazil.

**How it helps:** One bill, and an SCP on the Dev OU that only allows UK and Ireland Regions.

**What it looks like:**

```
 Management account (billing)
   ├── OU: Production ── live account
   └── OU: Development (SCP: UK/IE Regions only) ── dev account, test account
```

## Try it yourself

> ⚠️ **Cost warning:** Organizations is free. New member accounts are only charged for what they use.

### Option A – Using the AWS Console (clicking in the website)

1. Open **AWS Organizations** → **Create an organization**.
2. Look at the **AWS accounts** tree. Create an OU called `Sandbox`.
3. Under **Policies**, enable **Service control policies** to see how they work (you don't have to attach one).

### Option B – Using the AWS CLI (typing commands)

```bash
# Show the organisation and list its accounts
aws organizations describe-organization
aws organizations list-accounts --query 'Accounts[].[Name,Id,Status]' --output table
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# Turn on Organizations with all features (needed for SCPs)
resource "aws_organizations_organization" "org" {
  feature_set          = "ALL"
  enabled_policy_types = ["SERVICE_CONTROL_POLICY"]
}
```

### Clean up (delete what you made)

1. Delete any OUs you created (they must be empty).
2. If you want to remove the organisation: remove member accounts, then **Settings** → **Delete organization**.

## How much does it cost?

Free.

Official info: <https://aws.amazon.com/organizations/pricing/>

## Security tips

- Don't run workloads in the management account.
- SCPs don't affect the management account – protect it with MFA and few users.

## Common mistakes

- Thinking an SCP *grants* permissions – it only sets the maximum. IAM must still allow the action.

## Works well with

- [IAM Identity Center](iam-identity-center.md), [Control Tower](../management-governance/control-tower.md), [AWS Budgets](../cost-management/budgets.md).

## Quick check (test yourself)

1. Do SCPs grant permissions?
   <details><summary>Answer</summary>No. They limit the maximum permissions.</details>
2. What is an OU?
   <details><summary>Answer</summary>A folder that groups accounts.</details>
3. What is consolidated billing?
   <details><summary>Answer</summary>One bill for all accounts in the organisation.</details>

## Learn more

- [AWS Organizations User Guide](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html)
