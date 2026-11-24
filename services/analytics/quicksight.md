# Amazon QuickSight

**Category:** Analytics  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check) <!-- TODO: verify how QuickSight is packaged within Amazon Quick Suite -->

## In one sentence

QuickSight creates interactive dashboards and charts from your data, which you can share with people across your organisation.

## Real-life comparison

It's like turning a messy spreadsheet into a clear car-style dashboard with gauges and graphs that update themselves.

## What problem does it solve?

Business people need to see trends without writing SQL. QuickSight connects to data and makes visuals, with AI features to ask questions in plain English.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Data source** | Where data comes from (S3, Athena, Redshift, RDS, Excel). |
| **Dataset** | Prepared data ready for charts. |
| **Analysis** | Where you build charts. |
| **Dashboard** | A published, read-only view to share. |
| **SPICE** | QuickSight's fast in-memory data store. |

## How it works (step by step)

1. Sign up for QuickSight.
2. Connect a data source and create a dataset.
3. Build charts in an analysis.
4. Publish as a dashboard and share it.

## When to use it

- Business dashboards on AWS data.

## When NOT to use it (and what to use instead)

- **Monitoring AWS resources.** → [CloudWatch](../management-governance/cloudwatch.md) dashboards.

## Real-world example

**Scenario:** A café chain wants daily sales by branch.

**How it helps:** Till data in Athena feeds a QuickSight dashboard managers check each morning.

**What it looks like:**

```
 Athena / Redshift ──► QuickSight dataset ──► dashboard ──► managers
```

## Try it yourself

> ⚠️ **Cost warning:** QuickSight has per-user subscriptions and may have a free trial. **Cancel the subscription after testing** – it isn't removed automatically.

### Option A – Using the AWS Console (clicking in the website)

1. Search for **QuickSight** and sign up (check the trial terms).
2. Upload a small CSV as a dataset.
3. Create an analysis and add a bar chart.

### Option B – Using the AWS CLI (typing commands)

```bash
# List dashboards (replace account ID)
aws quicksight list-dashboards --aws-account-id 123456789012
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete the analysis and dataset, then **Manage QuickSight** → **Account settings** → **Delete account/unsubscribe**.

## How much does it cost?

Per user per month (authors cost more than readers), plus SPICE capacity and some AI features.

Official pricing: <https://aws.amazon.com/quicksight/pricing/>

## Security tips

- Use row-level security so each manager sees only their branch.

## Common mistakes

- Forgetting to cancel after the trial.

## Works well with

- [Athena](athena.md), [Redshift](../databases/redshift.md), [S3](../storage/s3.md).

## Quick check (test yourself)

1. What is SPICE?
   <details><summary>Answer</summary>QuickSight's in-memory data engine.</details>
2. What's the difference between an analysis and a dashboard?
   <details><summary>Answer</summary>You build in an analysis; a dashboard is the published read-only view.</details>
3. How is it charged?
   <details><summary>Answer</summary>Mainly per user per month.</details>

## Learn more

- [Amazon QuickSight User Guide](https://docs.aws.amazon.com/quicksight/latest/user/welcome.html)
