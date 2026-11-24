# Amazon Redshift

**Category:** Databases  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Redshift is a data warehouse – a database built to run big analysis queries over huge amounts of data quickly.

## Real-life comparison

A normal database is like a shop till: fast at handling one sale at a time. A data warehouse is like the head office's accounts department: slower to record single sales, but brilliant at answering "what were total sales by region for the last five years?"

## What problem does it solve?

Running big reports on your live database slows down your app. Redshift copies data into a system designed for analysis, storing it by column so it can scan billions of rows fast.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Data warehouse** | A database designed for reports and analysis. |
| **Columnar storage** | Data stored by column, which makes totals and averages fast. |
| **Redshift Serverless** | Redshift that sizes itself; you pay for use. |
| **Provisioned cluster** | Redshift on nodes you choose and pay for by the hour. |
| **Redshift Spectrum** | Query files in S3 without loading them. |

## How it works (step by step)

1. Create a Serverless workgroup or a provisioned cluster.
2. Load data from S3, databases or streams (or use zero-ETL integrations).
3. Run SQL queries in the Query Editor or BI tools like [QuickSight](../analytics/quicksight.md).

## When to use it

- Business reports and dashboards over large data sets.

## When NOT to use it (and what to use instead)

- **The database behind an app.** → [RDS](rds.md) / [DynamoDB](dynamodb.md).
- **Occasional queries on files in S3.** → [Athena](../analytics/athena.md) may be cheaper.

## Real-world example

**Scenario:** A supermarket chain wants weekly sales trends from 3 years of till data.

**How it helps:** Till data lands in S3 nightly and loads into Redshift. Analysts run reports in seconds and share dashboards in QuickSight.

**What it looks like:**

```
 Tills ──► S3 ──load──► Redshift ──► QuickSight dashboards
```

## Try it yourself

> ⚠️ **Cost warning:** New accounts may get Redshift Serverless trial credits. Otherwise it's charged per RPU-hour while queries run, plus storage. Delete the workgroup and namespace at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Redshift** → **Try Redshift Serverless free** (or **Create workgroup**).
2. Use default settings and create.
3. Open **Query editor v2**, connect, and run the sample `tickit` queries.

### Option B – Using the AWS CLI (typing commands)

```bash
aws redshift-serverless list-workgroups
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_redshiftserverless_namespace` and `aws_redshiftserverless_workgroup`; try the Console first.

### Clean up (delete what you made)

1. Delete the **workgroup**, then the **namespace**.

## How much does it cost?

Serverless: per RPU-hour used plus storage. Provisioned: per node-hour plus managed storage.

Official pricing: <https://aws.amazon.com/redshift/pricing/>

## Security tips

- Keep it private; encrypt it; control access with IAM and database roles.

## Common mistakes

- Using it like an app database with many tiny updates.

## Works well with

- [S3](../storage/s3.md), [QuickSight](../analytics/quicksight.md), [Glue](../analytics/glue.md).

## Quick check (test yourself)

1. What is a data warehouse for?
   <details><summary>Answer</summary>Analysis and reporting over large amounts of data.</details>
2. Why is columnar storage fast for reports?
   <details><summary>Answer</summary>Queries only read the columns they need.</details>
3. What could you use for occasional queries on S3 files?
   <details><summary>Answer</summary>Amazon Athena.</details>

## Learn more

- [Amazon Redshift documentation](https://docs.aws.amazon.com/redshift/)
- [Amazon Redshift pricing](https://aws.amazon.com/redshift/pricing/)
