# AWS CodeDeploy

**Category:** Developer tools  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

CodeDeploy rolls out new versions of your app to EC2 servers, on-premises servers, Lambda or ECS, safely and automatically.

## Real-life comparison

It's like a shop refit done section by section: close one aisle, refit it, reopen it, then move to the next – so the shop never fully closes. If something goes wrong, put the old shelves back.

## What problem does it solve?

Copying new code to servers by hand is error-prone and causes downtime. CodeDeploy deploys in controlled steps and can roll back automatically.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Application** | What you're deploying. |
| **Deployment group** | The servers or service to deploy to. |
| **appspec.yml** | Instructions for the deployment (files to copy, scripts to run). |
| **In-place / blue/green** | Update existing servers / switch to a new set. |
| **Rollback** | Return to the previous version. |

## How it works (step by step)

1. Install the CodeDeploy agent on servers (not needed for Lambda/ECS).
2. Add `appspec.yml` to your app bundle.
3. Create an application and deployment group.
4. Start a deployment; CodeDeploy follows your chosen strategy and checks health.

## When to use it

- Releasing to EC2 or on-premises servers; traffic shifting for Lambda/ECS.

## When NOT to use it (and what to use instead)

- **Simple container services.** ECS rolling updates may be enough.

## Real-world example

**Scenario:** A company updates its web app on 6 EC2 servers.

**How it helps:** CodeDeploy updates 2 servers at a time and rolls back if health checks fail.

**What it looks like:**

```
 New version ──► CodeDeploy ──► servers 1–2 ✓ ──► servers 3–4 ✓ ──► servers 5–6 ✓
```

## Try it yourself

> ⚠️ **Cost warning:** Free for EC2, Lambda and ECS; small per-update charge for on-premises servers.

### Option A – Using the AWS Console (clicking in the website)

1. Open **CodeDeploy** → **Applications** → **Create application** and explore the options.

### Option B – Using the AWS CLI (typing commands)

```bash
aws deploy list-applications
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_codedeploy_app` and `aws_codedeploy_deployment_group`.

### Clean up (delete what you made)

Delete the application.

## How much does it cost?

Free for EC2/Lambda/ECS; per on-premises instance update.

Official pricing: <https://aws.amazon.com/codedeploy/pricing/>

## Security tips

- Give servers an instance role that can read only the deployment bucket.

## Common mistakes

- Missing or wrong `appspec.yml`.

## Works well with

- [CodePipeline](codepipeline.md), [EC2](../compute/ec2.md), [Lambda](../compute/lambda.md).

## Quick check (test yourself)

1. What is blue/green deployment?
   <details><summary>Answer</summary>Deploying to a new set of servers and switching traffic over.</details>
2. Which file describes the deployment?
   <details><summary>Answer</summary>appspec.yml</details>
3. Can it roll back automatically?
   <details><summary>Answer</summary>Yes.</details>

## Learn more

- [AWS CodeDeploy User Guide](https://docs.aws.amazon.com/codedeploy/latest/userguide/welcome.html)
