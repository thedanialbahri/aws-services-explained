# Amazon EMR

**Category:** Analytics  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

EMR runs big data frameworks like Apache Spark and Hadoop to process huge data sets across many computers.

## Real-life comparison

EMR is like hiring a whole team of temporary workers to sort a mountain of post in an evening, then sending them home.

## What problem does it solve?

Processing terabytes or petabytes needs many machines working together. EMR sets up those clusters quickly, on EC2, EKS or serverless.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Cluster** | A group of EC2 instances running the frameworks. |
| **Spark** | A popular engine for large-scale data processing. |
| **EMR Serverless** | Run Spark/Hive jobs without managing clusters. |

## How it works (step by step)

1. Create an EMR Serverless application (or a cluster).
2. Submit a job (e.g. a Spark script reading S3).
3. EMR runs it across many workers and writes results.

## When to use it

- Very large or custom data processing and machine-learning prep.

## When NOT to use it (and what to use instead)

- **Simpler ETL.** → [Glue](glue.md).
- **Ad-hoc SQL on S3.** → [Athena](athena.md).

## Real-world example

**Scenario:** A telecom firm processes billions of call records nightly.

**How it helps:** A Spark job on EMR Serverless aggregates them into usage reports.

**What it looks like:**

```
 S3 raw records ──► EMR (Spark) ──► S3 reports
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per instance-hour or vCPU/memory used by jobs. Avoid unless you need it.

### Option A – Using the AWS Console (clicking in the website)

1. Open **EMR** → **EMR Serverless** → **Get started** and review the setup.

### Option B – Using the AWS CLI (typing commands)

```bash
aws emr-serverless list-applications
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Stop and delete applications or terminate clusters.

## How much does it cost?

EMR fee plus underlying EC2/EKS or serverless vCPU and memory charges.

Official pricing: <https://aws.amazon.com/emr/pricing/>

## Security tips

- Encrypt data at rest and in transit; use least-privilege job roles.

## Common mistakes

- Leaving clusters running after jobs finish.

## Works well with

- [S3](../storage/s3.md), [Glue](glue.md).

## Quick check (test yourself)

1. Name a framework EMR runs.
   <details><summary>Answer</summary>Apache Spark (or Hadoop, Hive).</details>
2. What avoids managing clusters?
   <details><summary>Answer</summary>EMR Serverless.</details>
3. For simple ETL, what's easier?
   <details><summary>Answer</summary>AWS Glue.</details>

## Learn more

- [Amazon EMR documentation](https://docs.aws.amazon.com/emr/)
