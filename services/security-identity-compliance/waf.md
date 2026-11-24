# AWS WAF (Web Application Firewall)

**Category:** Security, identity & compliance  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

AWS WAF inspects web requests to your site or API and blocks ones that look like attacks, before they reach your app.

## Real-life comparison

WAF is like a bouncer at a club door with a list of rules: no one from the banned list, no one acting suspiciously, and no more than a certain number of people from one group at once.

## What problem does it solve?

Websites get attacked with tricks like **SQL injection** (sneaking database commands into forms) and floods of requests from bots. WAF filters these out using rules you choose or ready-made rule sets.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Web ACL** | Your set of WAF rules. |
| **Rule** | One check, e.g. "block requests from this IP list". |
| **Managed rule group** | Ready-made rules maintained by AWS or sellers. |
| **Rate-based rule** | Blocks an IP that sends too many requests. |

## How it works (step by step)

1. You create a **web ACL**.
2. You add rules (often AWS managed rule groups first).
3. You attach it to CloudFront, an ALB, API Gateway or Cognito.
4. Each request is checked; matching requests are allowed, blocked or counted.

## When to use it

- Any public website or API.

## When NOT to use it (and what to use instead)

- **Network-level firewalls for a VPC.** → Security groups, network ACLs or AWS Network Firewall.
- **Large DDoS floods.** → [Shield](shield.md) (works together with WAF).

## Real-world example

**Scenario:** A ticketing site's login page is hit by bots trying stolen passwords.

**How it helps:** A web ACL on CloudFront uses AWS's managed common rules plus a rate-based rule limiting each IP to a sensible number of login attempts.

**What it looks like:**

```
 Visitors + bots ──► CloudFront [WAF web ACL] ──(clean traffic)──► ALB ──► App
                              └── blocked ✗
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per web ACL per month, per rule per month and per million requests. Delete the web ACL at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Open **WAF & Shield** → **Web ACLs** → **Create web ACL**.
2. Choose your Region (or **Global (CloudFront)**) and an existing resource.
3. **Add rules** → **Add managed rule groups** → turn on **Core rule set**.
4. Set the default action to **Allow** → create.
5. Check **Overview** later to see sampled requests.

### Option B – Using the AWS CLI (typing commands)

```bash
# List web ACLs for regional resources (ALB, API Gateway)
aws wafv2 list-web-acls --scope REGIONAL
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_wafv2_web_acl`; the rule blocks are long, so try the Console first.

### Clean up (delete what you made)

1. Remove the web ACL from its resource.
2. Delete the web ACL.

## How much does it cost?

Per web ACL per month, per rule per month, and per million requests inspected. Some managed rule groups cost extra.

Official pricing: <https://aws.amazon.com/waf/pricing/>

## Security tips

- Start rules in **Count** mode to check they don't block real users, then switch to Block.

## Common mistakes

- Blocking legitimate users with overly strict rules.

## Works well with

- [CloudFront](../networking/cloudfront.md), [Elastic Load Balancing](../networking/elastic-load-balancing.md), [Shield](shield.md), [Firewall Manager](firewall-manager.md).

## Quick check (test yourself)

1. What is a web ACL?
   <details><summary>Answer</summary>A set of WAF rules attached to a resource.</details>
2. Which rule type stops an IP sending too many requests?
   <details><summary>Answer</summary>A rate-based rule.</details>
3. Why test rules in Count mode first?
   <details><summary>Answer</summary>To make sure they don't block real users.</details>

## Learn more

- [AWS WAF Developer Guide](https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html)
- [AWS WAF pricing](https://aws.amazon.com/waf/pricing/)
