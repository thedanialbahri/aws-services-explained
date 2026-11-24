# AWS Glue

**Category:** Analytics  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Glue discovers your data, keeps a catalogue of what it looks like, and runs jobs to clean and move it between stores.

## Real-life comparison

Glue is like a library's cataloguing team plus its repair shop: they label every book so you can find it, and fix up damaged ones before they go on the shelf.

## What problem does it solve?

Data arrives messy and spread out. Before analysis, it must be found, described and transformed (**ETL** – extract, transform, load). Glue does this serverlessly.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Data Catalog** | The list of tables and their columns. |
| **Crawler** | Scans data and fills in the catalogue. |
| **ETL job** | A job (often Spark) that transforms data. |
| **Glue Studio** | A visual editor for jobs. |

## How it works (step by step)

1. Run a **crawler** on an S3 folder.
2. It creates **tables** in the Data Catalog.
3. Athena, EMR and Redshift can now query them.
4. Build **ETL jobs** to clean and convert data (e.g. CSV → Parquet).

## When to use it

- Preparing data for analytics; cataloguing a data lake.

## When NOT to use it (and what to use instead)

- **Huge custom Spark clusters you tune yourself.** → [EMR](emr.md).

## Real-world example

**Scenario:** Daily CSV exports land in S3.

**How it helps:** A crawler catalogues them; a nightly job converts them to Parquet so Athena queries are cheaper.

**What it looks like:**

```
 S3 raw CSV ──crawler──► Data Catalog ──ETL job──► S3 Parquet ──► Athena
```

## Try it yourself

> ⚠️ **Cost warning:** Crawlers and jobs are charged per DPU-hour (with minimums). The Data Catalog has a free tier.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Glue** → **Crawlers** → **Create crawler**.
2. Point it at your S3 test folder, create a database `demo`, and run it.
3. Check **Tables** – then query it in [Athena](athena.md).

### Option B – Using the AWS CLI (typing commands)

```bash
aws glue get-tables --database-name demo
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_glue_catalog_database` and `aws_glue_crawler`.

### Clean up (delete what you made)

Delete the crawler, tables and database, and the crawler's IAM role.

## How much does it cost?

Jobs and crawlers per DPU-hour; Data Catalog storage and requests above free amounts.

Official pricing: <https://aws.amazon.com/glue/pricing/>

## Security tips

- Give crawlers read access only to the buckets they scan.

## Common mistakes

- Running crawlers far more often than data changes.

## Works well with

- [Athena](athena.md), [S3](../storage/s3.md), [Lake Formation](lake-formation.md).

## Quick check (test yourself)

1. What does a crawler do?
   <details><summary>Answer</summary>Scans data and creates tables in the Data Catalog.</details>
2. What does ETL stand for?
   <details><summary>Answer</summary>Extract, transform, load.</details>
3. Why convert CSV to Parquet?
   <details><summary>Answer</summary>Faster, cheaper queries.</details>

## Learn more

- [AWS Glue User Guide](https://docs.aws.amazon.com/glue/latest/dg/what-is-glue.html)
