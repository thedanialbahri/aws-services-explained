# Amazon MemoryDB

**Category:** Databases  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

MemoryDB is an in-memory database compatible with Valkey and Redis OSS that also keeps your data safely, so it can be your main database, not just a cache.

## Real-life comparison

ElastiCache is a whiteboard – quick to read but easily wiped. MemoryDB is a whiteboard that photographs itself after every change, so nothing is lost if it's wiped.

## What problem does it solve?

Apps that need microsecond speed often used a cache *and* a database, which is complex. MemoryDB is both: fast like a cache, durable like a database (it writes to a multi-AZ transaction log).

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Durable** | Data survives failures. |
| **Transaction log** | A record of every change, stored across AZs. |
| **Cluster** | A group of nodes running MemoryDB. |

## How it works (step by step)

1. Create a cluster in your VPC.
2. Apps use normal Valkey/Redis commands.
3. Each write is saved to a multi-AZ log before it's confirmed.

## When to use it

- Very fast primary databases for sessions, leaderboards, real-time apps.

## When NOT to use it (and what to use instead)

- **Just a cache in front of another database.** → [ElastiCache](elasticache.md) (cheaper).

## Real-world example

**Scenario:** A betting app needs live odds updated thousands of times a second and can't lose bets.

**How it helps:** MemoryDB gives microsecond reads with durable writes.

**What it looks like:**

```
 App ──► MemoryDB (in-memory + multi-AZ transaction log)
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per node-hour and per GB written. No meaningful free option – only browse unless you're prepared to pay.

### Option A – Using the AWS Console (clicking in the website)

1. Open **MemoryDB** → **Clusters** → **Create cluster** and read the options. Cancel to avoid charges.

### Option B – Using the AWS CLI (typing commands)

```bash
aws memorydb describe-clusters
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete any cluster you created.

## How much does it cost?

Per node-hour plus data written per GB, plus snapshot storage.

Official pricing: <https://aws.amazon.com/memorydb/pricing/>

## Security tips

- Use ACLs (user access lists), TLS and private subnets.

## Common mistakes

- Using it only as a cache and overpaying.

## Works well with

- [EC2](../compute/ec2.md), [ECS](../containers/ecs.md), [Lambda](../compute/lambda.md).

## Quick check (test yourself)

1. How is MemoryDB different from ElastiCache?
   <details><summary>Answer</summary>It's durable and can be a primary database, not just a cache.</details>
2. Which commands does it support?
   <details><summary>Answer</summary>Valkey / Redis OSS commands.</details>
3. Where is every write recorded?
   <details><summary>Answer</summary>In a multi-AZ transaction log.</details>

## Learn more

- [Amazon MemoryDB Developer Guide](https://docs.aws.amazon.com/memorydb/latest/devguide/what-is-memorydb.html)
- [MemoryDB pricing](https://aws.amazon.com/memorydb/pricing/)
