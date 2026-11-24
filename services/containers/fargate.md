# AWS Fargate

**Category:** Containers  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Fargate runs your containers without you having to create or manage any servers – you just say how much CPU and memory each one needs.

## Real-life comparison

Running containers on EC2 is like owning delivery vans. Fargate is like using a courier: you hand over the parcel and say how big it is; they handle the vans.

## What problem does it solve?

With EC2 you must pick server sizes, patch them and pack containers onto them efficiently. Fargate removes the servers entirely.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Serverless** | You don't manage servers. |
| **Task size** | The vCPU and memory you request. |
| **Fargate Spot** | Cheaper capacity that can be interrupted. |

## How it works (step by step)

1. In [ECS](ecs.md) (or [EKS](eks.md)), choose Fargate as the launch type.
2. Set CPU and memory in the task definition.
3. AWS runs each task in its own isolated environment.

## When to use it

- Most container workloads where you don't need special server control.

## When NOT to use it (and what to use instead)

- **GPUs or special hardware, or very steady heavy loads where EC2 is cheaper.** → ECS/EKS on EC2.

## Real-world example

**Scenario:** A two-person team runs three microservices.

**How it helps:** On Fargate, there are no servers to patch – they only manage their containers.

**What it looks like:**

```
 ECS service ──► Fargate (AWS manages the servers) ──► your containers
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per second for vCPU and memory while tasks run. Stop tasks when finished.

### Option A – Using the AWS Console (clicking in the website)

Follow the Console steps on the [ECS page](ecs.md) – they use Fargate.

### Option B – Using the AWS CLI (typing commands)

```bash
# Run a one-off Fargate task (replace names and IDs)
aws ecs run-task --cluster demo --launch-type FARGATE --task-definition nginx-demo \
  --network-configuration 'awsvpcConfiguration={subnets=[subnet-aaaa1111],securityGroups=[sg-bbbb2222],assignPublicIp=ENABLED}'
```

### Option C – Using Terraform (infrastructure as code)

Set `launch_type = "FARGATE"` and `requires_compatibilities = ["FARGATE"]` in your ECS resources.

### Clean up (delete what you made)

Stop running tasks and delete services as on the [ECS page](ecs.md).

## How much does it cost?

Per vCPU-second and GB-second of memory (and storage above the default). Fargate Spot is cheaper.

Official pricing: <https://aws.amazon.com/fargate/pricing/>

## Security tips

- Each task gets its own isolated environment; still use least-privilege task roles.

## Common mistakes

- Over-sizing CPU and memory "to be safe" and paying for it.

## Works well with

- [ECS](ecs.md), [EKS](eks.md), [ECR](ecr.md).

## Quick check (test yourself)

1. Do you manage servers with Fargate?
   <details><summary>Answer</summary>No.</details>
2. What do you choose for each task?
   <details><summary>Answer</summary>Its CPU and memory.</details>
3. What's a cheaper, interruptible option?
   <details><summary>Answer</summary>Fargate Spot.</details>

## Learn more

- [AWS Fargate documentation](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html)
- [Fargate pricing](https://aws.amazon.com/fargate/pricing/)
