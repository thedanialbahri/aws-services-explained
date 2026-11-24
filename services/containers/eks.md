# Amazon Elastic Kubernetes Service (EKS)

**Category:** Containers  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

EKS runs the Kubernetes control plane for you, so you can run containers with standard Kubernetes tools on AWS.

## Real-life comparison

Kubernetes is like a big airport's control tower system used worldwide. EKS is AWS running the control tower for you, while you decide which planes (containers) fly.

## What problem does it solve?

Kubernetes is powerful but complex to install and keep highly available. EKS manages the hardest part (the control plane) and integrates with AWS networking and security.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Kubernetes (K8s)** | Open-source container orchestrator. |
| **Control plane** | The "brain" of the cluster – managed by AWS. |
| **Node** | A server that runs containers. |
| **Pod** | One or more containers running together. |
| **kubectl** | The command-line tool for Kubernetes. |
| **EKS Auto Mode** | AWS also manages the nodes for you. |

## How it works (step by step)

1. Create an EKS cluster.
2. Add compute: managed node groups, Fargate, or Auto Mode.
3. Use `kubectl` and YAML manifests to deploy apps.

## When to use it

- Teams already using Kubernetes, or needing its ecosystem.

## When NOT to use it (and what to use instead)

- **Simpler needs.** → [ECS](ecs.md).

## Real-world example

**Scenario:** A company runs Kubernetes in its data centre and wants to move to AWS.

**How it helps:** EKS runs the same manifests, with AWS managing the control plane.

**What it looks like:**

```
 kubectl ──► EKS control plane (AWS) ──► nodes / Fargate ──► pods
```

## Try it yourself

> ⚠️ **Cost warning:** Each cluster has an hourly charge, plus nodes. Not cheap to leave running – delete within an hour.

### Option A – Using the AWS Console (clicking in the website)

1. Open **EKS** → **Create cluster** → **Quick configuration (with EKS Auto Mode)** and review the steps.

### Option B – Using the AWS CLI (typing commands)

```bash
# Connect kubectl to an existing cluster
aws eks update-kubeconfig --name demo-cluster --region eu-west-2
kubectl get nodes
```

### Option C – Using Terraform (infrastructure as code)

The community `terraform-aws-modules/eks/aws` module is the usual starting point.

### Clean up (delete what you made)

Delete workloads, node groups, then the cluster.

## How much does it cost?

Per cluster-hour plus EC2/Fargate compute and other resources.

Official pricing: <https://aws.amazon.com/eks/pricing/>

## Security tips

- Use EKS Pod Identity or IRSA so pods get IAM roles; keep the API endpoint private if possible.

## Common mistakes

- Choosing Kubernetes for a small app where ECS would be far simpler.

## Works well with

- [ECR](ecr.md), [Fargate](fargate.md), [Elastic Load Balancing](../networking/elastic-load-balancing.md).

## Quick check (test yourself)

1. What part of Kubernetes does EKS manage?
   <details><summary>Answer</summary>The control plane.</details>
2. What is a pod?
   <details><summary>Answer</summary>One or more containers running together.</details>
3. What tool deploys apps to Kubernetes?
   <details><summary>Answer</summary>kubectl.</details>

## Learn more

- [Amazon EKS User Guide](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html)
- [EKS pricing](https://aws.amazon.com/eks/pricing/)
