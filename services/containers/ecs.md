# Amazon Elastic Container Service (ECS)

**Category:** Containers  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

ECS runs and manages your containers on AWS, keeping the right number running and replacing any that fail.

## Real-life comparison

ECS is like a port manager. You say "I need 5 containers of this type on ships at all times"; the manager loads them, watches them, and replaces any that fall overboard.

## What problem does it solve?

Running containers by hand on servers doesn't scale: you must decide where each runs, restart crashed ones and roll out new versions. ECS does this for you.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Cluster** | A logical group where your containers run. |
| **Task definition** | The recipe: which image, CPU, memory, ports, environment. |
| **Task** | One running copy of a task definition (one or more containers). |
| **Service** | Keeps a set number of tasks running, often behind a load balancer. |
| **Launch type / capacity provider** | Where tasks run: [Fargate](fargate.md) (serverless) or EC2 instances you manage. |

## How it works (step by step)

1. Push your image to [ECR](ecr.md).
2. Create a **cluster**.
3. Write a **task definition**.
4. Create a **service** with a desired count (e.g. 2) and a load balancer.
5. ECS starts the tasks, health-checks them and replaces failures.
6. To deploy a new version, update the task definition; ECS rolls it out.

## When to use it

- Running containerised web apps and workers on AWS.

## When NOT to use it (and what to use instead)

- **You need Kubernetes specifically.** → [EKS](eks.md).
- **Simplest possible web app hosting.** → [App Runner](app-runner.md).

## Real-world example

**Scenario:** A start-up has a Node.js API in a Docker image.

**How it helps:** An ECS service on Fargate runs 2 tasks behind an ALB, scaling to 10 when busy.

**What it looks like:**

```
 Users ──► ALB ──► ECS service (Fargate) ──► Task ×2–10 ──► RDS
                        ▲
                 image from ECR
```

## Try it yourself

> ⚠️ **Cost warning:** ECS is free; Fargate tasks are charged per vCPU and GB of memory per second. Delete the service and cluster at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Open **ECS** → **Clusters** → **Create cluster** (name `demo`, **Fargate only**).
2. **Task definitions** → **Create new task definition**: Fargate, 0.25 vCPU / 0.5 GB, container image `public.ecr.aws/nginx/nginx:latest`, port 80.
3. In the cluster, **Services** → **Create**: choose the task definition, desired tasks **1**, public IP **on**, security group allowing port 80.
4. When the task is **Running**, open its public IP in a browser – you'll see the nginx welcome page.

### Option B – Using the AWS CLI (typing commands)

```bash
# List clusters and services
aws ecs list-clusters
aws ecs list-services --cluster demo
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_ecs_cluster`, `aws_ecs_task_definition` and `aws_ecs_service`; follow the Console first to understand each part.

### Clean up (delete what you made)

1. Update the service's desired count to 0, then delete the service.
2. Delete the cluster.
3. Deregister the task definition (optional).

## How much does it cost?

ECS itself is free; you pay for Fargate or EC2 capacity, load balancers and logs.

Official pricing: <https://aws.amazon.com/ecs/pricing/>

## Security tips

- Give each task its own **task role** with least privilege.
- Run tasks in private subnets behind a load balancer.
- Scan images with [Inspector](../security-identity-compliance/inspector.md).

## Common mistakes

- Confusing the **task role** (what your app can do) with the **execution role** (what ECS needs to pull images and write logs).

## Works well with

- [ECR](ecr.md), [Fargate](fargate.md), [Elastic Load Balancing](../networking/elastic-load-balancing.md), [CloudWatch](../management-governance/cloudwatch.md).

## Quick check (test yourself)

1. What is a task definition?
   <details><summary>Answer</summary>The recipe for a task: image, CPU, memory, ports and settings.</details>
2. What keeps a set number of tasks running?
   <details><summary>Answer</summary>An ECS service.</details>
3. Does ECS itself cost money?
   <details><summary>Answer</summary>No – you pay for the compute it uses.</details>

## Learn more

- [Amazon ECS Developer Guide](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html)
- [Amazon ECS pricing](https://aws.amazon.com/ecs/pricing/)
