# AWS App Runner

**Category:** Containers  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check) <!-- TODO: verify App Runner's current availability status -->

## In one sentence

App Runner takes your source code or container image and turns it into a running, auto-scaling web app with HTTPS – no servers, clusters or load balancers to set up.

## Real-life comparison

It's like a takeaway kitchen you can rent by the minute, already fitted with ovens, a counter and a delivery driver. You just bring the recipe.

## What problem does it solve?

Even ECS on Fargate needs a cluster, task definitions, a load balancer and networking. App Runner hides all of that for simple web apps and APIs.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Service** | Your running app in App Runner. |
| **Source** | A container image in ECR or code in a GitHub repo. |
| **Auto scaling** | Adds or removes instances with traffic. |

## How it works (step by step)

1. Point App Runner at an image or a code repo.
2. Choose CPU and memory.
3. App Runner builds (if needed), deploys and gives you an HTTPS URL.
4. It scales up with traffic and back down when quiet.

## When to use it

- Simple web apps and APIs, prototypes.

## When NOT to use it (and what to use instead)

- **Complex networking or background workers.** → [ECS](ecs.md).

## Real-world example

**Scenario:** A student builds a Flask app for a hackathon.

**How it helps:** App Runner deploys it from GitHub in minutes with HTTPS.

**What it looks like:**

```
 GitHub repo ──► App Runner (build + run + HTTPS) ──► https://xyz.awsapprunner.com
```

## Try it yourself

> ⚠️ **Cost warning:** Charged for vCPU and memory while active, and memory while idle. Pause or delete the service after testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **App Runner** → **Create service**.
2. Source: **Container registry** → **Amazon ECR Public** → image `public.ecr.aws/aws-containers/hello-app-runner:latest`, port 8000.
3. Create, then open the default domain.

### Option B – Using the AWS CLI (typing commands)

```bash
aws apprunner list-services
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_apprunner_service`.

### Clean up (delete what you made)

1. Open the service → **Actions** → **Delete**.

## How much does it cost?

Per vCPU-second and GB-second while handling requests, plus memory while provisioned but idle, plus build minutes.

Official pricing: <https://aws.amazon.com/apprunner/pricing/>

## Security tips

- Store secrets in Secrets Manager and reference them, not in plain environment variables.

## Common mistakes

- Leaving test services running.

## Works well with

- [ECR](ecr.md), [Secrets Manager](../security-identity-compliance/secrets-manager.md).

## Quick check (test yourself)

1. What sources can App Runner deploy from?
   <details><summary>Answer</summary>Container images (ECR) or source code repositories.</details>
2. Do you set up a load balancer?
   <details><summary>Answer</summary>No.</details>
3. When would you choose ECS instead?
   <details><summary>Answer</summary>For more complex networking or background workers.</details>

## Learn more

- [AWS App Runner Developer Guide](https://docs.aws.amazon.com/apprunner/latest/dg/what-is-apprunner.html)
