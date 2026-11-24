# Amazon Elastic Container Registry (ECR)

**Category:** Containers  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

ECR is a private, secure place to store your container images so ECS, EKS and other services can pull them.

## Real-life comparison

ECR is like a warehouse for your shipping containers' blueprints. When a port needs a container, it collects the blueprint from your warehouse.

## What problem does it solve?

Images need a safe home that your AWS services can reach quickly, with access control and vulnerability scanning.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Repository** | A folder for one image's versions. |
| **Tag** | A label for a version, e.g. `v1.2`. |
| **Push / pull** | Upload / download an image. |
| **Lifecycle policy** | Automatically deletes old images. |
| **Image scanning** | Checks images for known vulnerabilities. |

## How it works (step by step)

1. Create a repository.
2. Log Docker in to ECR.
3. Tag and push your image.
4. ECS/EKS pull it when starting containers.

## When to use it

- Storing images for any AWS container service.

## When NOT to use it (and what to use instead)

- **Public, open-source images for everyone.** ECR Public or Docker Hub.

## Real-world example

**Scenario:** A team builds a new image on every code change.

**How it helps:** CodeBuild pushes images to ECR; a lifecycle policy keeps only the last 20.

**What it looks like:**

```
 CodeBuild ──push──► ECR repo "api" ──pull──► ECS
```

## Try it yourself

> ⚠️ **Cost warning:** Small free storage allowance for new accounts; then per GB-month. Delete test repositories.

### Option A – Using the AWS Console (clicking in the website)

1. Open **ECR** → **Create repository** → name `demo-app`, private.
2. Click **View push commands** to see the exact commands for your computer.

### Option B – Using the AWS CLI (typing commands)

```bash
# Log Docker in to your private registry (replace account ID)
aws ecr get-login-password --region eu-west-2 | \
  docker login --username AWS --password-stdin 123456789012.dkr.ecr.eu-west-2.amazonaws.com

# Tag a local image and push it
docker tag demo-app:latest 123456789012.dkr.ecr.eu-west-2.amazonaws.com/demo-app:v1
docker push 123456789012.dkr.ecr.eu-west-2.amazonaws.com/demo-app:v1
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# A private repository that scans images when they're pushed
resource "aws_ecr_repository" "app" {
  name                 = "demo-app"
  image_tag_mutability = "IMMUTABLE"
  image_scanning_configuration {
    scan_on_push = true
  }
}
```

### Clean up (delete what you made)

1. **ECR** → tick `demo-app` → **Delete** (type `delete`).

## How much does it cost?

Per GB-month stored plus data transfer out.

Official pricing: <https://aws.amazon.com/ecr/pricing/>

## Security tips

- Turn on scanning and immutable tags.

## Common mistakes

- Never deleting old images – use lifecycle policies.

## Works well with

- [ECS](ecs.md), [EKS](eks.md), [CodeBuild](../developer-tools/codebuild.md), [Inspector](../security-identity-compliance/inspector.md).

## Quick check (test yourself)

1. What is a repository in ECR?
   <details><summary>Answer</summary>A folder holding versions of one image.</details>
2. How do you remove old images automatically?
   <details><summary>Answer</summary>A lifecycle policy.</details>
3. What does "immutable tags" mean?
   <details><summary>Answer</summary>A tag can't be overwritten with a different image.</details>

## Learn more

- [Amazon ECR User Guide](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html)
- [ECR pricing](https://aws.amazon.com/ecr/pricing/)
