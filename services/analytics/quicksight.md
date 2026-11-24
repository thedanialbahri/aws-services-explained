# AWS Quick Sight (formerly Amazon QuickSight)

**Category:** Analytics  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ℹ️ **Name change:** Amazon QuickSight became part of **Amazon Quick Suite** in October 2025, then **Amazon Quick**. On 9 November 2026 it was renamed again to **AWS Quick**, and its dashboard feature is now **AWS Quick Sight**. Existing dashboards, datasets and prices didn't change. You'll still see "QuickSight" in older tutorials, API names and web addresses.

## In one sentence

Quick Sight creates interactive dashboards and charts from your data, which you can share with people across your organisation.

## Real-life comparison

It's like turning a messy spreadsheet into a clear car-style dashboard with gauges and graphs that update themselves.

## What problem does it solve?

Business people need to see trends without writing SQL. Quick Sight connects to data and makes visuals. The wider AWS Quick workspace adds AI chat, research and automation on top.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **AWS Quick** | AWS's AI workspace for business data (the whole product). |
| **Quick Sight** | The dashboards and charts part of AWS Quick (the old QuickSight). |
| **Data source** | Where data comes from (S3, Athena, Redshift, RDS, Excel). |
| **Dataset** | Prepared data ready for charts. |
| **Analysis** | Where you build charts. |
| **Dashboard** | A published, read-only view to share. |
| **SPICE** | Quick Sight's fast in-memory data store. |

## How it works (step by step)

1. Sign up for AWS Quick.
2. Connect a data source and create a dataset.
3. Build charts in an analysis.
4. Publish as a dashboard and share it.

## When to use it

- Business dashboards on AWS data.
- Replacing Amazon Q Business for new projects (AWS Quick is its recommended successor).

## When NOT to use it (and what to use instead)

- **Monitoring AWS resources.** → [CloudWatch](../management-governance/cloudwatch.md) dashboards.

## Real-world example

**Scenario:** A café chain wants daily sales by branch.

**How it helps:** Till data in Athena feeds a Quick Sight dashboard that managers check each morning.

**What it looks like:**

```
 Athena / Redshift ──► Quick Sight dataset ──► dashboard ──► managers
```

## Try it yourself

> ⚠️ **Cost warning:** AWS Quick has per-user plans (and a monthly account fee on some organisation plans). **Cancel the subscription after testing** – it isn't removed automatically. Check the pricing page first.

### Option A – Using the AWS Console (clicking in the website)

1. Search for **Quick** in the Console and sign up (check the plan and trial terms).
2. Upload a small CSV as a dataset.
3. Create an analysis and add a bar chart.

### Option B – Using the AWS CLI (typing commands)

```bash
# The CLI still uses the old "quicksight" name (replace the account ID)
aws quicksight list-dashboards --aws-account-id 123456789012
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete the analysis and dataset, then unsubscribe from AWS Quick in its account settings.

## How much does it cost?

Per user per month, by plan, plus extras such as SPICE capacity and AI features. Some organisation plans also have a monthly account fee.

Official pricing: <https://aws.amazon.com/quick/pricing/>

## Security tips

- Use row-level security so each manager sees only their own branch.

## Common mistakes

- Forgetting to cancel after testing.
- Searching only for "QuickSight" and missing newer docs under "Quick".

## Works well with

- [Athena](athena.md), [Redshift](../databases/redshift.md), [S3](../storage/s3.md).

## Quick check (test yourself)

1. What is Amazon QuickSight called now?
   <details><summary>Answer</summary>AWS Quick Sight, part of AWS Quick.</details>
2. What is SPICE?
   <details><summary>Answer</summary>Quick Sight's in-memory data engine.</details>
3. What's the difference between an analysis and a dashboard?
   <details><summary>Answer</summary>You build in an analysis; a dashboard is the published, read-only view.</details>

## Learn more

- [AWS Quick user guide](https://docs.aws.amazon.com/quick/latest/userguide/what-is.html)
- [QuickSight evolves to Quick Suite (AWS blog, October 2025)](https://aws.amazon.com/blogs/business-intelligence/reimagine-business-intelligence-amazon-quicksight-evolves-to-amazon-quick-suite/)
