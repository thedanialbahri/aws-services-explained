# AWS Site-to-Site VPN

**Category:** Networking & content delivery  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Site-to-Site VPN creates an encrypted tunnel over the internet between your office network and your AWS VPC.

## Real-life comparison

It's like a private, armoured tunnel built under a public road. The road (the internet) is shared, but nobody can see or touch what travels through your tunnel.

## What problem does it solve?

Office servers often need to talk to servers in AWS – for example, during a migration. Sending that traffic over the open internet unprotected isn't safe. A VPN encrypts it, and it can be set up in hours (unlike a private cable).

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **VPN** | Virtual Private Network – an encrypted connection over a public network. |
| **Customer gateway** | Your office router or firewall, as described to AWS. |
| **Virtual private gateway** | The VPN end point on the AWS side, attached to your VPC. |
| **Tunnel** | Each VPN connection has two tunnels, for resilience. |
| **IPsec** | The standard used to encrypt the tunnel. |

## How it works (step by step)

1. You create a **customer gateway** with your office router's public IP.
2. You create a **virtual private gateway** (or use a [Transit Gateway](transit-gateway.md)) and attach it to your VPC.
3. You create the **VPN connection** and download the configuration for your router.
4. Your network team applies it to the office router. Two tunnels come up.
5. You update route tables so traffic for each side goes through the VPN.

## When to use it

- Connecting an office to AWS quickly and cheaply.
- A backup link for [Direct Connect](direct-connect.md).

## When NOT to use it (and what to use instead)

- **Very high, steady bandwidth or consistent speed needed.** → [Direct Connect](direct-connect.md).
- **Individual staff connecting from laptops.** → AWS Client VPN (a different service).

## Real-world example

**Scenario:** A solicitors' firm is moving its file server into AWS bit by bit.

**The problem:** Office PCs still need to reach servers in AWS securely.

**How it helps:** A Site-to-Site VPN joins the office network to the VPC, so staff reach AWS servers by private IP as if they were in the office.

**What it looks like:**

```
 Office network ── router ══ encrypted tunnels (internet) ══ VPN gateway ── VPC
```

## Try it yourself

> ⚠️ **Cost warning:** VPN connections are charged per hour while they exist, even if unused. You also need a compatible router at the other end. Only build one if you can test it, and delete it straight after.

### Option A – Using the AWS Console (clicking in the website)

1. Open **VPC** → **Site-to-Site VPN connections** and read the **Create VPN connection** form. Cancel without creating unless you have a router to connect.

### Option B – Using the AWS CLI (typing commands)

```bash
# List VPN connections and tunnel status
aws ec2 describe-vpn-connections \
  --query 'VpnConnections[].[VpnConnectionId,State,VgwTelemetry[].Status]'
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for a solo learner without an office router.

### Clean up (delete what you made)

1. Delete the **VPN connection**.
2. Detach and delete the **virtual private gateway**.
3. Delete the **customer gateway**.

## How much does it cost?

Per VPN connection-hour, plus data transfer out of AWS.

Official pricing: <https://aws.amazon.com/vpn/pricing/>

## Security tips

- Use strong, modern encryption settings from the downloaded config.
- Only route the networks that really need to talk to each other.

## Common mistakes

- Overlapping IP ranges between the office and the VPC.
- Configuring only one of the two tunnels.

## Works well with

- [VPC](vpc.md), [Transit Gateway](transit-gateway.md), [Direct Connect](direct-connect.md).

## Quick check (test yourself)

1. What does a Site-to-Site VPN travel over?
   <details><summary>Answer</summary>The public internet, inside encrypted tunnels.</details>
2. How many tunnels does each connection have?
   <details><summary>Answer</summary>Two.</details>
3. What's the private-cable alternative?
   <details><summary>Answer</summary>AWS Direct Connect.</details>

## Learn more

- [AWS Site-to-Site VPN User Guide](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html)
- [AWS VPN pricing](https://aws.amazon.com/vpn/pricing/)
