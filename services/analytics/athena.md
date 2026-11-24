# Amazon Athena

**Category:** Analytics  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Athena lets you run SQL queries straight on files stored in S3, with no servers or database to set up.

## Real-life comparison

Athena is like being able to search inside every box in your storage unit without unpacking them – just ask the question and get the answer.

## What problem does it solve?

Loading log files or CSVs into a database before you can query them takes time. Athena queries them where they sit and charges only for the data scanned.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **SQL** | The standard language for asking databases questions. |
| **Table** | A description of how files in S3 are laid out (stored in the Glue Data Catalog). |
| **Partition** | Splitting data into folders (e.g. by date) so queries read less. |
| **Parquet** | A compressed, column-based file format that makes queries cheaper. |

## How it works (step by step)

1. Put data files in S3.
2. Create a table describing them (by hand or with a [Glue](glue.md) crawler).
3. Write SQL in the Athena editor.
4. Athena reads the files, returns results and saves them to an S3 results bucket.

## When to use it

- Ad-hoc questions on logs (CloudTrail, ALB, VPC Flow Logs) and data lakes.

## When NOT to use it (and what to use instead)

- **Fast, frequent dashboard queries on huge data.** → [Redshift](../databases/redshift.md).
- **App databases.** → [RDS](../databases/rds.md) / [DynamoDB](../databases/dynamodb.md).

## Real-world example

**Scenario:** A security engineer must find every console login from outside the UK last month.

**How it helps:** CloudTrail logs are already in S3; one Athena query finds them.

**What it looks like:**

```
 S3 (CloudTrail logs) ──► Athena: SELECT ... WHERE eventname='ConsoleLogin' ──► results
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per TB of data scanned (with a minimum per query). Small test files cost almost nothing. Delete the results bucket at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Upload a small CSV (e.g. `name,age` rows) to `s3://my-example-bucket-12345/people/`.
2. Open **Athena** → set a query result location (another S3 folder) in **Settings**.
3. Run:
```sql
CREATE EXTERNAL TABLE people (name string, age int)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
LOCATION 's3://my-example-bucket-12345/people/'
TBLPROPERTIES ('skip.header.line.count'='1');
```
4. Then run `SELECT * FROM people WHERE age > 30;`

### Option B – Using the AWS CLI (typing commands)

```bash
aws athena start-query-execution --query-string "SELECT * FROM people LIMIT 10" \
  --result-configuration OutputLocation=s3://my-example-bucket-12345/athena-results/
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_athena_workgroup` and `aws_glue_catalog_table`.

### Clean up (delete what you made)

1. Run `DROP TABLE people;`
2. Delete the test files and results from S3.

## How much does it cost?

Per TB scanned. Using Parquet and partitions can cut costs a lot.

Official pricing: <https://aws.amazon.com/athena/pricing/>

## Security tips

- Encrypt the results bucket; control access with IAM and Lake Formation.

## Common mistakes

- `SELECT *` on huge uncompressed data – expensive.

## Works well with

- [S3](../storage/s3.md), [Glue](glue.md), [QuickSight](quicksight.md).

## Quick check (test yourself)

1. Where does Athena's data live?
   <details><summary>Answer</summary>In S3.</details>
2. How is Athena charged?
   <details><summary>Answer</summary>By the amount of data scanned.</details>
3. How can you make queries cheaper?
   <details><summary>Answer</summary>Use Parquet, compression and partitions.</details>

## Learn more

- [Amazon Athena User Guide](https://docs.aws.amazon.com/athena/latest/ug/what-is.html)
- [Athena pricing](https://aws.amazon.com/athena/pricing/)
