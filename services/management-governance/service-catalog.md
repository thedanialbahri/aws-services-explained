# AWS Service Catalog

**Category:** Management & governance  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Service Catalog lets an IT team publish a menu of approved, pre-built AWS setups that other staff can launch themselves.

## Real-life comparison

It's like a company's approved-equipment catalogue. Staff can order a standard laptop or monitor themselves, without asking IT to build one from scratch – and they can only pick from the approved list.

## What problem does it solve?

Teams want to move fast, but central IT wants everything secure and consistent. Service Catalog gives teams self-service while IT controls what's available.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Product** | A CloudFormation or Terraform template offered in the catalogue. |
| **Portfolio** | A collection of products shared with certain users. |
| **Constraint** | A rule, e.g. which instance sizes are allowed. |

## How it works (step by step)

1. IT creates products from templates.
2. IT groups them into portfolios and shares them with users.
3. Users launch products from the catalogue.

## When to use it

- Larger organisations offering standard environments.

## When NOT to use it (and what to use instead)

- **Small teams.** Templates in Git with [CloudFormation](cloudformation.md) or Terraform are enough.

## Real-world example

**Scenario:** A university's research teams need servers quickly.

**How it helps:** IT publishes an approved "research server" product with encryption and budgets built in.

**What it looks like:**

```
 IT ──publishes──► Portfolio [Research server, Data bucket] ──► Researchers launch
```

## Try it yourself

> ⚠️ **Cost warning:** Free for small use; you pay for what products create.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Service Catalog** → **Portfolios** → **Create portfolio**.
2. Add a product using the `bucket.yaml` template from the [CloudFormation page](cloudformation.md).

### Option B – Using the AWS CLI (typing commands)

```bash
aws servicecatalog list-portfolios
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Terminate launched products, remove the product from the portfolio, then delete both.

## How much does it cost?

A small per-API-call charge above a free amount.

Official pricing: <https://aws.amazon.com/servicecatalog/pricing/>

## Security tips

- Use launch constraints so users don't need broad permissions.

## Common mistakes

- Publishing products that aren't maintained.

## Works well with

- [CloudFormation](cloudformation.md), [Organizations](../security-identity-compliance/organizations.md).

## Quick check (test yourself)

1. What is a portfolio?
   <details><summary>Answer</summary>A collection of products shared with users.</details>
2. What is a product built from?
   <details><summary>Answer</summary>A CloudFormation or Terraform template.</details>
3. Who benefits most?
   <details><summary>Answer</summary>Larger organisations with central IT.</details>

## Learn more

- [AWS Service Catalog Administrator Guide](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/introduction.html)
