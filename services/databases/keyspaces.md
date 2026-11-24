# Amazon Keyspaces (for Apache Cassandra)

**Category:** Databases  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Keyspaces is a serverless database compatible with Apache Cassandra, so Cassandra apps can run on AWS without managing servers.

## Real-life comparison

It's like switching from maintaining your own fleet of lorries to using a delivery firm that uses the same type of lorries – your drivers already know how to use them.

## What problem does it solve?

Cassandra handles huge write-heavy workloads but is hard to run. Keyspaces removes the servers while keeping the same query language (CQL).

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Keyspace** | A group of tables (like a database). |
| **CQL** | Cassandra Query Language. |
| **Partition key** | Decides where data is stored. |

## How it works (step by step)

1. Create a keyspace and tables.
2. Connect with Cassandra drivers using TLS.
3. Choose on-demand or provisioned capacity.

## When to use it

- Moving existing Cassandra workloads to AWS.

## When NOT to use it (and what to use instead)

- **New apps with no Cassandra history.** → [DynamoDB](dynamodb.md) is usually simpler.

## Real-world example

**Scenario:** A logistics firm tracks millions of parcel scans a day in Cassandra.

**How it helps:** It moves to Keyspaces and stops managing a 12-node cluster.

**What it looks like:**

```
 Scanners ──► App (Cassandra driver) ──► Keyspaces table
```

## Try it yourself

> ⚠️ **Cost warning:** Free Tier for a limited amount of reads, writes and storage in the first months (check the pricing page). Delete tables afterwards.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Keyspaces** → **Create keyspace** (`demo`), then **Create table**.
2. Use **CQL editor** to run `SELECT * FROM demo.yourtable;`.

### Option B – Using the AWS CLI (typing commands)

```bash
aws keyspaces create-keyspace --keyspace-name demo
```

### Option C – Using Terraform (infrastructure as code)

```hcl
resource "aws_keyspaces_keyspace" "demo" {
  name = "demo"
}
```

### Clean up (delete what you made)

Delete tables, then the keyspace.

## How much does it cost?

On-demand per million reads/writes, or provisioned capacity per hour, plus storage per GB-month.

Official pricing: <https://aws.amazon.com/keyspaces/pricing/>

## Security tips

- Use IAM authentication and TLS.

## Common mistakes

- Expecting every Cassandra feature to be supported – check the docs.

## Works well with

- [Lambda](../compute/lambda.md), [ECS](../containers/ecs.md).

## Quick check (test yourself)

1. Which query language does Keyspaces use?
   <details><summary>Answer</summary>CQL (Cassandra Query Language).</details>
2. Do you manage servers?
   <details><summary>Answer</summary>No, it's serverless.</details>
3. For a brand-new app, what's often simpler?
   <details><summary>Answer</summary>DynamoDB.</details>

## Learn more

- [Amazon Keyspaces Developer Guide](https://docs.aws.amazon.com/keyspaces/latest/devguide/what-is-keyspaces.html)
- [Keyspaces pricing](https://aws.amazon.com/keyspaces/pricing/)
