# Project 1: Billing alarm and monitoring dashboard

**Services:** [Budgets](../services/cost-management/budgets.md) + [CloudWatch](../services/management-governance/cloudwatch.md) + [SNS](../services/application-integration/sns.md)  **Level:** 🟢 Beginner

## What you'll build

A safety net for your AWS account:
- An **SNS topic** that emails you.
- A **budget** that warns you at 80% of £/$5 and when the forecast goes over.
- A **CloudWatch billing alarm** as a second warning.
- A **CloudWatch dashboard** showing your estimated charges.

```
 AWS usage ──► Budgets ($5) ──────────────┐
           └─► CloudWatch EstimatedCharges ─► Alarm ──► SNS topic ──► your email
                         │
                         └─► Dashboard (chart of charges)
```

## Why this matters

Real-life comparison: it's a smoke alarm for your wallet. You hope it never goes off, but you'd never live without one.

## Steps

> ⚠️ **Cost warning:** A couple of budgets, a few alarms and a few dashboards are free. This project should cost nothing.

### Step 1 – Turn on billing alerts in CloudWatch

1. Sign in as the root user or a user with billing access.
2. Open **Billing and Cost Management** → **Billing preferences**.
3. Under **Alert preferences**, tick **Receive CloudWatch billing alerts** and save.
4. Wait about 15 minutes for billing metrics to appear.

### Step 2 – Create the SNS topic (in us-east-1)

Billing metrics only exist in **US East (N. Virginia) `us-east-1`**, so the topic and alarm must be there.

1. Switch the Region to **us-east-1**.
2. Open **SNS** → **Topics** → **Create topic** → **Standard** → name `billing-alerts`.
3. **Create subscription** → **Email** → your email → confirm via the email you receive.

### Step 3 – Create the budget

1. Open **Budgets** → **Create budget** → **Monthly cost budget** template.
2. Amount `5`, add your email. Create it.
3. (Optional) Edit the budget's alerts to also notify the `billing-alerts` SNS topic.

### Step 4 – Create the billing alarm

1. In **us-east-1**, open **CloudWatch** → **Alarms** → **Create alarm**.
2. **Select metric** → **Billing** → **Total Estimated Charge** → tick **USD** → **Select metric**.
3. Threshold: **Greater than 5**. Next.
4. Notification: **In alarm** → `billing-alerts`. Next.
5. Name `estimated-charges-over-5` → **Create alarm**.

### Step 5 – Create the dashboard

1. **CloudWatch** → **Dashboards** → **Create dashboard** → `cost-watch`.
2. Add a **Line** widget → **Billing** → **Total Estimated Charge (USD)**.
3. Add an **Alarm status** widget showing `estimated-charges-over-5`.
4. Save.

### Terraform version (optional)

```hcl
# Billing metrics live in us-east-1
provider "aws" {
  region = "us-east-1"
}

# Topic that emails you (confirm the subscription email)
resource "aws_sns_topic" "billing" {
  name = "billing-alerts"
}

resource "aws_sns_topic_subscription" "email" {
  topic_arn = aws_sns_topic.billing.arn
  protocol  = "email"
  endpoint  = "you@example.com"
}

# Alarm when estimated charges go over $5
resource "aws_cloudwatch_metric_alarm" "charges" {
  alarm_name          = "estimated-charges-over-5"
  namespace           = "AWS/Billing"
  metric_name         = "EstimatedCharges"
  dimensions          = { Currency = "USD" }
  statistic           = "Maximum"
  period              = 21600
  evaluation_periods  = 1
  threshold           = 5
  comparison_operator = "GreaterThanThreshold"
  alarm_actions       = [aws_sns_topic.billing.arn]
}

# $5 monthly budget, alert at 80% actual
resource "aws_budgets_budget" "monthly" {
  name         = "monthly-5"
  budget_type  = "COST"
  limit_amount = "5"
  limit_unit   = "USD"
  time_unit    = "MONTHLY"
  notification {
    comparison_operator       = "GREATER_THAN"
    threshold                 = 80
    threshold_type            = "PERCENTAGE"
    notification_type         = "ACTUAL"
    subscriber_sns_topic_arns = [aws_sns_topic.billing.arn]
  }
}
```

(Sending budget alerts to SNS also needs a topic policy allowing `budgets.amazonaws.com` to publish. <!-- TODO: verify and add topic policy -->)

## Test it

- In SNS, **Publish message** to the topic and check you receive it.

## Clean up

Keep this project – it protects you. If you must remove it: delete the dashboard, alarm, budget and SNS topic.

## What you learned

- Billing metrics live in `us-east-1`.
- Budgets can alert on forecasts; CloudWatch alarms watch metrics.
- SNS is the "messenger" many AWS services use.
