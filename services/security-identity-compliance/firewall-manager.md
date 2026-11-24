# AWS Firewall Manager

**Category:** Security, identity & compliance  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Firewall Manager sets up and enforces firewall rules (WAF, security groups, Network Firewall and more) across all the accounts in your organisation from one place.

## Real-life comparison

It's like head office sending one security rulebook to every branch and checking each branch follows it, instead of every branch writing its own.

## What problem does it solve?

With dozens of accounts, making sure every public load balancer has the right WAF rules is hard. Firewall Manager applies them automatically, including to new resources.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Security policy** | A rule set Firewall Manager applies, e.g. "every ALB gets this WAF web ACL". |
| **Administrator account** | The account that manages policies. |
| **Scope** | Which accounts and resources a policy covers. |

## How it works (step by step)

1. Set up [Organizations](organizations.md) with all features and [AWS Config](../management-governance/config.md).
2. Choose a Firewall Manager administrator account.
3. Create security policies and choose their scope.
4. Firewall Manager applies them and reports non-compliant resources.

## When to use it

- Organisations with many accounts needing consistent firewall rules.

## When NOT to use it (and what to use instead)

- **One account.** → Configure [WAF](waf.md) and security groups directly.

## Real-world example

**Scenario:** A bank has 60 AWS accounts.

**How it helps:** One policy ensures every internet-facing ALB has the bank's WAF rules, even ones created tomorrow.

**What it looks like:**

```
 Firewall Manager (admin account) ──policy──► every account's ALBs, CloudFront, VPCs
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per policy per Region per month, plus the WAF, Config and other resources it creates. Not suitable for a single learning account.

### Option A – Using the AWS Console (clicking in the website)

Not applicable without an organisation of several accounts.

### Option B – Using the AWS CLI (typing commands)

```bash
# Show the Firewall Manager administrator account (if any)
aws fms get-admin-account
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Nothing to clean up.

## How much does it cost?

Per protection policy per Region per month, plus underlying service charges.

Official pricing: <https://aws.amazon.com/firewall-manager/pricing/>

## Security tips

- Keep the administrator account locked down – it controls firewalls everywhere.

## Common mistakes

- Forgetting AWS Config must be enabled in each account.

## Works well with

- [WAF](waf.md), [Shield](shield.md), [Organizations](organizations.md).

## Quick check (test yourself)

1. What does Firewall Manager need in place?
   <details><summary>Answer</summary>AWS Organizations and AWS Config.</details>
2. Does it apply rules to new resources automatically?
   <details><summary>Answer</summary>Yes, within the policy's scope.</details>
3. Is it useful for a single account?
   <details><summary>Answer</summary>Not really – configure WAF and security groups directly.</details>

## Learn more

- [AWS Firewall Manager documentation](https://docs.aws.amazon.com/waf/latest/developerguide/fms-chapter.html)
- [Firewall Manager pricing](https://aws.amazon.com/firewall-manager/pricing/)
