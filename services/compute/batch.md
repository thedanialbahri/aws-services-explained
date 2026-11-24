# AWS Batch

**Category:** Compute  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

AWS Batch runs large numbers of background jobs from a queue, starting and stopping the computers needed to run them.

## Real-life comparison

Batch is like a print shop. You drop off a pile of print jobs; the shop queues them, starts more printers when it's busy, and turns them off when the pile is done.

## What problem does it solve?

Jobs like rendering video, processing scientific data or running nightly reports may need hundreds of computers for a few hours. Setting up and tearing down that capacity yourself is hard. Batch does it automatically.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Job** | One task, run as a container. |
| **Job definition** | The recipe for a job: container image, CPU, memory. |
| **Job queue** | Where jobs wait their turn. |
| **Compute environment** | The pool of computers (EC2, Spot or Fargate) that runs the jobs. |

## How it works (step by step)

1. You package your task as a container image.
2. You create a **compute environment** and a **job queue**.
3. You write a **job definition**.
4. You submit jobs to the queue.
5. Batch starts computers, runs the jobs and shuts the computers down when finished.

## When to use it

- Large numbers of long-running background jobs.
- Scientific, financial or media processing.

## When NOT to use it (and what to use instead)

- **Short tasks triggered by events.** → [Lambda](lambda.md).
- **Always-on web apps.** → [ECS](../containers/ecs.md) or [EC2](ec2.md).

## Real-world example

**Scenario:** A university genetics lab must analyse 5,000 DNA samples.

**The problem:** On one lab computer, this would take months.

**How Batch helps:** Each sample becomes a job. Batch runs hundreds at once on cheap Spot servers and finishes in a day.

**What it looks like:**

```
 Job queue [5,000 jobs] ──► Compute environment (Spot EC2) ──► results in S3
```

## Try it yourself

> ⚠️ **Cost warning:** Batch is free, but the compute it uses is not. Use Fargate with tiny jobs and delete everything at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Open **AWS Batch** → **Get started** / **Wizard**.
2. Choose **Fargate** orchestration.
3. Follow the wizard to create a compute environment, queue and a job definition using a public image such as `public.ecr.aws/amazonlinux/amazonlinux:latest` with command `echo hello`.
4. Submit the job and watch it move from **SUBMITTED** to **SUCCEEDED**.

### Option B – Using the AWS CLI (typing commands)

```bash
# Submit a job to an existing queue and job definition
aws batch submit-job --job-name hello --job-queue demo-queue --job-definition demo-def
```

### Option C – Using Terraform (infrastructure as code)

Not included here – a Batch setup needs several IAM roles and network resources. See the [Terraform AWS provider docs](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/batch_compute_environment).

### Clean up (delete what you made)

1. Disable and delete the **job queue**.
2. Disable and delete the **compute environment**.
3. Deregister the **job definition**.

## How much does it cost?

No extra charge for Batch. You pay for the EC2, Spot or Fargate resources used while jobs run.

Official pricing: <https://aws.amazon.com/batch/pricing/>

## Security tips

- Give jobs an IAM role with only the permissions they need.
- Run compute in private subnets.

## Common mistakes

- Leaving a minimum number of vCPUs above zero, so servers stay running.

## Works well with

- [S3](../storage/s3.md) – input and output data.
- [ECR](../containers/ecr.md) – stores job container images.

## Quick check (test yourself)

1. What does a job queue do?
   <details><summary>Answer</summary>Holds jobs until computers are free to run them.</details>
2. What format must a Batch job be in?
   <details><summary>Answer</summary>A container image.</details>
3. What's a cheaper compute option for flexible jobs?
   <details><summary>Answer</summary>Spot Instances.</details>

## Learn more

- [AWS Batch User Guide](https://docs.aws.amazon.com/batch/latest/userguide/what-is-batch.html)
- [AWS Batch pricing](https://aws.amazon.com/batch/pricing/)
