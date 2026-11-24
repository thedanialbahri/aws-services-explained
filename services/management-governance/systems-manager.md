# AWS Systems Manager (SSM)

**Category:** Management & governance  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Systems Manager lets you connect to, patch, run commands on and store settings for many servers from one place – without opening SSH or RDP ports.

## Real-life comparison

Systems Manager is like a building's central maintenance office. Instead of visiting every flat to change a light bulb, the office can send instructions to every flat at once, and has a master intercom to talk to any flat without unlocking the front door.

## What problem does it solve?

Logging in to dozens of servers one by one to install updates is slow and needs open admin ports. SSM does it centrally, securely and with a record of what was done.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **SSM Agent** | Software on the server that talks to Systems Manager (pre-installed on many AMIs). |
| **Managed node** | A server Systems Manager can control. |
| **Session Manager** | Opens a terminal to a server in your browser – no SSH keys or open ports. |
| **Run Command** | Runs a command on many servers at once. |
| **Patch Manager** | Installs updates on a schedule. |
| **Parameter Store** | Stores settings and simple secrets. |

## How it works (step by step)

1. The server has the SSM Agent and an **IAM role** with `AmazonSSMManagedInstanceCore`.
2. The agent connects out to Systems Manager.
3. The server appears as a **managed node**.
4. You use Session Manager, Run Command or Patch Manager on it.

## When to use it

- Managing EC2 (and on-premises) servers securely.
- Storing configuration values.

## When NOT to use it (and what to use instead)

- **Storing secrets that need rotation.** → [Secrets Manager](../security-identity-compliance/secrets-manager.md).
- **Building infrastructure.** → [CloudFormation](cloudformation.md) or Terraform.

## Real-world example

**Scenario:** A school IT team runs 20 Windows and Linux servers in AWS.

**The problem:** RDP and SSH were open to the internet, and patching was manual.

**How it helps:** They close all admin ports, connect with Session Manager, and use Patch Manager to update every Sunday at 2am.

**What it looks like:**

```
 Admin's browser ──► Systems Manager ──(agent connects out)──► EC2 servers (no open ports)
```

## Try it yourself

> ⚠️ **Cost warning:** Most core features (Session Manager, Run Command, standard Parameter Store) are free for EC2. Advanced features cost extra.

### Option A – Using the AWS Console (clicking in the website)

1. Create an IAM role for EC2 with the `AmazonSSMManagedInstanceCore` policy.
2. Launch an Amazon Linux EC2 instance with that role and **no** SSH access.
3. Open **Systems Manager** → **Fleet Manager** – your instance appears.
4. Open **Session Manager** → **Start session** → choose the instance.
5. Type `whoami` in the browser terminal.

### Option B – Using the AWS CLI (typing commands)

```bash
# Store a setting in Parameter Store
aws ssm put-parameter --name /demo/site-colour --value blue --type String

# Run a command on every server tagged Environment=dev
aws ssm send-command --document-name AWS-RunShellScript \
  --targets Key=tag:Environment,Values=dev \
  --parameters 'commands=["uptime"]'
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# A setting stored in Parameter Store
resource "aws_ssm_parameter" "colour" {
  name  = "/demo/site-colour"
  type  = "String"
  value = "blue"
}
```

### Clean up (delete what you made)

1. Terminate the test instance.
2. Delete the parameter: `aws ssm delete-parameter --name /demo/site-colour`.

## How much does it cost?

Many features are free; advanced parameters, on-premises advanced instances and some automation have charges.

Official pricing: <https://aws.amazon.com/systems-manager/pricing/>

## Security tips

- Prefer Session Manager to SSH/RDP and close those ports.
- Turn on session logging to S3 or CloudWatch Logs.

## Common mistakes

- Forgetting the IAM role, so the server never appears.

## Works well with

- [EC2](../compute/ec2.md), [Inspector](../security-identity-compliance/inspector.md), [CloudWatch](cloudwatch.md).

## Quick check (test yourself)

1. What does a server need to be managed by SSM?
   <details><summary>Answer</summary>The SSM Agent and an IAM role with the right permissions.</details>
2. How does Session Manager avoid open ports?
   <details><summary>Answer</summary>The agent connects out to Systems Manager.</details>
3. What is Parameter Store?
   <details><summary>Answer</summary>A place to store settings and simple secrets.</details>

## Learn more

- [AWS Systems Manager User Guide](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html)
- [Systems Manager pricing](https://aws.amazon.com/systems-manager/pricing/)
