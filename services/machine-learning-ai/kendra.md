# Amazon Kendra

**Category:** Machine learning & AI  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Kendra is an intelligent search service that finds answers across your organisation's documents and systems.

## Real-life comparison

It's like a librarian who has read every document in the company and can point you to the exact paragraph that answers your question.

## What problem does it solve?

Information is scattered across SharePoint, file shares and wikis, and keyword search misses things. Kendra understands questions and ranks the best answers.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Index** | Kendra's searchable store. |
| **Connector** | Pulls content from sources like S3, SharePoint, Confluence. |
| **GenAI index** | An index designed for use with generative AI (RAG). |

## How it works (step by step)

1. Create an index.
2. Add data sources with connectors.
3. Users search; Kendra returns answers and documents.

## When to use it

- Enterprise search; as the retriever for AI assistants.

## When NOT to use it (and what to use instead)

- **Small projects.** → A [Bedrock](bedrock.md) knowledge base or [OpenSearch](../analytics/opensearch.md) may be cheaper.

## Real-world example

**Scenario:** HR staff spend hours finding policy answers.

**How it helps:** Kendra indexes the HR SharePoint; staff ask "How many days' paternity leave do I get?" and get the paragraph.

**What it looks like:**

```
 SharePoint + S3 ──connectors──► Kendra index ──► search box / AI assistant
```

## Try it yourself

> ⚠️ **Cost warning:** Indexes are charged per hour and are **expensive to leave running**. Only browse unless you have a budget.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Kendra** → **Create an index** and review the editions. Cancel to avoid charges.

### Option B – Using the AWS CLI (typing commands)

```bash
aws kendra list-indices
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete any index you created.

## How much does it cost?

Per index-hour by edition, plus connector usage.

Official pricing: <https://aws.amazon.com/kendra/pricing/>

## Security tips

- Respect document permissions (Kendra can filter results by user access).

## Common mistakes

- Leaving a test index running.

## Works well with

- [Bedrock](bedrock.md), [Amazon Q](amazon-q.md), [S3](../storage/s3.md).

## Quick check (test yourself)

1. What does a connector do?
   <details><summary>Answer</summary>Pulls content from a source into the index.</details>
2. Is Kendra cheap to leave running?
   <details><summary>Answer</summary>No.</details>
3. What's a cheaper option for small projects?
   <details><summary>Answer</summary>A Bedrock knowledge base or OpenSearch.</details>

## Learn more

- [Amazon Kendra Developer Guide](https://docs.aws.amazon.com/kendra/latest/dg/what-is-kendra.html)
