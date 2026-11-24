# Amazon DocumentDB (with MongoDB compatibility)

**Category:** Databases  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

DocumentDB is a managed document database that works with many MongoDB tools and drivers.

## Real-life comparison

A document database is like a filing cabinet of forms where each form can have different boxes filled in. You can still search across all the forms quickly.

## What problem does it solve?

Many apps store data as JSON documents using MongoDB. Running MongoDB yourself means managing servers, replication and backups. DocumentDB does that for you.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Document** | A record stored as JSON-like data. |
| **Collection** | A group of documents (like a table). |
| **Elastic cluster** | A DocumentDB option that scales to very large sizes. |

## How it works (step by step)

1. Create a cluster in private subnets.
2. Connect with MongoDB drivers using TLS.
3. Data is stored six ways across three AZs (similar to Aurora).

## When to use it

- Existing MongoDB apps moving to AWS; content catalogues, profiles.

## When NOT to use it (and what to use instead)

- **Need every MongoDB feature exactly.** Check compatibility, or consider MongoDB Atlas on AWS.
- **Simple key lookups at massive scale.** → [DynamoDB](dynamodb.md).

## Real-world example

**Scenario:** A recipe app stores recipes as JSON in self-managed MongoDB.

**How it helps:** Moving to DocumentDB removes server patching and adds automated backups.

**What it looks like:**

```
 App (MongoDB driver) ──TLS──► DocumentDB cluster (private subnets)
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per instance-hour, storage and I/O. A free trial may be available for new users – check the pricing page. Delete the cluster quickly.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon DocumentDB** → **Create cluster** and review the options.

### Option B – Using the AWS CLI (typing commands)

```bash
aws docdb describe-db-clusters
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete instances, then the cluster.

## How much does it cost?

Per instance-hour, per GB-month of storage, per million I/Os and backup storage.

Official pricing: <https://aws.amazon.com/documentdb/pricing/>

## Security tips

- Keep TLS on, use private subnets and Secrets Manager.

## Common mistakes

- Assuming 100% MongoDB compatibility without testing.

## Works well with

- [Lambda](../compute/lambda.md), [EC2](../compute/ec2.md), [Database Migration Service](../migration-transfer/database-migration-service.md).

## Quick check (test yourself)

1. Which tools can talk to DocumentDB?
   <details><summary>Answer</summary>Many MongoDB drivers and tools.</details>
2. What is a collection?
   <details><summary>Answer</summary>A group of documents, like a table.</details>
3. Is it public by default?
   <details><summary>Answer</summary>No, it runs in your VPC.</details>

## Learn more

- [Amazon DocumentDB Developer Guide](https://docs.aws.amazon.com/documentdb/latest/developerguide/what-is.html)
- [DocumentDB pricing](https://aws.amazon.com/documentdb/pricing/)
