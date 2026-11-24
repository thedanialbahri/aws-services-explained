# Developer tools

These services help you **write**, **store**, **build**, **test**, **release** and **troubleshoot** code on AWS.

**Real-life comparison:** Think of a car factory. CodeCommit is the drawing office where designs are kept, CodeBuild is the assembly line, CodeDeploy is the delivery lorry to the showroom, CodePipeline is the conveyor belt joining them all, and X-Ray is the diagnostics tool that finds faults.

## Services in this category

| Service | Level | What it does |
|---------|-------|--------------|
| [AWS CLI](cli.md) | 🟢 | Control AWS by typing commands |
| [AWS CloudShell](cloudshell.md) | 🟢 | A terminal in your browser, already logged in to AWS |
| [AWS SDKs](sdks.md) | 🟡 | Code libraries for using AWS from your own programs |
| [AWS CDK](cdk.md) | 🟡 | Write infrastructure as code using programming languages |
| [AWS CodeCommit](codecommit.md) | 🟡 | Private Git repositories hosted by AWS |
| [AWS CodeBuild](codebuild.md) | 🟡 | Builds and tests your code automatically |
| [AWS CodeDeploy](codedeploy.md) | 🟡 | Releases new versions of your app |
| [AWS CodePipeline](codepipeline.md) | 🟡 | Joins build, test and release steps into one automatic process |
| [AWS CodeArtifact](codeartifact.md) | 🔴 | Stores software packages your code depends on |
| [AWS X-Ray](x-ray.md) | 🔴 | Traces requests through your app to find slow or broken parts |
| [AWS Cloud9](cloud9.md) ⛔ | 🟡 | Browser-based code editor (closed to new customers) |

## CI/CD in one picture

**CI/CD** (continuous integration / continuous delivery) means every code change is automatically built, tested and released.

```
 git push ──► CodePipeline: [Source] ──► [Build & test: CodeBuild] ──► [Deploy: CodeDeploy / ECS / CloudFormation]
```

[← Back to the main index](../../README.md)
