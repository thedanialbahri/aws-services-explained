# AWS Direct Connect

**Category:** Networking & content delivery  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Direct Connect is a private network connection from your building or data centre to AWS that doesn't go over the public internet.

## Real-life comparison

If a VPN is an armoured tunnel under a public road, Direct Connect is your own private road. Nobody else uses it, so traffic is steady and predictable.

## What problem does it solve?

Big companies move huge amounts of data to and from AWS. The internet can be slow, unpredictable and costly for that. Direct Connect gives a dedicated, consistent link.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Direct Connect location** | A data centre where AWS's network meets other networks. |
| **Dedicated connection** | A physical port just for you (e.g. 1, 10 or 100 Gbps). |
| **Hosted connection** | A share of a connection provided by an AWS partner. |
| **Virtual interface (VIF)** | A logical connection on top of the link (private to a VPC, public to AWS services, or transit). |

## How it works (step by step)

1. You choose a Direct Connect location and a speed.
2. You (or a partner) run a cable from your network to that location.
3. AWS connects it to its network.
4. You create **virtual interfaces** to reach your VPCs or public AWS services.

## When to use it

- Large, steady data transfers.
- Predictable network performance for hybrid systems.

## When NOT to use it (and what to use instead)

- **Small offices or quick setups.** → [Site-to-Site VPN](site-to-site-vpn.md) (hours to set up, not weeks).

## Real-world example

**Scenario:** A bank runs core systems in its own data centre and analytics in AWS.

**The problem:** Nightly data copies over the internet are slow and inconsistent.

**How it helps:** A 10 Gbps Direct Connect link gives a steady private path, with a VPN as backup.

**What it looks like:**

```
 Bank data centre ══ private fibre ══ Direct Connect location ══ AWS Region (VPCs)
                 └─ VPN over internet (backup) ─┘
```

## Try it yourself

> ⚠️ **Cost warning:** Direct Connect involves port-hour charges and usually a telecoms contract. Not suitable for personal learning.

### Option A – Using the AWS Console (clicking in the website)

Not applicable – needs a physical connection.

### Option B – Using the AWS CLI (typing commands)

```bash
# List Direct Connect locations in this Region (free to run)
aws directconnect describe-locations --query 'locations[].locationName'
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Nothing to clean up if you only listed locations.

## How much does it cost?

Per port-hour (depends on speed) plus data transfer out per GB. Partners charge for their part of the connection.

Official pricing: <https://aws.amazon.com/directconnect/pricing/>

## Security tips

- Direct Connect is private but **not encrypted by default**. Add MACsec (on supported ports) or run a VPN over it if you need encryption.

## Common mistakes

- Having only one connection – plan a backup (a second link or a VPN).

## Works well with

- [Transit Gateway](transit-gateway.md), [VPC](vpc.md), [Site-to-Site VPN](site-to-site-vpn.md).

## Quick check (test yourself)

1. Does Direct Connect use the public internet?
   <details><summary>Answer</summary>No, it's a private connection.</details>
2. Is it encrypted by default?
   <details><summary>Answer</summary>No. Use MACsec or a VPN on top if needed.</details>
3. What's a quicker, cheaper alternative?
   <details><summary>Answer</summary>Site-to-Site VPN.</details>

## Learn more

- [AWS Direct Connect User Guide](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html)
- [AWS Direct Connect pricing](https://aws.amazon.com/directconnect/pricing/)
