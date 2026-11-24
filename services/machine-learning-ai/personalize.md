# Amazon Personalize

**Category:** Machine learning & AI  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Personalize builds "you might also like" recommendations from your users' behaviour, using the same kind of technology as Amazon.com.

## Real-life comparison

It's like a shop assistant who remembers what each customer bought and suggests things they'll probably like.

## What problem does it solve?

Building a recommendation system needs ML expertise. Personalize trains one from your data with no ML background needed.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Interactions** | Clicks, views, purchases. |
| **Items / users** | What you recommend, and to whom. |
| **Recipe / recommender** | The type of recommendation model. |
| **Campaign** | A deployed model you can call. |

## How it works (step by step)

1. Import interaction, item and user data.
2. Create a recommender (e.g. "Recommended for you").
3. Call it from your app to get recommendations.

## When to use it

- Shops, streaming, news – personalised lists.

## When NOT to use it (and what to use instead)

- **Very little data.** Simple "most popular" lists may work better.

## Real-world example

**Scenario:** A bookshop wants personalised home pages.

**How it helps:** Purchase history trains a recommender; each visitor sees their own suggestions.

**What it looks like:**

```
 Purchases ──► Personalize (train) ──► recommender ──► "Recommended for you"
```

## Try it yourself

> ⚠️ **Cost warning:** Charged for data, training hours and recommendations. Free Tier may cover small trials – check before starting.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Personalize** → **Create dataset group** and read the domain options.

### Option B – Using the AWS CLI (typing commands)

```bash
aws personalize list-dataset-groups
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Delete recommenders/campaigns, solutions, datasets and the dataset group.

## How much does it cost?

Per GB of data ingested, training hours and recommendation requests or throughput.

Official pricing: <https://aws.amazon.com/personalize/pricing/>

## Security tips

- Remove personal details that aren't needed for recommendations.

## Common mistakes

- Forgetting to delete campaigns, which charge per hour.

## Works well with

- [S3](../storage/s3.md), [Lambda](../compute/lambda.md).

## Quick check (test yourself)

1. What data does Personalize learn from?
   <details><summary>Answer</summary>User interactions like clicks and purchases.</details>
2. Do you need ML expertise?
   <details><summary>Answer</summary>No.</details>
3. What should you delete to stop charges?
   <details><summary>Answer</summary>Campaigns and recommenders.</details>

## Learn more

- [Amazon Personalize Developer Guide](https://docs.aws.amazon.com/personalize/latest/dg/what-is-personalize.html)
