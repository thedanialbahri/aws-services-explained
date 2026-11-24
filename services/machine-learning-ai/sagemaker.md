# Amazon SageMaker

**Category:** Machine learning & AI  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ℹ️ **About the name:** In December 2024 AWS renamed the original ML service to **Amazon SageMaker AI**. The name **Amazon SageMaker** now means a wider data, analytics and AI platform, which includes **SageMaker Unified Studio** and SageMaker AI. This page is about **SageMaker AI**. Some SageMaker AI features, such as Ground Truth, Clarify and Studio Lab, closed to new customers in July 2026.

## In one sentence

SageMaker is a set of tools to prepare data, build, train and deploy your own machine learning models.

## Real-life comparison

If the ready-made AI services are takeaway meals, SageMaker is a fully equipped professional kitchen where you cook your own recipes.

## What problem does it solve?

Training models needs powerful computers, notebooks, experiment tracking and somewhere to host the finished model. SageMaker provides all of these, managed.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Model** | What ML produces – a program that makes predictions. |
| **Training job** | Teaching a model using data. |
| **Endpoint** | A hosted model you can send requests to. |
| **Studio** | The web-based workspace (notebooks and tools). |
| **JumpStart** | Ready-made models and solutions to start from. |

## How it works (step by step)

1. Prepare data in S3.
2. Train a model with a training job.
3. Evaluate it.
4. Deploy to an endpoint (or run batch predictions).

## When to use it

- Custom ML: fraud scores, demand forecasts, image models on your own data.

## When NOT to use it (and what to use instead)

- **A ready-made AI service already does the job.** → e.g. [Rekognition](rekognition.md), [Comprehend](comprehend.md).
- **Using existing generative AI models.** → [Bedrock](bedrock.md).

## Real-world example

**Scenario:** An insurer wants to predict which claims might be fraudulent.

**How it helps:** Data scientists train a model on past claims and deploy it to an endpoint the claims system calls.

**What it looks like:**

```
 S3 data ──► SageMaker training ──► model ──► endpoint ◄── claims app
```

## Try it yourself

> ⚠️ **Cost warning:** Notebooks, training and endpoints are charged per hour. **Endpoints charge until deleted.** New accounts may have a limited free tier – check first.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon SageMaker AI** and look through **JumpStart** models without deploying.

### Option B – Using the AWS CLI (typing commands)

```bash
# Check for running endpoints (these cost money)
aws sagemaker list-endpoints
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete endpoints, endpoint configurations and models; stop notebooks and Studio apps.

## How much does it cost?

Per instance-hour for notebooks, training and hosting, plus storage.

Official pricing: <https://aws.amazon.com/sagemaker/pricing/>

## Security tips

- Run in a VPC, encrypt data, and use least-privilege execution roles.

## Common mistakes

- Leaving endpoints running after testing.

## Works well with

- [S3](../storage/s3.md), [Bedrock](bedrock.md), [Glue](../analytics/glue.md).

## Quick check (test yourself)

1. What is an endpoint?
   <details><summary>Answer</summary>A hosted model you can send requests to.</details>
2. What should you check to avoid charges?
   <details><summary>Answer</summary>That no endpoints are left running.</details>
3. When should you use a ready-made AI service instead?
   <details><summary>Answer</summary>When it already solves your problem.</details>

## Learn more

- [Amazon SageMaker AI documentation](https://docs.aws.amazon.com/sagemaker/)
