# Amazon ElastiCache

**Category:** Databases  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

ElastiCache keeps frequently used data in memory (Valkey, Redis OSS or Memcached), so your app can get it back in microseconds instead of asking the database each time.

## Real-life comparison

A cache is like keeping the things you use most on your desk instead of walking to the filing room each time. Much faster – but the desk is small, so only the most useful things go there.

## What problem does it solve?

Databases slow down when the same popular queries run thousands of times. A cache answers those repeat requests from memory, taking load off the database.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Cache** | A fast, temporary store of frequently used data. |
| **In-memory** | Stored in RAM, which is much faster than disk. |
| **Cache hit / miss** | Found in the cache / not found, so fetch from the database. |
| **TTL** | How long an item stays before it expires. |
| **Valkey / Redis OSS / Memcached** | The cache engines you can choose. |
| **Serverless cache** | ElastiCache sizes itself automatically. |

## How it works (step by step)

1. You create a cache (serverless or node-based) in your VPC.
2. Your app checks the cache first.
3. On a **hit**, it returns the data instantly.
4. On a **miss**, it reads from the database and saves the result in the cache with a TTL.

## When to use it

- Product pages, sessions, leaderboards, results of slow queries.

## When NOT to use it (and what to use instead)

- **As your only copy of important data.** → Use a database; or [MemoryDB](memorydb.md) for durable in-memory data.

## Real-world example

**Scenario:** An online shop's home page runs the same "top products" query 5,000 times a minute.

**How it helps:** The result is cached for 60 seconds. The database runs it once a minute instead of 5,000 times.

**What it looks like:**

```
 App ──1. check──► ElastiCache ──hit──► return
      └─2. miss──► RDS ──3. save to cache──► return
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per hour (node-based) or per GB-hour and request (serverless). Small node types may be in the Free Tier for new accounts. Delete it at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Open **ElastiCache** → **Create cache** → **Valkey** → **Serverless**.
2. Name it `demo-cache`, choose your default VPC, and create.
3. Note the endpoint – apps inside the VPC connect to it.

### Option B – Using the AWS CLI (typing commands)

```bash
aws elasticache describe-serverless-caches
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# A serverless Valkey cache
resource "aws_elasticache_serverless_cache" "demo" {
  name   = "demo-cache"
  engine = "valkey"
}
```

### Clean up (delete what you made)

1. Tick the cache → **Actions** → **Delete**.

## How much does it cost?

Node-based: per node-hour by size. Serverless: per GB-hour stored plus per ElastiCache Processing Unit.

Official pricing: <https://aws.amazon.com/elasticache/pricing/>

## Security tips

- Keep caches in private subnets; turn on encryption in transit and authentication.

## Common mistakes

- Never expiring data, so users see stale information.

## Works well with

- [RDS](rds.md), [DynamoDB](dynamodb.md), [EC2](../compute/ec2.md).

## Quick check (test yourself)

1. What is a cache miss?
   <details><summary>Answer</summary>When the data isn't in the cache, so the app fetches it from the database.</details>
2. Where is cached data stored?
   <details><summary>Answer</summary>In memory (RAM).</details>
3. Should a cache be the only copy of important data?
   <details><summary>Answer</summary>No.</details>

## Learn more

- [Amazon ElastiCache User Guide](https://docs.aws.amazon.com/AmazonElastiCache/latest/dg/WhatIs.html)
- [ElastiCache pricing](https://aws.amazon.com/elasticache/pricing/)
