# Savings Plans

**Category:** Cost management  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Savings Plans give you lower prices on compute (EC2, Fargate, Lambda and some ML) in return for promising to spend a set amount per hour for 1 or 3 years.

## Real-life comparison

It's like a gym membership vs paying per visit. Commit to a monthly fee for a year and each visit is much cheaper – but you pay even in weeks you don't go.

## What problem does it solve?

On-demand prices are flexible but highest. If you know you'll use a steady amount, committing saves a lot.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Commitment** | The amount per hour you promise to spend (e.g. $1/hour). |
| **Compute Savings Plan** | Flexible: applies across EC2, Fargate and Lambda, any Region. |
| **EC2 Instance Savings Plan** | Bigger discount, but tied to an instance family in one Region. |
| **Term** | 1 or 3 years. |
| **Payment option** | No upfront, partial upfront or all upfront. |

## How it works (step by step)

1. Check the Savings Plans **recommendations** in the Console.
2. Buy a plan with a commitment per hour.
3. Matching usage is automatically charged at the lower rate up to your commitment.
4. Usage above it is charged on-demand.

## When to use it

- Steady compute that will run for at least a year.

## When NOT to use it (and what to use instead)

- **Short projects or learning.** Stay on-demand.
- **Interruptible work.** → Spot Instances can be cheaper still.

## Real-world example

**Scenario:** A company always runs at least 10 servers.

**How it helps:** A Compute Savings Plan covering that baseline cuts its compute bill; extra servers on busy days are on-demand.

**What it looks like:**

```
 Hourly usage:  ████ commitment (discounted) ░░ extra (on-demand)
```

## Try it yourself

> ⚠️ **Cost warning:** **Don't buy a Savings Plan for learning** – it's a 1–3 year financial commitment and can't be cancelled.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Billing and Cost Management** → **Savings Plans** → **Recommendations** to look only.

### Option B – Using the AWS CLI (typing commands)

```bash
# View Savings Plans you own (read-only)
aws savingsplans describe-savings-plans
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Nothing to clean up if you only looked.

## How much does it cost?

You pay your commitment every hour of the term, whether you use it or not.

Official pricing: <https://aws.amazon.com/savingsplans/pricing/>

## Security tips

- Limit who can purchase commitments.

## Common mistakes

- Committing too much based on a busy month.

## Works well with

- [Cost Explorer](cost-explorer.md), [Reserved Instances](reserved-instances.md).

## Quick check (test yourself)

1. What do you commit to?
   <details><summary>Answer</summary>A spend per hour for 1 or 3 years.</details>
2. Which plan type is most flexible?
   <details><summary>Answer</summary>Compute Savings Plan.</details>
3. Should you buy one while learning?
   <details><summary>Answer</summary>No.</details>

## Learn more

- [Savings Plans User Guide](https://docs.aws.amazon.com/savingsplans/latest/userguide/what-is-savings-plans.html)
