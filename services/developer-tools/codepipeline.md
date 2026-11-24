# AWS CodePipeline

**Category:** Developer tools  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

CodePipeline joins the steps of releasing software – get code, build, test, deploy – into one automatic process that runs on every change.

## Real-life comparison

CodePipeline is a factory conveyor belt. A new part (code change) goes on at one end and passes each station (build, test, approve, deploy) automatically.

## What problem does it solve?

Manual releases are slow and inconsistent. A pipeline makes every release follow the same steps.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Pipeline** | The whole process. |
| **Stage** | A group of actions, e.g. Build. |
| **Action** | One task, e.g. run CodeBuild. |
| **Manual approval** | A stage where a person must click Approve. |
| **Connection** | Links to GitHub, GitLab or Bitbucket. |

## How it works (step by step)

1. Create a pipeline with a **source** (GitHub, CodeCommit, S3, ECR).
2. Add **build** (CodeBuild) and **deploy** stages.
3. Every push starts the pipeline automatically.

## When to use it

- CI/CD on AWS.

## When NOT to use it (and what to use instead)

- **Teams already using GitHub Actions end to end.** Keep it simple.

## Real-world example

**Scenario:** A team wants every merge to `main` to reach the test environment automatically, and production after approval.

**What it looks like:**

```
 GitHub (main) ──► Build (CodeBuild) ──► Deploy to test ──► Manual approval ──► Deploy to prod
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per active pipeline per month or per action-minute depending on pipeline type, with a free allowance. Delete test pipelines.

### Option A – Using the AWS Console (clicking in the website)

1. Open **CodePipeline** → **Create pipeline** and follow the wizard with a CodeCommit or GitHub source and a CodeBuild build stage.

### Option B – Using the AWS CLI (typing commands)

```bash
aws codepipeline list-pipelines
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_codepipeline`.

### Clean up (delete what you made)

Delete the pipeline, its artifact S3 bucket and IAM role.

## How much does it cost?

V1 pipelines: per active pipeline per month. V2: per action execution minute. Free allowances apply.

Official pricing: <https://aws.amazon.com/codepipeline/pricing/>

## Security tips

- Use manual approval before production.

## Common mistakes

- Giving the pipeline role admin access.

## Works well with

- [CodeBuild](codebuild.md), [CodeDeploy](codedeploy.md), [CloudFormation](../management-governance/cloudformation.md).

## Quick check (test yourself)

1. What is a stage?
   <details><summary>Answer</summary>A group of actions in a pipeline, like Build.</details>
2. How do you require a human sign-off?
   <details><summary>Answer</summary>Add a manual approval action.</details>
3. What starts a pipeline?
   <details><summary>Answer</summary>A change in the source, e.g. a git push.</details>

## Learn more

- [AWS CodePipeline User Guide](https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html)
