# AWS CloudFormation

**Category:** Management & governance  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

CloudFormation builds and updates AWS resources from a template file, so your infrastructure is written down as code.

## Real-life comparison

CloudFormation is like a flat-pack furniture instruction sheet. Follow the same sheet and you get the same wardrobe every time. Lose the wardrobe? Build it again from the sheet.

## What problem does it solve?

Clicking in the Console is slow, easy to get wrong and hard to repeat. **Infrastructure as code** (IaC) means you describe what you want in a file, keep it in Git, review changes, and rebuild identical environments.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Template** | A YAML or JSON file describing resources. |
| **Stack** | The set of resources created from one template. |
| **Change set** | A preview of what an update will change. |
| **Drift** | When someone changed a resource by hand so it no longer matches the template. |
| **StackSets** | Deploy a stack to many accounts and Regions. |

## How it works (step by step)

1. Write a **template**.
2. Create a **stack** from it.
3. CloudFormation creates resources in the right order.
4. To change things, edit the template and update the stack (preview with a change set).
5. Delete the stack to delete everything it made.

## When to use it

- Repeatable, reviewable infrastructure on AWS.

## When NOT to use it (and what to use instead)

- **You want one tool for several clouds.** → Terraform.
- **You prefer a programming language to YAML.** → [AWS CDK](../developer-tools/cdk.md) (which produces CloudFormation).

## Real-world example

**Scenario:** A team keeps rebuilding test environments by hand, each slightly different.

**How it helps:** One template builds the VPC, servers and database. Each developer creates their own identical stack and deletes it when done.

**What it looks like:**

```
 template.yaml ──► CloudFormation ──► Stack: VPC + EC2 + RDS
```

## Try it yourself

> ⚠️ **Cost warning:** CloudFormation itself is free for AWS resources; you pay for what the stack creates. Delete the stack at the end.

Save this as `bucket.yaml`:

```yaml
# A template that creates one private, versioned S3 bucket
AWSTemplateFormatVersion: "2010-09-09"
Resources:
  DemoBucket:
    Type: AWS::S3::Bucket
    Properties:
      VersioningConfiguration:
        Status: Enabled
      PublicAccessBlockConfiguration:
        BlockPublicAcls: true
        BlockPublicPolicy: true
        IgnorePublicAcls: true
        RestrictPublicBuckets: true
Outputs:
  BucketName:
    Value: !Ref DemoBucket
```

### Option A – Using the AWS Console (clicking in the website)

1. Open **CloudFormation** → **Create stack** → **With new resources**.
2. **Upload a template file** → choose `bucket.yaml` → **Next**.
3. Stack name `demo-stack` → **Next** → **Next** → **Submit**.
4. Watch the **Events** tab, then see the bucket name in **Outputs**.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create (or update) the stack from the template
aws cloudformation deploy --template-file bucket.yaml --stack-name demo-stack
```

### Option C – Using Terraform (infrastructure as code)

Not applicable – Terraform is an alternative to CloudFormation, not used with it.

### Clean up (delete what you made)

1. Empty the bucket if you added files.
2. Delete the stack: Console **Delete**, or `aws cloudformation delete-stack --stack-name demo-stack`.

## How much does it cost?

Free for AWS resource types; third-party resource types have small per-operation charges.

Official pricing: <https://aws.amazon.com/cloudformation/pricing/>

## Security tips

- Never put passwords in templates – reference Secrets Manager instead.
- Use stack policies and termination protection for important stacks.

## Common mistakes

- Editing stack resources by hand, causing drift.

## Works well with

- [CDK](../developer-tools/cdk.md), [CodePipeline](../developer-tools/codepipeline.md), [Service Catalog](service-catalog.md).

## Quick check (test yourself)

1. What is a stack?
   <details><summary>Answer</summary>The resources created from one template.</details>
2. How can you preview changes?
   <details><summary>Answer</summary>With a change set.</details>
3. What is drift?
   <details><summary>Answer</summary>When resources were changed by hand and no longer match the template.</details>

## Learn more

- [AWS CloudFormation User Guide](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
- [CloudFormation pricing](https://aws.amazon.com/cloudformation/pricing/)
