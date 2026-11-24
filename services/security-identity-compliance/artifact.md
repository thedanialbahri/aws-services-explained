# AWS Artifact

**Category:** Security, identity & compliance  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Artifact is a free portal where you can download AWS's security and compliance reports and accept agreements with AWS.

## Real-life comparison

It's like a restaurant's food hygiene certificate in the window. Customers (or auditors) can see proof that the kitchen passed its inspections.

## What problem does it solve?

Auditors ask "how do you know AWS's data centres are secure?" You can't inspect them yourself. Artifact gives you the official audit reports (like ISO 27001 and SOC 2) on demand.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Compliance report** | Proof from an independent auditor that AWS meets a standard. |
| **SOC 2** | A widely used security audit report. |
| **ISO 27001** | An international information security standard. |
| **Agreement** | A legal document, e.g. a Business Associate Addendum for US health data. |

## How it works (step by step)

1. Open Artifact in the Console.
2. Search for the report you need.
3. Accept the terms and download it.
4. Share it with your auditor as allowed by the terms.

## When to use it

- Audits, security questionnaires, customer due diligence.

## When NOT to use it (and what to use instead)

- **Checking your own account's compliance.** → [AWS Config](../management-governance/config.md), [Security Hub](security-hub.md) or AWS Audit Manager.

## Real-world example

**Scenario:** A payroll company is asked by a big client to prove its cloud provider is secure.

**How it helps:** The company downloads AWS's SOC 2 report from Artifact and sends it with its own answers.

**What it looks like:**

```
 Auditor asks ──► You download AWS report from Artifact ──► Auditor
```

## Try it yourself

> ⚠️ **Cost warning:** Free.

### Option A – Using the AWS Console (clicking in the website)

1. Search for **Artifact** in the Console.
2. Click **View reports**, search for `ISO 27001`.
3. Open the report and read its summary.

### Option B – Using the AWS CLI (typing commands)

```bash
# List available reports
aws artifact list-reports --region us-east-1
```

### Option C – Using Terraform (infrastructure as code)

Not applicable – there's nothing to build.

### Clean up (delete what you made)

Not applicable.

## How much does it cost?

Free.

## Security tips

- Some reports are confidential – follow their sharing terms.

## Common mistakes

- Assuming AWS's reports cover *your* setup. They cover AWS's part of the shared responsibility model only.

## Works well with

- [Security Hub](security-hub.md), [AWS Config](../management-governance/config.md).

## Quick check (test yourself)

1. What can you download from Artifact?
   <details><summary>Answer</summary>AWS's compliance reports and agreements.</details>
2. Do AWS's reports prove your own workloads are compliant?
   <details><summary>Answer</summary>No, only AWS's side of shared responsibility.</details>
3. Is Artifact free?
   <details><summary>Answer</summary>Yes.</details>

## Learn more

- [AWS Artifact User Guide](https://docs.aws.amazon.com/artifact/latest/ug/what-is-aws-artifact.html)
