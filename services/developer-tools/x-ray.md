# AWS X-Ray

**Category:** Developer tools  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

X-Ray traces each request as it travels through your app's services, showing where it slows down or fails.

## Real-life comparison

It's like tracking a parcel: you see every depot it passed through and how long it waited at each, so you know exactly where the delay happened.

## What problem does it solve?

In apps made of many services (API Gateway → Lambda → DynamoDB), finding the slow part is hard. X-Ray shows a map and timeline for each request.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Trace** | The full journey of one request. |
| **Segment** | One service's part of the trace. |
| **Service map** | A diagram of services and their health. |
| **OpenTelemetry** | An open standard for traces (AWS recommends ADOT/OTel for new work). |

## How it works (step by step)

1. Turn on tracing (e.g. a checkbox in Lambda or API Gateway) or add instrumentation.
2. Requests are recorded as traces.
3. View the service map and traces in the CloudWatch console.

## When to use it

- Debugging slow or failing requests in distributed apps.

## When NOT to use it (and what to use instead)

- **Simple single-server apps.** → [CloudWatch](../management-governance/cloudwatch.md) logs and metrics.

## Real-world example

**Scenario:** A checkout API sometimes takes 5 seconds.

**How it helps:** Traces show a slow call to a third-party payment API, not the database.

**What it looks like:**

```
 API Gateway (20ms) ──► Lambda (40ms) ──► Payment API (4,800ms!) ──► DynamoDB (8ms)
```

## Try it yourself

> ⚠️ **Cost warning:** Free allowance of traces each month, then per million traces.

### Option A – Using the AWS Console (clicking in the website)

1. Open your Lambda function → **Configuration** → **Monitoring and operations tools** → turn on **Active tracing**.
2. Invoke it a few times.
3. Open **CloudWatch** → **Traces** / **Service map**.

### Option B – Using the AWS CLI (typing commands)

```bash
# Turn on active tracing for a function
aws lambda update-function-configuration --function-name hello-function --tracing-config Mode=Active
```

### Option C – Using Terraform (infrastructure as code)

Add `tracing_config { mode = "Active" }` to an `aws_lambda_function`.

### Clean up (delete what you made)

Set tracing back to `PassThrough`, or delete the function.

## How much does it cost?

Per million traces recorded and retrieved, above the free allowance.

Official pricing: <https://aws.amazon.com/xray/pricing/>

## Security tips

- Don't put personal data in trace annotations.

## Common mistakes

- Tracing 100% of requests at high volume – use sampling.

## Works well with

- [Lambda](../compute/lambda.md), [API Gateway](../networking/api-gateway.md), [CloudWatch](../management-governance/cloudwatch.md).

## Quick check (test yourself)

1. What is a trace?
   <details><summary>Answer</summary>The full journey of one request through your services.</details>
2. How do you turn on tracing for Lambda?
   <details><summary>Answer</summary>Enable active tracing.</details>
3. Why use sampling?
   <details><summary>Answer</summary>To keep costs down at high volume.</details>

## Learn more

- [AWS X-Ray Developer Guide](https://docs.aws.amazon.com/xray/latest/devguide/aws-xray.html)
