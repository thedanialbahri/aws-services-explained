# Amazon Neptune

**Category:** Databases  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Neptune is a graph database, built to store and search data about how things are connected.

## Real-life comparison

A graph database is like a detective's pinboard with photos joined by string. It's easy to ask "who is connected to whom, and how?"

## What problem does it solve?

Questions like "friends of friends who like the same band" or "which accounts share a device with a known fraudster" are slow in normal databases. Graph databases answer them quickly.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Node / vertex** | A thing, e.g. a person. |
| **Edge** | A connection, e.g. "follows". |
| **Gremlin / openCypher / SPARQL** | Query languages for graphs. |

## How it works (step by step)

1. Create a Neptune cluster (or Neptune Serverless).
2. Load nodes and edges.
3. Run graph queries.

## When to use it

- Social networks, fraud detection, recommendations, knowledge graphs.

## When NOT to use it (and what to use instead)

- **Normal business data with few relationships.** → [RDS](rds.md).

## Real-world example

**Scenario:** A bank wants to spot fraud rings.

**How it helps:** Accounts, devices and addresses are nodes; shared use is an edge. A query finds groups of accounts linked to known fraud.

**What it looks like:**

```
 (Account A)─uses─►(Device X)◄─uses─(Account B)─lives at─►(Address Y)
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per instance-hour (or capacity unit for serverless) and storage. A free trial may be available – check the pricing page.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Neptune** → **Create database** and review the options; cancel if you don't want charges.

### Option B – Using the AWS CLI (typing commands)

```bash
aws neptune describe-db-clusters
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete instances, then the cluster.

## How much does it cost?

Per instance-hour, storage, I/O and backups.

Official pricing: <https://aws.amazon.com/neptune/pricing/>

## Security tips

- Private subnets, IAM authentication, encryption.

## Common mistakes

- Using a graph database for simple table data.

## Works well with

- [SageMaker](../machine-learning-ai/sagemaker.md) (Neptune ML), [Lambda](../compute/lambda.md).

## Quick check (test yourself)

1. What is an edge?
   <details><summary>Answer</summary>A connection between two nodes.</details>
2. Name a use case for graphs.
   <details><summary>Answer</summary>Fraud detection, social networks, recommendations.</details>
3. Name a graph query language.
   <details><summary>Answer</summary>Gremlin, openCypher or SPARQL.</details>

## Learn more

- [Amazon Neptune User Guide](https://docs.aws.amazon.com/neptune/latest/userguide/intro.html)
- [Neptune pricing](https://aws.amazon.com/neptune/pricing/)
