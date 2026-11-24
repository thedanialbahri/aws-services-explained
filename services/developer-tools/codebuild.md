# AWS CodeBuild

**Category:** Developer tools  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

CodeBuild compiles your code, runs your tests and produces ready-to-deploy packages, on demand, without a build server to manage.

## Real-life comparison

CodeBuild is like a bakery's oven you rent by the minute. Bring the ingredients (code) and the recipe (`buildspec.yml`); it bakes and hands back the finished loaf (build output).

## What problem does it solve?

Build servers (like a self-hosted Jenkins) need patching and sit idle most of the time. CodeBuild starts a fresh build environment for each build and charges only for build minutes.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Build project** | Settings: where the code is, which environment, which role. |
| **buildspec.yml** | A file in your repo listing the build commands. |
| **Artifact** | The output, e.g. a zip or container image. |
| **Build environment** | The container image (OS and tools) the build runs in. |

## How it works (step by step)

1. Add a `buildspec.yml` to your repo.
2. Create a build project pointing at the repo.
3. Start a build (by hand, from CodePipeline, or on a push).
4. CodeBuild runs the phases (install, pre_build, build, post_build) and saves artifacts and logs.

## When to use it

- Building and testing code automatically; building Docker images.

## When NOT to use it (and what to use instead)

- **You already use GitHub Actions or GitLab CI happily.** Keep them.

## Real-world example

**Scenario:** Every push should run unit tests and build a Docker image.

**How it helps:** CodeBuild runs `pytest`, builds the image and pushes it to ECR.

**What it looks like:**

```yaml
# buildspec.yml – runs tests, then builds the app
version: 0.2
phases:
  install:
    commands:
      - pip install -r requirements.txt
  build:
    commands:
      - pytest
```

## Try it yourself

> ⚠️ **Cost warning:** Free allowance of build minutes per month on small instances; then per build minute.

### Option A – Using the AWS Console (clicking in the website)

1. Open **CodeBuild** → **Create build project**.
2. Source: a public GitHub repo or your CodeCommit repo with a `buildspec.yml`.
3. Environment: managed image, Amazon Linux, standard runtime.
4. Create, then **Start build** and watch the logs.

### Option B – Using the AWS CLI (typing commands)

```bash
# Start a build for an existing project
aws codebuild start-build --project-name demo-build
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_codebuild_project` (needs a service role).

### Clean up (delete what you made)

Delete the build project and its IAM role.

## How much does it cost?

Per build minute, by compute size.

Official pricing: <https://aws.amazon.com/codebuild/pricing/>

## Security tips

- Store secrets in Secrets Manager or Parameter Store and reference them in the buildspec.

## Common mistakes

- Printing secrets in build logs.

## Works well with

- [CodePipeline](codepipeline.md), [ECR](../containers/ecr.md), [CodeCommit](codecommit.md).

## Quick check (test yourself)

1. What file holds the build commands?
   <details><summary>Answer</summary>buildspec.yml</details>
2. How is CodeBuild charged?
   <details><summary>Answer</summary>Per build minute.</details>
3. What is an artifact?
   <details><summary>Answer</summary>The build output, like a zip or image.</details>

## Learn more

- [AWS CodeBuild User Guide](https://docs.aws.amazon.com/codebuild/latest/userguide/welcome.html)
- [CodeBuild pricing](https://aws.amazon.com/codebuild/pricing/)
