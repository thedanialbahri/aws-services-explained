# Reserved Instances (RIs)

**Category:** Cost management  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Reserved Instances give a discount on specific resources (such as RDS, ElastiCache, Redshift or EC2) in return for a 1- or 3-year commitment.

## Real-life comparison

It's like a season ticket for one particular train route. Much cheaper than daily tickets, but only for that route.

## What problem does it solve?

Databases and other long-running resources often run for years. RIs lower their cost. For EC2, AWS generally recommends Savings Plans instead because they're more flexible.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Standard RI** | Biggest discount, least flexible. |
| **Convertible RI** | Can be exchanged for other types; smaller discount. |
| **Scope** | Regional or a specific AZ. |

## How it works (step by step)

1. Choose the service, instance type, Region and term.
2. Buy the RI.
3. Matching running resources are billed at the RI rate automatically.

## When to use it

- Steady RDS, ElastiCache, OpenSearch or Redshift usage.

## When NOT to use it (and what to use instead)

- **EC2, Fargate, Lambda.** → [Savings Plans](savings-plans.md) usually fit better.

## Real-world example

**Scenario:** An app's production RDS database will run 24/7 for at least three years.

**How it helps:** A 3-year RDS RI cuts the database's cost substantially.

**What it looks like:**

```
 RDS db.r6g.large (eu-west-2) ◄── matched by ── 3-year RI
```

## Try it yourself

> ⚠️ **Cost warning:** **Don't buy RIs for learning** – they are long financial commitments.

### Option A – Using the AWS Console (clicking in the website)

1. Open **RDS** → **Reserved instances** → **Purchase reserved DB instance** to see offerings, then cancel.

### Option B – Using the AWS CLI (typing commands)

```bash
# Browse RDS RI offerings (read-only)
aws rds describe-reserved-db-instances-offerings --db-instance-class db.t4g.micro --max-records 20
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Nothing to clean up if you only browsed.

## How much does it cost?

Paid for the whole term, upfront, partly upfront or monthly.

Official info: <https://aws.amazon.com/ec2/pricing/reserved-instances/>

## Security tips

- Limit who can buy reservations.

## Common mistakes

- Buying an RI that doesn't match what's actually running.

## Works well with

- [RDS](../databases/rds.md), [Cost Explorer](cost-explorer.md).

## Quick check (test yourself)

1. What do RIs need in return for a discount?
   <details><summary>Answer</summary>A 1- or 3-year commitment.</details>
2. For EC2, what's usually more flexible?
   <details><summary>Answer</summary>Savings Plans.</details>
3. Which RI type can be exchanged?
   <details><summary>Answer</summary>Convertible RI.</details>

## Learn more

- [Reserved Instances (EC2) documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-reserved-instances.html)
