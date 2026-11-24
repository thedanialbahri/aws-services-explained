# AWS Command Line Interface (CLI)

**Category:** Developer tools  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

The AWS CLI lets you control AWS by typing commands in a terminal instead of clicking in the Console.

## Real-life comparison

The Console is like ordering at a restaurant by pointing at pictures on the menu. The CLI is like ordering by saying exactly what you want – quicker once you know the words, and you can write the order down to repeat it any time (a script).

## What problem does it solve?

Clicking is slow and hard to repeat. With the CLI you can do the same task in seconds, save commands in scripts, and automate boring jobs.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Terminal** | A text window where you type commands (Terminal on Mac/Linux, PowerShell on Windows). |
| **Command structure** | `aws <service> <action> --options`, e.g. `aws s3 ls`. |
| **Profile** | A saved set of login details and settings. |
| **Region** | Set per profile or with `--region`. |
| **`--query`** | Filters the output (uses JMESPath). |
| **`--output`** | Output format: `json`, `table`, `text` or `yaml`. |

## How it works (step by step)

1. You install the CLI (version 2).
2. You sign in – ideally with IAM Identity Center (`aws configure sso`).
3. You type a command.
4. The CLI sends a secure request to the AWS API using your credentials.
5. AWS replies, and the CLI prints the result.

## When to use it

- Repeating tasks, scripting, quick checks, automation.
- Learning how AWS really works underneath the Console.

## When NOT to use it (and what to use instead)

- **Building and managing whole environments.** → Infrastructure as code: Terraform, [CloudFormation](../management-governance/cloudformation.md) or [CDK](cdk.md).
- **Inside your own app's code.** → [AWS SDKs](sdks.md).

## Real-world example

**Scenario:** An IT support engineer must check every morning which EC2 servers are stopped.

**The problem:** Clicking through Regions takes 15 minutes.

**How the CLI helps:** One command, saved as a script, lists stopped servers in seconds.

**What it looks like:**

```
 Terminal ──aws ec2 describe-instances──► AWS API ──► table of stopped servers
```

## Try it yourself

> ⚠️ **Cost warning:** The CLI is free. Commands that create resources may cost money – these examples only read information.

### Option A – Using the AWS Console (clicking in the website)

Not applicable – the CLI is the alternative to the Console. To try it with no install, use [CloudShell](cloudshell.md).

### Option B – Using the AWS CLI (typing commands)

1. Install it by following the [official install guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).
2. Check it works:
```bash
# Show the installed version
aws --version

# Set up sign-in through IAM Identity Center (follow the prompts)
aws configure sso

# Check who you're signed in as
aws sts get-caller-identity --profile my-profile

# List your S3 buckets
aws s3 ls --profile my-profile

# List stopped EC2 servers in London as a table
aws ec2 describe-instances --region eu-west-2 --profile my-profile \
  --filters Name=instance-state-name,Values=stopped \
  --query 'Reservations[].Instances[].[InstanceId,InstanceType]' --output table

# Get help for any command
aws ec2 describe-instances help
```

### Option C – Using Terraform (infrastructure as code)

Not applicable – Terraform is a separate tool (it uses the same credentials as the CLI).

### Clean up (delete what you made)

Nothing to clean up – these commands only read information.

## How much does it cost?

Free. You pay only for resources your commands create.

## Security tips

- Use `aws configure sso` (short-lived credentials) instead of long-term access keys.
- Never put access keys in scripts you share or commit to Git.
- Be careful with commands that delete things – there's no "Are you sure?" by default.

## Common mistakes

- Running a command in the wrong Region or with the wrong profile.
- Forgetting `--profile` and using a different account than intended.

## Works well with

- [CloudShell](cloudshell.md), [IAM Identity Center](../security-identity-compliance/iam-identity-center.md), every AWS service.

## Quick check (test yourself)

1. What command shows which identity you're using?
   <details><summary>Answer</summary>aws sts get-caller-identity</details>
2. What's the safest way to sign the CLI in?
   <details><summary>Answer</summary>IAM Identity Center with aws configure sso.</details>
3. How do you get help on a command?
   <details><summary>Answer</summary>Add `help` at the end, e.g. `aws s3 ls help`.</details>

## Learn more

- [AWS CLI User Guide](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)
- [AWS CLI command reference](https://docs.aws.amazon.com/cli/latest/)
