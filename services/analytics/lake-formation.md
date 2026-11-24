# AWS Lake Formation

**Category:** Analytics  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Lake Formation helps you build a data lake in S3 and control who can see which databases, tables, columns and rows.

## Real-life comparison

It's like a library's membership system that says which readers can enter which rooms – and even which pages of which books they're allowed to read.

## What problem does it solve?

Giving people access to data lakes with S3 bucket policies alone is clumsy. Lake Formation gives fine-grained permissions across Athena, Redshift, EMR and Glue.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Data lake** | One big store of raw and processed data, usually in S3. |
| **Data location** | An S3 path registered with Lake Formation. |
| **Fine-grained access** | Column- and row-level permissions. |
| **LF-Tags** | Labels used to grant access at scale. |

## How it works (step by step)

1. Register S3 locations.
2. Catalogue data with Glue.
3. Grant permissions on databases, tables, columns or rows.
4. Query engines check Lake Formation before returning data.

## When to use it

- Data lakes shared by many teams with different access needs.

## When NOT to use it (and what to use instead)

- **One small bucket and one user.** IAM and S3 policies are enough.

## Real-world example

**Scenario:** HR and marketing share a customer data lake.

**How it helps:** Marketing sees purchase history but not salary or personal columns.

**What it looks like:**

```
 Athena query ──► Lake Formation (check permissions) ──► allowed columns only
```

## Try it yourself

> ⚠️ **Cost warning:** No extra charge for Lake Formation permissions; you pay for S3, Glue and query engines.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Lake Formation** and add yourself as a data lake administrator.
2. Explore **Data permissions** for the `demo` database from the [Glue](glue.md) page.

### Option B – Using the AWS CLI (typing commands)

```bash
aws lakeformation list-permissions
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Revoke test permissions and deregister locations.

## How much does it cost?

Free for permissions; some features (e.g. transactions) and underlying services are charged.

Official pricing: <https://aws.amazon.com/lake-formation/pricing/>

## Security tips

- Use LF-Tags for scalable permissions.

## Common mistakes

- Mixing IAM-only and Lake Formation permissions without understanding which applies.

## Works well with

- [Glue](glue.md), [Athena](athena.md), [S3](../storage/s3.md).

## Quick check (test yourself)

1. What is a data lake?
   <details><summary>Answer</summary>One large store of raw and processed data, usually in S3.</details>
2. Can Lake Formation limit access to certain columns?
   <details><summary>Answer</summary>Yes.</details>
3. What are LF-Tags?
   <details><summary>Answer</summary>Labels used to grant permissions at scale.</details>

## Learn more

- [AWS Lake Formation Developer Guide](https://docs.aws.amazon.com/lake-formation/latest/dg/what-is-lake-formation.html)
