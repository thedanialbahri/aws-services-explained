# Amazon Aurora

**Category:** Databases  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Aurora is AWS's own relational database, compatible with MySQL and PostgreSQL, built for higher performance and resilience than standard databases.

## Real-life comparison

If RDS MySQL is a reliable family car, Aurora is the same car with an upgraded engine and a chassis designed by the manufacturer – you drive it the same way, but it goes faster and copes better with crashes.

## What problem does it solve?

Standard databases store data on one server's disks. Aurora separates compute from a shared storage layer that keeps six copies across three AZs, so it recovers faster and scales reads easily.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Cluster** | The Aurora database: one writer plus optional readers sharing storage. |
| **Writer instance** | Handles writes (and reads). |
| **Aurora Replica** | A reader instance; can be promoted if the writer fails. |
| **Aurora Serverless v2** | Capacity scales up and down automatically with demand. |
| **Global Database** | Copies the cluster to other Regions. |

## How it works (step by step)

1. You create an Aurora cluster (MySQL- or PostgreSQL-compatible).
2. Aurora creates shared storage across three AZs.
3. You add a writer and, optionally, readers.
4. Your app uses the **cluster endpoint** for writes and the **reader endpoint** for reads.
5. If the writer fails, a reader takes over, usually within about a minute.

## When to use it

- Busy production apps needing MySQL or PostgreSQL.
- Unpredictable workloads (Serverless v2).

## When NOT to use it (and what to use instead)

- **Small or test databases.** → [RDS](rds.md) is often cheaper.
- **Engines like SQL Server or Oracle.** → [RDS](rds.md).

## Real-world example

**Scenario:** A ticketing platform's PostgreSQL database struggles when popular events go on sale.

**How it helps:** They move to Aurora PostgreSQL with two readers. Ticket searches go to readers; purchases go to the writer.

**What it looks like:**

```
 App ──writes──► Writer ─┐
 App ──reads───► Reader ─┼── shared storage (6 copies, 3 AZs)
                 Reader ─┘
```

## Try it yourself

> ⚠️ **Cost warning:** Aurora isn't in the standard Free Tier. Serverless v2 can scale down to a small minimum (check current settings). Delete the cluster within an hour of testing.

### Option A – Using the AWS Console (clicking in the website)

1. **RDS** → **Create database** → **Aurora (PostgreSQL Compatible)**.
2. Choose **Dev/Test**, **Serverless v2**, with the lowest capacity range.
3. Public access **No**. Create it and look at the writer and reader endpoints.

### Option B – Using the AWS CLI (typing commands)

```bash
# List Aurora clusters and their endpoints
aws rds describe-db-clusters --query 'DBClusters[].[DBClusterIdentifier,Endpoint,ReaderEndpoint]'
```

### Option C – Using Terraform (infrastructure as code)

Uses `aws_rds_cluster` plus `aws_rds_cluster_instance`. Try the Console first.

### Clean up (delete what you made)

1. Delete each instance in the cluster, then the cluster itself (skip final snapshot for test data).

## How much does it cost?

Per instance-hour (or per ACU-hour for Serverless), plus storage per GB-month and I/O (or the I/O-Optimized option), plus backups beyond the free amount.

Official pricing: <https://aws.amazon.com/rds/aurora/pricing/>

## Security tips

- Same as RDS: private subnets, encryption, Secrets Manager.

## Common mistakes

- Leaving test clusters running.

## Works well with

- [RDS](rds.md), [Lambda](../compute/lambda.md), [Secrets Manager](../security-identity-compliance/secrets-manager.md).

## Quick check (test yourself)

1. How many copies of data does Aurora storage keep?
   <details><summary>Answer</summary>Six, across three AZs.</details>
2. Which endpoint should reads use?
   <details><summary>Answer</summary>The reader endpoint.</details>
3. Which engines is Aurora compatible with?
   <details><summary>Answer</summary>MySQL and PostgreSQL.</details>

## Learn more

- [Amazon Aurora User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html)
- [Amazon Aurora pricing](https://aws.amazon.com/rds/aurora/pricing/)
