# AWS Shield

**Category:** Security, identity & compliance  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Shield protects your AWS-hosted apps from DDoS attacks – floods of fake traffic meant to knock them offline.

## Real-life comparison

A DDoS attack is like thousands of people crowding the entrance of a shop so real customers can't get in. Shield is the crowd-control team that spots the fake crowd and keeps the entrance clear.

## What problem does it solve?

A **DDoS** (Distributed Denial of Service) attack uses thousands of hacked devices to overwhelm a site. Defending alone is almost impossible. Shield Standard protects every AWS customer automatically; Shield Advanced adds extra protection and expert help.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **DDoS** | An attack flooding a service with traffic from many sources. |
| **Shield Standard** | Free, automatic protection against common network attacks. |
| **Shield Advanced** | Paid, extra protection, 24/7 response team and cost protection. |

## How it works (step by step)

1. Shield Standard is on automatically for all accounts.
2. It watches traffic at AWS's edge and filters common attack patterns.
3. With Shield Advanced, you choose resources to protect and get detailed reports and expert help.

## When to use it

- Standard: always (you can't turn it off).
- Advanced: business-critical sites that are likely attack targets.

## When NOT to use it (and what to use instead)

- **Attacks on your app's logic (e.g. SQL injection).** → [WAF](waf.md).

## Real-world example

**Scenario:** An online retailer is threatened with a DDoS attack on Black Friday.

**How it helps:** It subscribes to Shield Advanced for its CloudFront and load balancer, plus WAF rate rules. During the attack, traffic is absorbed at the edge.

**What it looks like:**

```
 Attack traffic ✗ ─┐
 Real customers ✓ ─┼─► AWS edge [Shield] ──► CloudFront ──► ALB ──► App
```

## Try it yourself

> ⚠️ **Cost warning:** Shield Standard is free. Shield Advanced has a large monthly fee and a 1-year commitment – **don't subscribe for learning**.

### Option A – Using the AWS Console (clicking in the website)

1. Open **WAF & Shield** → **Shield** → **Overview** to see what Standard covers. Don't subscribe.

### Option B – Using the AWS CLI (typing commands)

```bash
# Check whether you have a Shield Advanced subscription
aws shield get-subscription-state
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Nothing to clean up.

## How much does it cost?

Standard: free. Advanced: monthly fee per organisation with a 1-year term, plus data transfer charges.

Official pricing: <https://aws.amazon.com/shield/pricing/>

## Security tips

- Put public apps behind CloudFront or Global Accelerator to benefit from edge protection.

## Common mistakes

- Thinking Shield replaces WAF – they solve different problems and work together.

## Works well with

- [WAF](waf.md), [CloudFront](../networking/cloudfront.md), [Route 53](../networking/route-53.md).

## Quick check (test yourself)

1. Do you have to pay for Shield Standard?
   <details><summary>Answer</summary>No, it's free and automatic.</details>
2. What is a DDoS attack?
   <details><summary>Answer</summary>A flood of traffic from many sources meant to knock a service offline.</details>
3. Which service blocks SQL injection?
   <details><summary>Answer</summary>AWS WAF.</details>

## Learn more

- [AWS Shield documentation](https://docs.aws.amazon.com/waf/latest/developerguide/shield-chapter.html)
- [AWS Shield pricing](https://aws.amazon.com/shield/pricing/)
