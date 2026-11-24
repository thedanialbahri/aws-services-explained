# AWS Data Exchange

**Category:** Analytics  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Data Exchange is a marketplace where you can find, subscribe to and use third-party data sets in AWS.

## Real-life comparison

It's like a newsagent for data: browse titles, subscribe, and new editions arrive automatically.

## What problem does it solve?

Getting data from providers (weather, finance, demographics) used to mean emails, FTP and contracts. Data Exchange delivers it directly into S3, Redshift or via APIs.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Data product** | A data set offered by a provider. |
| **Subscription** | Your access to a product. |
| **Revision** | A new version of the data. |

## How it works (step by step)

1. Browse data products in AWS Marketplace.
2. Subscribe (some are free).
3. Export revisions to S3 or query through Redshift or APIs.

## When to use it

- Adding external data to your analytics.

## When NOT to use it (and what to use instead)

- **Your own internal data.** → [S3](../storage/s3.md) and [Glue](glue.md).

## Real-world example

**Scenario:** An energy company wants weather data to forecast demand.

**How it helps:** It subscribes to a weather data product delivered to S3 daily.

**What it looks like:**

```
 Provider ──► Data Exchange ──► your S3 bucket ──► Athena / SageMaker
```

## Try it yourself

> ⚠️ **Cost warning:** Many products are paid; there are free ones to explore.

### Option A – Using the AWS Console (clicking in the website)

1. Open **AWS Data Exchange** → **Browse catalog** and filter for free products.

### Option B – Using the AWS CLI (typing commands)

```bash
aws dataexchange list-data-sets --origin ENTITLED
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Cancel any subscriptions and delete exported data.

## How much does it cost?

Set by each provider; plus your own storage costs.

Official info: <https://aws.amazon.com/data-exchange/pricing/>

## Security tips

- Check licence terms before sharing data.

## Common mistakes

- Forgetting auto-renewing paid subscriptions.

## Works well with

- [S3](../storage/s3.md), [Redshift](../databases/redshift.md), [Athena](athena.md).

## Quick check (test yourself)

1. What is a data product?
   <details><summary>Answer</summary>A data set offered by a provider.</details>
2. Where can data be delivered?
   <details><summary>Answer</summary>S3, Redshift or APIs.</details>
3. Are all products paid?
   <details><summary>Answer</summary>No, some are free.</details>

## Learn more

- [AWS Data Exchange User Guide](https://docs.aws.amazon.com/data-exchange/latest/userguide/what-is.html)
