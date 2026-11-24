# Amazon Timestream

**Category:** Databases  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ℹ️ **Timestream for LiveAnalytics** closed to new customers on 20 June 2025. New projects use **Timestream for InfluxDB**.

## In one sentence

Timestream stores and analyses time-series data – measurements recorded over time, like temperature readings or server CPU.

## Real-life comparison

It's like a weather station's logbook: one reading after another, each with a time. Timestream is built to store those logs and answer "what was the average temperature each hour last week?"

## What problem does it solve?

Sensors and apps produce millions of time-stamped readings. Normal databases get slow and expensive. Time-series databases are designed for this.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Time series** | Values recorded over time. |
| **InfluxDB** | A popular open-source time-series database. |
| **Retention** | How long data is kept. |

## How it works (step by step)

1. Create a Timestream for InfluxDB instance.
2. Devices or apps write readings with timestamps.
3. You query and chart them (e.g. with Grafana).

## When to use it

- IoT sensors, monitoring metrics, industrial telemetry.

## When NOT to use it (and what to use instead)

- **App metrics and logs for AWS resources.** → [CloudWatch](../management-governance/cloudwatch.md).

## Real-world example

**Scenario:** A smart greenhouse records temperature and humidity every 10 seconds.

**How it helps:** Readings go into Timestream for InfluxDB; a Grafana dashboard shows trends.

**What it looks like:**

```
 Sensors ──► IoT Core ──► Timestream for InfluxDB ──► Grafana dashboard
```

## Try it yourself

> ⚠️ **Cost warning:** InfluxDB instances are charged per hour plus storage. Only browse unless you're prepared to pay.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Timestream** → **InfluxDB databases** → **Create** and review the options.

### Option B – Using the AWS CLI (typing commands)

```bash
aws timestream-influxdb list-db-instances
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete any instance you created.

## How much does it cost?

Per instance-hour and per GB-month of storage.

Official pricing: <https://aws.amazon.com/timestream/pricing/>

## Security tips

- Private subnets and strong passwords stored in Secrets Manager.

## Common mistakes

- Keeping raw high-frequency data forever – set retention.

## Works well with

- [IoT Core](../iot/iot-core.md), [Managed Grafana](https://aws.amazon.com/grafana/).

## Quick check (test yourself)

1. What is time-series data?
   <details><summary>Answer</summary>Measurements recorded over time.</details>
2. Which Timestream option is for new customers?
   <details><summary>Answer</summary>Timestream for InfluxDB.</details>
3. Where should AWS resource metrics go?
   <details><summary>Answer</summary>CloudWatch.</details>

## Learn more

- [Amazon Timestream documentation](https://docs.aws.amazon.com/timestream/)
- [Timestream pricing](https://aws.amazon.com/timestream/pricing/)
