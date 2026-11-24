# Amazon CloudWatch

**Category:** Management & governance  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

CloudWatch collects numbers (metrics) and logs from your AWS resources and apps, shows them on dashboards, and raises alarms when something goes wrong.

## Real-life comparison

CloudWatch is like the dashboard in a car. It shows your speed, fuel and engine temperature (metrics), keeps a log of journeys (logs), and flashes a warning light when something needs attention (alarms).

## What problem does it solve?

Without monitoring, you only find out your website is down when customers complain. CloudWatch watches everything all the time and tells you – or fixes things automatically – before users notice.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Metric** | A number measured over time, e.g. CPU % every 5 minutes. |
| **Namespace** | A group of metrics, e.g. `AWS/EC2`. |
| **Dimension** | A label that narrows a metric, e.g. `InstanceId`. |
| **Alarm** | Watches a metric and acts when it crosses a limit. |
| **Log group** | A folder of logs, e.g. `/aws/lambda/my-function`. |
| **Log stream** | One source's logs within a group. |
| **Logs Insights** | A tool for searching logs with queries. |
| **Dashboard** | A page of charts you build. |
| **CloudWatch agent** | Software on a server that sends extra metrics (like memory and disk) and log files. |

## How it works (step by step)

1. AWS services send basic **metrics** automatically (e.g. EC2 CPU, Lambda errors).
2. Apps and services send **logs** to log groups (Lambda does this automatically).
3. You create **alarms**, e.g. "if CPU > 80% for 10 minutes".
4. When an alarm triggers, it can notify you through [SNS](../application-integration/sns.md), scale with Auto Scaling, or stop/reboot a server.
5. You build **dashboards** to see everything at a glance.

## When to use it

- Always – every production system needs monitoring and alarms.
- Troubleshooting with logs.
- Triggering automatic scaling.

## When NOT to use it (and what to use instead)

- **Recording who changed what in your account.** → [CloudTrail](cloudtrail.md).
- **Tracing a single request through many services.** → [X-Ray](../developer-tools/x-ray.md) (or CloudWatch Application Signals).
- **Tracking spending.** → [AWS Budgets](../cost-management/budgets.md).

## Real-world example

**Scenario:** Tom runs a small online booking system on EC2 and Lambda.

**The problem:** One Saturday the site was down for 6 hours before anyone noticed.

**How CloudWatch helps:** Tom creates alarms for high CPU, failed status checks and Lambda errors, all sending emails and texts through SNS. A dashboard shows everything on one page. Next time, he's alerted within minutes.

**What it looks like:**

```
 EC2 / Lambda / RDS ──metrics + logs──► CloudWatch
                                          │
                              Alarm: CPU > 80% for 10 min
                                          │
                                          ▼
                                   SNS topic ──► Email / SMS to Tom
```

## Try it yourself

> ⚠️ **Cost warning:** CloudWatch has an always-free allowance of basic metrics, a few alarms and dashboards, and some log storage. Extra alarms, detailed metrics, custom metrics and large log volumes cost money. Delete test alarms and log groups at the end.

**Before you start:** A running EC2 instance (see [EC2](../compute/ec2.md)) and an SNS topic with your email subscribed (see [SNS](../application-integration/sns.md)).

### Option A – Using the AWS Console (clicking in the website)

1. Open **CloudWatch** → **Alarms** → **All alarms** → **Create alarm**.
2. Click **Select metric** → **EC2** → **Per-Instance Metrics**.
3. Tick **CPUUtilization** for your instance → **Select metric**.
4. **Statistic:** Average. **Period:** 5 minutes.
5. **Threshold:** Greater than **80**. Click **Next**.
6. **Notification:** In alarm → choose your SNS topic. Click **Next**.
7. Name it `high-cpu-demo` → **Next** → **Create alarm**.
8. Go to **Dashboards** → **Create dashboard** → add a **Line** widget showing the same CPU metric.
9. Go to **Logs** → **Log groups** to see logs from any Lambda functions you've run.

### Option B – Using the AWS CLI (typing commands)

```bash
# Alarm when average CPU is over 80% for two 5-minute periods (replace IDs/ARNs)
aws cloudwatch put-metric-alarm --alarm-name high-cpu-demo \
  --namespace AWS/EC2 --metric-name CPUUtilization \
  --dimensions Name=InstanceId,Value=i-0123456789abcdef0 \
  --statistic Average --period 300 --evaluation-periods 2 \
  --threshold 80 --comparison-operator GreaterThanThreshold \
  --alarm-actions arn:aws:sns:eu-west-2:123456789012:alerts

# Show the last 10 minutes of a Lambda function's logs, and keep following
aws logs tail /aws/lambda/hello-function --since 10m --follow
```

### Option C – Using Terraform (infrastructure as code)

Written for the AWS provider `~> 6.0`.

```hcl
# Alarm when average CPU is over 80% for 10 minutes
resource "aws_cloudwatch_metric_alarm" "high_cpu" {
  alarm_name          = "high-cpu-demo"
  namespace           = "AWS/EC2"
  metric_name         = "CPUUtilization"
  dimensions          = { InstanceId = "i-0123456789abcdef0" }
  statistic           = "Average"
  period              = 300
  evaluation_periods  = 2
  threshold           = 80
  comparison_operator = "GreaterThanThreshold"
  alarm_actions       = ["arn:aws:sns:eu-west-2:123456789012:alerts"]
}

# A log group that deletes logs after 14 days (saves money)
resource "aws_cloudwatch_log_group" "app" {
  name              = "/demo/app"
  retention_in_days = 14
}
```

### Clean up (delete what you made)

1. **Alarms** → tick `high-cpu-demo` → **Actions** → **Delete**.
2. **Dashboards** → tick your dashboard → **Delete**.
3. **Log groups** → delete any test log groups.

## How much does it cost?

- **Metrics:** basic AWS metrics are free; detailed and custom metrics are per metric per month.
- **Alarms:** per alarm per month (some free).
- **Logs:** per GB ingested and per GB stored per month.
- **Dashboards:** a few free, then per dashboard per month.

Official pricing: <https://aws.amazon.com/cloudwatch/pricing/>

## Security tips

- Never write passwords or personal data into logs.
- Encrypt sensitive log groups with KMS.
- Limit who can delete log groups.

## Common mistakes

- **Log groups set to "Never expire"** – log storage grows (and costs) forever. Set a retention period.
- **Expecting memory and disk metrics for EC2 by default** – you need the CloudWatch agent.
- **Alarms with no action** – nobody gets told.

## Works well with

- [SNS](../application-integration/sns.md) – sends alarm notifications.
- [Auto Scaling](../compute/auto-scaling.md) – scales on CloudWatch metrics.
- [Lambda](../compute/lambda.md) – logs go to CloudWatch automatically.
- [EventBridge](../application-integration/eventbridge.md) – reacts to alarm state changes.

## Quick check (test yourself)

1. What's the difference between a metric and a log?
   <details><summary>Answer</summary>A metric is a number measured over time; a log is a text record of events.</details>
2. Which EC2 metrics need the CloudWatch agent?
   <details><summary>Answer</summary>Memory and disk usage inside the server.</details>
3. How can an alarm tell you something is wrong?
   <details><summary>Answer</summary>By sending a notification through an SNS topic (email, SMS and so on).</details>

## Learn more

- [Amazon CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
- [Amazon CloudWatch pricing](https://aws.amazon.com/cloudwatch/pricing/)
