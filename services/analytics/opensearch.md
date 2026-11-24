# Amazon OpenSearch Service

**Category:** Analytics  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

OpenSearch Service runs OpenSearch clusters for fast full-text search and for searching and charting logs.

## Real-life comparison

It's like the index at the back of a huge book – it lets you jump to every page mentioning a word instantly.

## What problem does it solve?

Searching millions of log lines or product descriptions with normal databases is slow. OpenSearch is built for search.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Domain** | Your OpenSearch cluster. |
| **Index** | A collection of searchable documents. |
| **OpenSearch Dashboards** | The built-in charting and search UI. |
| **Serverless collection** | OpenSearch without managing a cluster. |

## How it works (step by step)

1. Create a domain or serverless collection.
2. Send documents (logs, products).
3. Search and build dashboards.

## When to use it

- Website search, log analytics, security monitoring.

## When NOT to use it (and what to use instead)

- **Simple AWS log searches.** → CloudWatch Logs Insights.

## Real-world example

**Scenario:** An online bookshop needs typo-tolerant search.

**How it helps:** Product data is indexed; searches like "harry poter" still find results.

**What it looks like:**

```
 Website search box ──► OpenSearch index ──► results
```

## Try it yourself

> ⚠️ **Cost warning:** Domains are charged per instance-hour and storage (a small instance may be in the Free Tier); serverless has minimum capacity charges. Delete it after testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **OpenSearch Service** → **Create domain** → **Easy create** with the smallest options and review settings.

### Option B – Using the AWS CLI (typing commands)

```bash
aws opensearch list-domain-names
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete the domain.

## How much does it cost?

Per instance-hour plus storage, or OpenSearch Compute Units for serverless.

Official pricing: <https://aws.amazon.com/opensearch-service/pricing/>

## Security tips

- Use fine-grained access control and keep domains in a VPC.

## Common mistakes

- Making a domain publicly open without authentication.

## Works well with

- [Kinesis](kinesis.md) (Firehose), [CloudWatch](../management-governance/cloudwatch.md).

## Quick check (test yourself)

1. What is an index?
   <details><summary>Answer</summary>A collection of searchable documents.</details>
2. Name two uses.
   <details><summary>Answer</summary>Website search and log analytics.</details>
3. What UI comes with it?
   <details><summary>Answer</summary>OpenSearch Dashboards.</details>

## Learn more

- [Amazon OpenSearch Service Developer Guide](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/what-is.html)
