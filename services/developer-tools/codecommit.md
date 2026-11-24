# AWS CodeCommit

**Category:** Developer tools  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ℹ️ **Status note:** CodeCommit stopped taking new customers in July 2024, but AWS reopened it to new customers in November 2025. It is generally available again.

## In one sentence

CodeCommit hosts private Git repositories inside your AWS account.

## Real-life comparison

It's like keeping your company's design documents in a locked filing room inside your own building, rather than at an external storage firm.

## What problem does it solve?

Teams that want code to stay inside AWS (for compliance, or IAM-based access) can host Git there without running their own Git server.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Git** | The standard tool for tracking code changes. |
| **Repository** | A project's code and history. |
| **Pull request** | A request to merge changes, with review. |
| **git-remote-codecommit** | A helper that lets Git use your AWS credentials. |

## How it works (step by step)

1. Create a repository.
2. Clone it using HTTPS (GRC) with your AWS credentials.
3. Push and pull as normal with Git.
4. Use pull requests and approval rules for reviews.

## When to use it

- Code that must stay within AWS, controlled by IAM.

## When NOT to use it (and what to use instead)

- **Open-source projects or rich collaboration features.** → GitHub or GitLab (CodePipeline connects to them).

## Real-world example

**Scenario:** A government contractor must keep source code inside its AWS environment.

**How it helps:** Repos live in CodeCommit, access is via Identity Center roles, and changes trigger CodePipeline.

**What it looks like:**

```
 Developer ──git push──► CodeCommit ──► CodePipeline
```

## Try it yourself

> ⚠️ **Cost warning:** A free allowance of users each month; small test repos cost nothing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **CodeCommit** → **Create repository** → name `demo-repo`.
2. Use **Add file** → **Create file** to add a README in the browser.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create a repository
aws codecommit create-repository --repository-name demo-repo

# Clone it using your AWS credentials (needs: pip install git-remote-codecommit)
git clone codecommit::eu-west-2://demo-repo
```

### Option C – Using Terraform (infrastructure as code)

```hcl
resource "aws_codecommit_repository" "demo" {
  repository_name = "demo-repo"
}
```

### Clean up (delete what you made)

```bash
aws codecommit delete-repository --repository-name demo-repo
```

## How much does it cost?

Free for a small number of active users per month; then per active user, with extra storage and Git requests charged.

Official pricing: <https://aws.amazon.com/codecommit/pricing/>

## Security tips

- Use IAM roles and Identity Center, not long-term Git credentials where possible.

## Common mistakes

- Assuming it's still closed – it reopened to new customers in November 2025.

## Works well with

- [CodePipeline](codepipeline.md), [CodeBuild](codebuild.md).

## Quick check (test yourself)

1. Is CodeCommit open to new customers?
   <details><summary>Answer</summary>Yes, since November 2025.</details>
2. What is a pull request?
   <details><summary>Answer</summary>A request to merge changes, with review.</details>
3. What controls access to repos?
   <details><summary>Answer</summary>IAM.</details>

## Learn more

- [AWS CodeCommit User Guide](https://docs.aws.amazon.com/codecommit/latest/userguide/welcome.html)
- [AWS CodeCommit pricing](https://aws.amazon.com/codecommit/pricing/)
