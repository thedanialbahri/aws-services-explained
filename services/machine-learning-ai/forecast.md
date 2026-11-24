# Amazon Forecast

**Category:** Machine learning & AI  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ⛔ **No longer available to new customers.** Use [SageMaker](sagemaker.md) (for example SageMaker Canvas) for forecasting instead.

## In one sentence

Forecast predicted future values – like sales or demand – from past time-based data.

## Real-life comparison

It was like a weather forecaster for your business numbers.

## What problem does it solve?

Planning stock and staff needs good forecasts; Forecast made that possible without ML skills.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Time series** | Values recorded over time. |
| **Predictor** | A trained forecasting model. |

## How it works (step by step)

1. Import historical data.
2. Train a predictor.
3. Generate forecasts.

## When to use it

- Existing customers only.

## When NOT to use it (and what to use instead)

- **New projects.** → [SageMaker](sagemaker.md) Canvas or your own models.

## Real-world example

**Scenario:** A retailer forecast weekly sales per store.

**Today:** New retailers use SageMaker Canvas for the same job.

**What it looks like:**

```
 Sales history ──► Predictor ──► next 12 weeks forecast
```

## Try it yourself

> ⚠️ **Cost warning:** Not applicable for new customers.

### Option A – Using the AWS Console (clicking in the website)

Not applicable – closed to new customers.

### Option B – Using the AWS CLI (typing commands)

Not applicable.

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Existing users: delete predictors and datasets you no longer need.

## How much does it cost?

Existing users pay for data storage, training hours and forecasts generated.

## Security tips

- Existing users: encrypt data with KMS.

## Common mistakes

- Following old tutorials as a new customer.

## Works well with

- [SageMaker](sagemaker.md), [S3](../storage/s3.md).

## Quick check (test yourself)

1. Can new customers use Forecast?
   <details><summary>Answer</summary>No.</details>
2. What's the suggested alternative?
   <details><summary>Answer</summary>SageMaker (e.g. SageMaker Canvas).</details>
3. What is time-series data?
   <details><summary>Answer</summary>Values recorded over time.</details>

## Learn more

- [Amazon Forecast documentation](https://docs.aws.amazon.com/forecast/)
