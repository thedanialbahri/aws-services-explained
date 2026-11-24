# AWS Cost Explorer

**Category:** Cost management  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Cost Explorer shows charts and tables of your AWS spending, so you can see what costs money, where, and how it's changing.

## Real-life comparison

It's like the spending analysis in a banking app: a pie chart showing groceries vs travel vs bills, and how this month compares to last month.

## What problem does it solve?

A bill tells you the total; Cost Explorer tells you the story – which service, which Region, which project, and whether it's growing.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Group by** | Split costs by service, Region, tag and so on. |
| **Filter** | Show only some costs, e.g. only EC2. |
| **Forecast** | AWS's prediction of future spending. |
| **Granularity** | Daily, monthly or hourly view. |

## How it works (step by step)

1. Open Cost Explorer (it may need enabling the first time; data then takes up to 24 hours).
2. Choose a date range, granularity and **Group by**.
3. Add filters to drill down.
4. Save useful views as reports.

## When to use it

- Weekly cost checks and investigating spikes.

## When NOT to use it (and what to use instead)

- **Alerts.** → [Budgets](budgets.md).
- **Estimating before you build.** → [Pricing Calculator](pricing-calculator.md).

## Real-world example

**Scenario:** A team's bill doubled.

**How it helps:** Grouping by service shows data transfer jumped; grouping by usage type shows it's NAT gateway traffic from a new app.

**What it looks like:**

```
 Cost Explorer ──group by Service──► EC2-Other ↑ ──group by Usage type──► NatGateway-Bytes ↑
```

## Try it yourself

> ⚠️ **Cost warning:** The Console is free. Cost Explorer API calls are charged per request.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Billing and Cost Management** → **Cost Explorer**.
2. Set **Date range** to the last 3 months and **Granularity** to Monthly.
3. **Group by:** **Service**.
4. Change **Group by** to **Region** and compare.

### Option B – Using the AWS CLI (typing commands)

```bash
# Last month's cost by service (set the dates)
aws ce get-cost-and-usage --region us-east-1 \
  --time-period Start=2026-10-01,End=2026-11-01 --granularity MONTHLY \
  --metrics UnblendedCost --group-by Type=DIMENSION,Key=SERVICE
```

### Option C – Using Terraform (infrastructure as code)

Not applicable – it's a reporting tool.

### Clean up (delete what you made)

Nothing to clean up.

## How much does it cost?

Console use is free; API requests are charged per request.

Official pricing: <https://aws.amazon.com/aws-cost-management/aws-cost-explorer/pricing/>

## Security tips

- Limit access – cost data can reveal business information.

## Common mistakes

- Forgetting to activate cost allocation tags, so grouping by tag shows nothing.

## Works well with

- [Budgets](budgets.md), [Billing](billing.md).

## Quick check (test yourself)

1. How do you see costs per service?
   <details><summary>Answer</summary>Group by Service.</details>
2. Is the Cost Explorer Console free?
   <details><summary>Answer</summary>Yes (the API is charged).</details>
3. What must you do before grouping by your own tags?
   <details><summary>Answer</summary>Activate them as cost allocation tags.</details>

## Learn more

- [Cost Explorer documentation](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-what-is.html)
