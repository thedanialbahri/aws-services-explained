# AWS Global Accelerator

**Category:** Networking & content delivery  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Global Accelerator gives your app two fixed IP addresses and carries users' traffic over AWS's private global network to the nearest healthy copy of your app.

## Real-life comparison

It's like getting on a motorway at the nearest junction instead of using slow local roads all the way. Users join AWS's fast network close to home.

## What problem does it solve?

Traffic crossing the public internet can take slow or unreliable routes. Global Accelerator gets users onto AWS's network quickly and can switch Regions in seconds if one fails – without DNS caching delays.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Accelerator** | Your Global Accelerator setup. |
| **Static anycast IPs** | Two fixed IP addresses announced from many locations at once. |
| **Endpoint group** | Your app's endpoints in one Region (load balancers, EC2, Elastic IPs). |
| **Listener** | The ports and protocol (TCP/UDP) to accept. |

## How it works (step by step)

1. You create an accelerator and get two static IPs.
2. You add a **listener** and **endpoint groups** in one or more Regions.
3. Users connect to the IPs; they enter AWS at the nearest edge location.
4. AWS sends traffic to the closest healthy endpoint.

## When to use it

- Games, voice and other TCP/UDP apps needing steady performance.
- Apps that need fixed IPs for customers' firewall allow-lists.
- Fast failover between Regions.

## When NOT to use it (and what to use instead)

- **Caching websites and files.** → [CloudFront](cloudfront.md).

## Real-world example

**Scenario:** An online multiplayer game runs in London and Virginia.

**The problem:** Players have lag and the game uses UDP, which CloudFront doesn't handle.

**How it helps:** Global Accelerator sends each player to the nearest Region over AWS's network and fails over automatically.

**What it looks like:**

```
 Players ──► 2 static IPs ──► nearest edge ══ AWS network ══► NLB (London) / NLB (Virginia)
```

## Try it yourself

> ⚠️ **Cost warning:** A fixed hourly fee per accelerator plus data transfer charges. Delete it soon after testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Global Accelerator** (it's managed from `us-west-2`) → **Create accelerator**.
2. Add a TCP listener on port 80 and an endpoint group pointing to an existing load balancer.

### Option B – Using the AWS CLI (typing commands)

```bash
# Global Accelerator's API lives in us-west-2
aws globalaccelerator list-accelerators --region us-west-2
```

### Option C – Using Terraform (infrastructure as code)

Not included – the setup is usually done once by hand for testing.

### Clean up (delete what you made)

1. Disable the accelerator and wait.
2. Delete endpoint groups, listeners, then the accelerator.

## How much does it cost?

A fixed fee per accelerator-hour plus a data transfer premium per GB.

Official pricing: <https://aws.amazon.com/global-accelerator/pricing/>

## Security tips

- [AWS Shield](../security-identity-compliance/shield.md) Standard protects accelerators against common DDoS attacks.

## Common mistakes

- Using it for cacheable web content where CloudFront is cheaper.

## Works well with

- [Elastic Load Balancing](elastic-load-balancing.md), [EC2](../compute/ec2.md).

## Quick check (test yourself)

1. How many static IPs does an accelerator give you?
   <details><summary>Answer</summary>Two.</details>
2. Can it handle UDP traffic?
   <details><summary>Answer</summary>Yes.</details>
3. For caching images worldwide, which service is better?
   <details><summary>Answer</summary>CloudFront.</details>

## Learn more

- [AWS Global Accelerator Developer Guide](https://docs.aws.amazon.com/global-accelerator/latest/dg/what-is-global-accelerator.html)
- [AWS Global Accelerator pricing](https://aws.amazon.com/global-accelerator/pricing/)
