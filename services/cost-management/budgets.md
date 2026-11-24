# AWS Budgets

**Category:** Cost management  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Budgets lets you set a spending limit and get an email (or other alert) when your actual or forecast AWS costs go over it.

## Real-life comparison

AWS Budgets is like the text your bank sends when your balance drops below £50, or a spending limit on a teenager's card. It doesn't stop the spending by itself, but it warns you in time to act.

## What problem does it solve?

Cloud bills can grow quietly – a forgotten server, a test database left on. Without alerts, you only find out when the bill arrives. Budgets warns you early, even before you've spent the money (forecast alerts).

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Budget** | A limit you set, e.g. £10 per month. |
| **Cost budget** | Tracks money spent. |
| **Usage budget** | Tracks an amount used, e.g. hours of EC2. |
| **Zero spend budget** | Alerts as soon as you spend anything at all. |
| **Actual vs forecasted** | Alert on what you've spent, or on what AWS predicts you'll spend by month end. |
| **Budget action** | An automatic response, e.g. apply a restrictive IAM policy. |

## How it works (step by step)

1. You create a budget with an amount and period (usually monthly).
2. You add one or more alert **thresholds**, e.g. 80% actual and 100% forecasted.
3. You add email addresses (or an [SNS](../application-integration/sns.md) topic).
4. AWS checks your costs several times a day.
5. When a threshold is crossed, you get an alert.

## When to use it

- Every account, from day one.
- Per project or team, using tags.

## When NOT to use it (and what to use instead)

- **Investigating where money went.** → [Cost Explorer](cost-explorer.md).
- **A hard cap that stops all spending.** AWS doesn't have a simple "stop at £X" switch. Budget actions can restrict permissions or stop some instances, but you should still clean up yourself.

## Real-world example

**Scenario:** Danial is learning AWS with a personal account.

**The problem:** He's worried about forgetting to delete something and getting a big bill.

**How Budgets helps:** He creates a zero spend budget and a £5 monthly budget with alerts at 80% actual and 100% forecast. When he forgets a NAT gateway, he gets an email the same day.

**What it looks like:**

```
 AWS usage ──► Budgets (£5/month)
                 ├─ 80% actual     ──► email
                 └─ 100% forecast  ──► email
```

## Try it yourself

> ⚠️ **Cost warning:** A small number of budgets are free; extra budgets and budget actions have small charges.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Billing and Cost Management** → **Budgets** → **Create budget**.
2. Choose **Use a template (simplified)** → **Monthly cost budget**.
3. **Budget name:** `monthly-learning`. **Budgeted amount:** `5` (USD).
4. **Email recipients:** your email.
5. Click **Create budget**.
6. Open the budget to see alerts at 85% and 100% actual, and 100% forecasted (the template's defaults).

### Option B – Using the AWS CLI (typing commands)

Save as `budget.json`:
```json
{
  "BudgetName": "monthly-learning",
  "BudgetLimit": { "Amount": "5", "Unit": "USD" },
  "TimeUnit": "MONTHLY",
  "BudgetType": "COST"
}
```
Save as `notifications.json`:
```json
[
  {
    "Notification": { "NotificationType": "ACTUAL", "ComparisonOperator": "GREATER_THAN", "Threshold": 80, "ThresholdType": "PERCENTAGE" },
    "Subscribers": [ { "SubscriptionType": "EMAIL", "Address": "you@example.com" } ]
  }
]
```
Then run:
```bash
# Create the budget with an 80% alert (replace the account ID)
aws budgets create-budget --account-id 123456789012 \
  --budget file://budget.json \
  --notifications-with-subscribers file://notifications.json
```

### Option C – Using Terraform (infrastructure as code)

Written for the AWS provider `~> 6.0`.

```hcl
# $5 monthly budget with two email alerts
resource "aws_budgets_budget" "monthly" {
  name         = "monthly-learning"
  budget_type  = "COST"
  limit_amount = "5"
  limit_unit   = "USD"
  time_unit    = "MONTHLY"

  # Alert when actual spend passes 80%
  notification {
    comparison_operator        = "GREATER_THAN"
    threshold                  = 80
    threshold_type             = "PERCENTAGE"
    notification_type          = "ACTUAL"
    subscriber_email_addresses = ["you@example.com"]
  }

  # Alert when AWS forecasts you'll pass 100%
  notification {
    comparison_operator        = "GREATER_THAN"
    threshold                  = 100
    threshold_type             = "PERCENTAGE"
    notification_type          = "FORECASTED"
    subscriber_email_addresses = ["you@example.com"]
  }
}
```

### Clean up (delete what you made)

Keep your budget – it protects you. To delete a test one: **Budgets** → tick it → **Actions** → **Delete**.

## How much does it cost?

A few budgets per account are free; extra budgets are charged per budget per day, and budget actions have a small charge.

Official pricing: <https://aws.amazon.com/aws-cost-management/aws-budgets/pricing/>

## Security tips

- Send alerts to a shared mailbox, not just one person.
- Budget actions can apply a "deny" policy automatically if spending runs away.

## Common mistakes

- **Thinking a budget stops spending.** It alerts; you must act.
- **Only using actual alerts** – forecast alerts warn you earlier.
- **Currency confusion** – budgets are usually in USD.

## Works well with

- [SNS](../application-integration/sns.md) – send alerts to more places.
- [Cost Explorer](cost-explorer.md) – find what's costing money.
- [Organizations](../security-identity-compliance/organizations.md) – budgets across accounts.

## Quick check (test yourself)

1. Does a budget stop you spending more?
   <details><summary>Answer</summary>No. It alerts you (budget actions can restrict some things).</details>
2. What's the advantage of a forecasted alert?
   <details><summary>Answer</summary>It warns you before you actually overspend.</details>
3. What type of budget alerts as soon as you spend anything?
   <details><summary>Answer</summary>A zero spend budget.</details>

## Learn more

- [AWS Budgets User Guide](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html)
- [AWS Budgets pricing](https://aws.amazon.com/aws-cost-management/aws-budgets/pricing/)
