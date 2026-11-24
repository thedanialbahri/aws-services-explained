# AWS App Runner

**Category:** Containers  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ⛔ **No longer available to new customers.** App Runner closed to new customers on 30 April 2026. Existing customers can keep using it, but no new features are planned. AWS recommends **Amazon ECS Express Mode** instead – see [ECS](ecs.md).

## In one sentence

App Runner takes your source code or container image and turns it into a running, auto-scaling web app with HTTPS – no servers, clusters or load balancers to set up.

## Real-life comparison

It's like a takeaway kitchen you can rent by the minute, already fitted with ovens, a counter and a delivery driver. You just bring the recipe.

## What problem does it solve?

Even ECS on Fargate needs a cluster, task definitions, a load balancer and networking. App Runner hid all of that for simple web apps and APIs. ECS Express Mode now aims to do the same job inside ECS.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Service** | Your running app in App Runner. |
| **Source** | A container image in ECR or code in a GitHub repo. |
| **Maintenance mode** | AWS keeps the service running and secure, but takes no new customers and adds no features. |
| **ECS Express Mode** | AWS's recommended replacement: a simpler way to run a web container on ECS. |

## How it works (step by step)

1. Point App Runner at an image or a code repo.
2. Choose CPU and memory.
3. App Runner builds (if needed), deploys and gives you an HTTPS URL.
4. It scales up with traffic and back down when quiet.

## When to use it

- Only if your account already uses App Runner.

## When NOT to use it (and what to use instead)

- **Any new project.** → [ECS](ecs.md) Express Mode, or [ECS on Fargate](fargate.md).
- **Complex networking or background workers.** → [ECS](ecs.md).

## Real-world example

**Scenario:** A student built a Flask app for a hackathon in 2025 and deployed it with App Runner.

**Today:** The app keeps running, but a new student starting now would deploy the same container with ECS Express Mode.

**What it looks like:**

```
 (existing) GitHub repo ──► App Runner ──► https://xyz.awsapprunner.com
 (new)      Container image ──► ECS Express Mode ──► HTTPS URL
```

## Try it yourself

> ⚠️ **Cost warning:** Not applicable for new customers.

### Option A – Using the AWS Console (clicking in the website)

Not applicable – closed to new customers. Try the [ECS page](ecs.md) instead.

### Option B – Using the AWS CLI (typing commands)

```bash
# Existing customers: list your App Runner services
aws apprunner list-services
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for new customers.

### Clean up (delete what you made)

Existing customers: open the service → **Actions** → **Delete** for any service you no longer need.

## How much does it cost?

Existing customers pay per vCPU-second and GB-second while handling requests, plus memory while idle, plus build minutes.

Official pricing: <https://aws.amazon.com/apprunner/pricing/>

## Security tips

- Store secrets in Secrets Manager and reference them, not in plain environment variables.

## Common mistakes

- Following older tutorials that start with "Create an App Runner service".

## Works well with

- [ECR](ecr.md), [ECS](ecs.md).

## Quick check (test yourself)

1. Can new customers use App Runner?
   <details><summary>Answer</summary>No – it closed to new customers on 30 April 2026.</details>
2. What does AWS recommend instead?
   <details><summary>Answer</summary>Amazon ECS Express Mode.</details>
3. What is maintenance mode?
   <details><summary>Answer</summary>The service keeps running for existing customers, but takes no new customers and gets no new features.</details>

## Learn more

- [AWS App Runner availability change](https://docs.aws.amazon.com/apprunner/latest/dg/apprunner-availability-change.html)
