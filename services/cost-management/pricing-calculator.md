# AWS Pricing Calculator

**Category:** Cost management  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

The Pricing Calculator lets you estimate what an AWS setup will cost before you build it.

## Real-life comparison

It's like a car insurance comparison site: put in the details, see the estimated price, change options and compare.

## What problem does it solve?

AWS pricing has many parts. The calculator adds them up for you so you can plan budgets and compare designs.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Estimate** | A saved collection of services with their expected usage. |
| **Group** | A section of an estimate, e.g. "web tier". |

## How it works (step by step)

1. Open <https://calculator.aws/>.
2. Add services and enter expected usage.
3. See monthly and yearly totals.
4. Save and share the estimate link, or export it.

## When to use it

- Planning a project or comparing options.

## When NOT to use it (and what to use instead)

- **Seeing what you actually spent.** → [Cost Explorer](cost-explorer.md).

## Real-world example

**Scenario:** A charity wants to compare running its website on EC2 vs Lightsail.

**How it helps:** Two estimates show the monthly cost of each, including storage and data transfer.

**What it looks like:**

```
 Estimate A: EC2 + EBS + ALB  vs  Estimate B: Lightsail plan
```

## Try it yourself

> ⚠️ **Cost warning:** Free.

### Option A – Using the AWS Console (clicking in the website)

1. Go to <https://calculator.aws/> → **Create estimate**.
2. Search **Amazon EC2** → **Configure**.
3. Choose Region **Europe (London)**, 1 instance of `t3.micro`, 730 hours a month.
4. Click **Save and add service**, then view the summary.

### Option B – Using the AWS CLI (typing commands)

```bash
# Look up raw price data for t3.micro Linux in London (Price List API)
aws pricing get-products --region us-east-1 --service-code AmazonEC2 \
  --filters Type=TERM_MATCH,Field=instanceType,Value=t3.micro \
            Type=TERM_MATCH,Field=location,Value="EU (London)" \
            Type=TERM_MATCH,Field=operatingSystem,Value=Linux --max-results 1
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Nothing to clean up.

## How much does it cost?

Free.

## Security tips

- Shared estimate links can be opened by anyone with the link.

## Common mistakes

- Forgetting data transfer, NAT gateways or storage in estimates.

## Works well with

- [Budgets](budgets.md), [Savings Plans](savings-plans.md).

## Quick check (test yourself)

1. What's the calculator's web address?
   <details><summary>Answer</summary>calculator.aws</details>
2. Is it free?
   <details><summary>Answer</summary>Yes.</details>
3. Name a cost people often forget.
   <details><summary>Answer</summary>Data transfer (or NAT gateways, or storage).</details>

## Learn more

- [AWS Pricing Calculator User Guide](https://docs.aws.amazon.com/pricing-calculator/latest/userguide/what-is-pricing-calculator.html)
