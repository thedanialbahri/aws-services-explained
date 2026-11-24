# Amazon Inspector

**Category:** Security, identity & compliance  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Inspector automatically scans your EC2 servers, container images and Lambda functions for known software weaknesses and risky network exposure.

## Real-life comparison

Inspector is like a mechanic doing a regular MOT check. It goes through a checklist of known problems and tells you what needs fixing, ranked by how dangerous it is.

## What problem does it solve?

Software has security holes (called **CVEs** – publicly listed vulnerabilities) found every day. Checking every server by hand is impossible. Inspector scans continuously and tells you what to patch.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Vulnerability** | A weakness in software that attackers could use. |
| **CVE** | The ID of a publicly known vulnerability. |
| **Finding** | Inspector's report of one problem. |
| **Risk score** | How urgent it is to fix. |

## How it works (step by step)

1. You turn on Inspector.
2. It finds EC2 instances (via the Systems Manager agent or agentless scans), ECR images and Lambda functions.
3. It checks installed software against vulnerability databases.
4. It creates findings with fixes and re-scans when things change.

## When to use it

- Any account running EC2, containers or Lambda.

## When NOT to use it (and what to use instead)

- **Detecting active attacks.** → [GuardDuty](guardduty.md).

## Real-world example

**Scenario:** A team runs 40 EC2 servers.

**The problem:** A serious OpenSSL flaw is announced; which servers are affected?

**How it helps:** Inspector lists exactly which servers have the vulnerable version, and the team patches them with Systems Manager.

**What it looks like:**

```
 EC2 / ECR / Lambda ──scan──► Inspector ──findings──► Security Hub ──► patch with Systems Manager
```

## Try it yourself

> ⚠️ **Cost warning:** New accounts get a free trial period; after that it's charged per instance, image or function scanned. Deactivate it after testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Inspector** → **Get started** → **Activate Inspector**.
2. After some time, open **Findings** → **By instance** to see results for any EC2 instances.

### Option B – Using the AWS CLI (typing commands)

```bash
# Turn on EC2 and ECR scanning for this account
aws inspector2 enable --resource-types EC2 ECR
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# Turn on Inspector for EC2 and ECR in this account
resource "aws_inspector2_enabler" "main" {
  account_ids    = ["123456789012"]
  resource_types = ["EC2", "ECR"]
}
```

### Clean up (delete what you made)

1. **Inspector** → **Account management** → **Deactivate**.

## How much does it cost?

Per EC2 instance per month, per container image scanned, and per Lambda function per month.

Official pricing: <https://aws.amazon.com/inspector/pricing/>

## Security tips

- Fix critical and high findings first.

## Common mistakes

- Turning it on but not patching.

## Works well with

- [Systems Manager](../management-governance/systems-manager.md), [ECR](../containers/ecr.md), [Security Hub](security-hub.md).

## Quick check (test yourself)

1. What is a CVE?
   <details><summary>Answer</summary>The ID of a publicly known software vulnerability.</details>
2. Which resources does Inspector scan?
   <details><summary>Answer</summary>EC2 instances, container images in ECR, and Lambda functions.</details>
3. Does Inspector detect active hackers?
   <details><summary>Answer</summary>No – that's GuardDuty.</details>

## Learn more

- [Amazon Inspector User Guide](https://docs.aws.amazon.com/inspector/latest/user/what-is-inspector.html)
- [Inspector pricing](https://aws.amazon.com/inspector/pricing/)
