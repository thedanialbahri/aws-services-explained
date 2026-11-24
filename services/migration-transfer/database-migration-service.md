# AWS Database Migration Service (DMS)

**Category:** Migration & transfer  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

DMS moves data from one database to another – for example from an office SQL Server into Amazon RDS – while the source keeps running.

## Real-life comparison

It's like moving a shop's stock to a new building while the old shop stays open, with a van ferrying new deliveries across until the final day.

## What problem does it solve?

Copying a live database means downtime and risk. DMS does a full copy, then keeps it in sync until you switch.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Source / target endpoint** | Where data comes from / goes to. |
| **Replication instance** | The server that does the copying (or DMS Serverless). |
| **Full load + CDC** | Copy everything, then copy ongoing changes (change data capture). |
| **Schema Conversion** | Converts table structures between different database engines. |

## How it works (step by step)

1. Create source and target endpoints.
2. Create a replication instance (or serverless config).
3. Start a task: full load, then CDC.
4. Switch the app to the target when ready.

## When to use it

- Moving databases into RDS, Aurora, DynamoDB, Redshift, S3.

## When NOT to use it (and what to use instead)

- **Whole servers.** → [Application Migration Service](application-migration-service.md).

## Real-world example

**Scenario:** A shop's MySQL database moves to Aurora.

**How it helps:** DMS copies it and keeps it in sync; cutover takes minutes.

**What it looks like:**

```
 On-prem MySQL ──full load + CDC──► DMS ──► Aurora MySQL
```

## Try it yourself

> ⚠️ **Cost warning:** Replication instances are charged per hour (some free hours for new accounts); serverless per capacity unit. Delete after testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Database Migration Service** and review **Endpoints** and **Database migration tasks**.

### Option B – Using the AWS CLI (typing commands)

```bash
aws dms describe-replication-tasks
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete tasks, endpoints and replication instances.

## How much does it cost?

Per replication instance-hour or DMS capacity unit, plus storage and data transfer.

Official pricing: <https://aws.amazon.com/dms/pricing/>

## Security tips

- Use SSL for endpoints and Secrets Manager for credentials.

## Common mistakes

- Not testing the converted schema before cutover.

## Works well with

- [RDS](../databases/rds.md), [Aurora](../databases/aurora.md).

## Quick check (test yourself)

1. What is CDC?
   <details><summary>Answer</summary>Change data capture – copying ongoing changes.</details>
2. Can the source keep running during migration?
   <details><summary>Answer</summary>Yes.</details>
3. What converts schemas between engines?
   <details><summary>Answer</summary>DMS Schema Conversion.</details>

## Learn more

- [AWS DMS User Guide](https://docs.aws.amazon.com/dms/latest/userguide/Welcome.html)
