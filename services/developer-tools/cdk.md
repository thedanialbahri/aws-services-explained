# AWS Cloud Development Kit (CDK)

**Category:** Developer tools  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

The CDK lets you define AWS infrastructure in a programming language like TypeScript or Python, then turns it into CloudFormation and deploys it.

## Real-life comparison

If CloudFormation is writing out every instruction by hand, the CDK is using a recipe app that already knows common steps – "make a secure bucket" – and writes the long version for you.

## What problem does it solve?

CloudFormation YAML gets long and repetitive. With the CDK you use loops, functions and ready-made building blocks (**constructs**) with safe defaults.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Construct** | A building block, e.g. `s3.Bucket`. |
| **Stack** | A deployable group of constructs. |
| **App** | Your CDK project. |
| **Synth** | Turn your code into a CloudFormation template. |
| **Bootstrap** | One-time setup of an account/Region for CDK. |

## How it works (step by step)

1. `cdk init app --language python`.
2. Write constructs in code.
3. `cdk synth` creates the template.
4. `cdk deploy` deploys it through CloudFormation.

## When to use it

- Developers who prefer code to YAML/HCL; AWS-only projects.

## When NOT to use it (and what to use instead)

- **Multi-cloud or teams standardised on Terraform.** → Terraform.

## Real-world example

**Scenario:** A team needs 10 similar SQS queues.

**How it helps:** A loop in the CDK creates them all, consistently.

**What it looks like:**

```python
# Inside a CDK stack: one encrypted, versioned bucket
s3.Bucket(self, "Reports", versioned=True, encryption=s3.BucketEncryption.S3_MANAGED,
          block_public_access=s3.BlockPublicAccess.BLOCK_ALL)
```

## Try it yourself

> ⚠️ **Cost warning:** CDK is free; you pay for resources deployed. `cdk destroy` at the end.

### Option A – Using the AWS Console (clicking in the website)

Not applicable – the CDK is a command-line tool. Results appear in **CloudFormation**.

### Option B – Using the AWS CLI (typing commands)

```bash
# Install the CDK CLI (needs Node.js)
npm install -g aws-cdk

# Create a new Python project
mkdir demo-cdk && cd demo-cdk && cdk init app --language python

# One-time setup for your account/Region, then deploy and remove
cdk bootstrap
cdk deploy
cdk destroy
```

### Option C – Using Terraform (infrastructure as code)

Not applicable – CDK and Terraform are alternatives.

### Clean up (delete what you made)

Run `cdk destroy`. The bootstrap stack (`CDKToolkit`) can be left or deleted in CloudFormation.

## How much does it cost?

Free.

## Security tips

- Review `cdk diff` before deploying, especially IAM changes.

## Common mistakes

- Forgetting to bootstrap the account/Region.

## Works well with

- [CloudFormation](../management-governance/cloudformation.md), [CodePipeline](codepipeline.md).

## Quick check (test yourself)

1. What does `cdk synth` do?
   <details><summary>Answer</summary>Turns your code into a CloudFormation template.</details>
2. What is a construct?
   <details><summary>Answer</summary>A building block for AWS resources.</details>
3. What deploys the CDK app?
   <details><summary>Answer</summary>cdk deploy (via CloudFormation).</details>

## Learn more

- [AWS CDK Developer Guide](https://docs.aws.amazon.com/cdk/v2/guide/home.html)
