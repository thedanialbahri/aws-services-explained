# AWS Billing and Cost Management (Billing)

**Category:** Cost management  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

The Billing and Cost Management console shows your AWS bills, payments, credits and Free Tier usage in one place.

## Real-life comparison

It's your online bank statement for AWS: every charge, when you paid, and any money-off vouchers.

## What problem does it solve?

You need to see what you owe, why, and how close you are to Free Tier limits. This console is the home for all money-related AWS tools.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Bill** | Monthly charges by service and Region. |
| **Free Tier usage** | How much of your free allowance you've used. |
| **Credits** | Vouchers that reduce your bill. |
| **Cost allocation tags** | Tags you switch on so bills can be split by project. |

## How it works (step by step)

1. AWS measures your usage all month.
2. Charges appear on the **Bills** page, updated through the month.
3. At month end, the bill is finalised and charged to your payment method.

## When to use it

- Checking charges and Free Tier usage, downloading invoices.

## When NOT to use it (and what to use instead)

- **Getting alerts.** → [Budgets](budgets.md).
- **Analysing trends.** → [Cost Explorer](cost-explorer.md).

## Real-world example

**Scenario:** Jade gets an unexpected bill for a few pounds.

**How it helps:** The **Bills** page shows it's from a NAT gateway left running in a test VPC. She deletes it.

**What it looks like:**

```
 Bills page ──► EC2 - Other ──► NAT Gateway hours (eu-west-2)
```

## Try it yourself

> ⚠️ **Cost warning:** Viewing billing is free.

### Option A – Using the AWS Console (clicking in the website)

1. Click your account name (top right) → **Billing and Cost Management**.
2. Open **Bills** and expand a service to see charges.
3. Open **Free Tier** to see usage against limits.
4. Open **Billing preferences** and turn on **Free Tier usage alerts**.

### Option B – Using the AWS CLI (typing commands)

```bash
# This month's total so far (Cost Explorer API, in us-east-1)
aws ce get-cost-and-usage --region us-east-1 \
  --time-period Start=$(date +%Y-%m-01),End=$(date +%Y-%m-%d) \
  --granularity MONTHLY --metrics UnblendedCost
```
(Doesn't work on the first day of the month, when Start and End are the same.)

### Option C – Using Terraform (infrastructure as code)

Not applicable – nothing to build.

### Clean up (delete what you made)

Nothing to clean up.

## How much does it cost?

Free.

## Security tips

- Give billing access only to people who need it.

## Common mistakes

- Never looking at the bill until it's big.

## Works well with

- [Budgets](budgets.md), [Cost Explorer](cost-explorer.md).

## Quick check (test yourself)

1. Where do you see Free Tier usage?
   <details><summary>Answer</summary>Billing and Cost Management → Free Tier.</details>
2. Is viewing billing free?
   <details><summary>Answer</summary>Yes.</details>
3. Which tool sends spending alerts?
   <details><summary>Answer</summary>AWS Budgets.</details>

## Learn more

- [AWS Billing User Guide](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-what-is.html)
