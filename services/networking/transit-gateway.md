# AWS Transit Gateway

**Category:** Networking & content delivery  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Transit Gateway is a central hub that connects many VPCs and office networks together, instead of linking each pair separately.

## Real-life comparison

It's like an airport hub. Instead of direct flights between every pair of small cities (which gets messy fast), everyone flies via the hub.

## What problem does it solve?

Connecting 10 VPCs to each other directly needs 45 separate links (VPC peering). Transit Gateway needs just 10 – one from each VPC to the hub – with central routing rules.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Attachment** | A connection from a VPC, VPN or Direct Connect to the hub. |
| **Transit Gateway route table** | Decides which attachments can reach which. |
| **VPC peering** | The simpler, one-to-one way to link two VPCs. |

## How it works (step by step)

1. You create a Transit Gateway in a Region.
2. You **attach** VPCs, VPNs and Direct Connect gateways.
3. You set route tables in the hub and in each VPC.
4. Traffic flows through the hub to its destination.

## When to use it

- Many VPCs (often across many accounts) that need to talk.
- Sharing one VPN or Direct Connect link with many VPCs.

## When NOT to use it (and what to use instead)

- **Just two or three VPCs.** → VPC peering is simpler and has no hourly charge.

## Real-world example

**Scenario:** A retailer has separate VPCs for web, payments, analytics and shared tools, plus an office VPN.

**The problem:** The peering links have become a tangle.

**How it helps:** Every VPC and the VPN attach to one Transit Gateway, and route tables control who can talk to whom (e.g. analytics can't reach payments).

**What it looks like:**

```
   Web VPC   Payments VPC   Analytics VPC
        \         |         /
         ─── Transit Gateway ─── Office VPN
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per attachment per hour plus per GB processed. Delete everything within an hour of testing.

### Option A – Using the AWS Console (clicking in the website)

1. **VPC** → **Transit gateways** → **Create transit gateway** with default settings.
2. **Transit gateway attachments** → attach two test VPCs (with different CIDR ranges).
3. Add routes in each VPC's route table pointing the other VPC's CIDR to the Transit Gateway.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create a Transit Gateway
aws ec2 create-transit-gateway --description "demo hub"
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# A Transit Gateway with default route table behaviour
resource "aws_ec2_transit_gateway" "hub" {
  description = "demo hub"
}
```

### Clean up (delete what you made)

1. Delete each **attachment**.
2. Delete the **Transit Gateway**.
3. Remove the routes you added.

## How much does it cost?

Per attachment-hour plus per GB of data processed.

Official pricing: <https://aws.amazon.com/transit-gateway/pricing/>

## Security tips

- Use separate route tables to keep sensitive VPCs apart.
- Share the hub across accounts with AWS Resource Access Manager.

## Common mistakes

- Forgetting to add routes in the VPC route tables (not just in the hub).

## Works well with

- [VPC](vpc.md), [Site-to-Site VPN](site-to-site-vpn.md), [Direct Connect](direct-connect.md), [Organizations](../security-identity-compliance/organizations.md).

## Quick check (test yourself)

1. Why use Transit Gateway instead of peering?
   <details><summary>Answer</summary>It scales to many networks with one central hub instead of many pair links.</details>
2. What is an attachment?
   <details><summary>Answer</summary>A connection from a VPC, VPN or Direct Connect to the hub.</details>
3. For two VPCs only, what's simpler?
   <details><summary>Answer</summary>VPC peering.</details>

## Learn more

- [Transit Gateway documentation](https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html)
- [Transit Gateway pricing](https://aws.amazon.com/transit-gateway/pricing/)
