# AWS PrivateLink

**Category:** Networking & content delivery  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

PrivateLink lets resources in your VPC reach AWS services or other companies' services through private addresses, without going over the internet.

## Real-life comparison

It's like a private internal door from your flat straight into the building's gym, so you don't have to go outside onto the street to get there.

## What problem does it solve?

Servers in a private subnet normally need a NAT gateway and the internet to reach services like S3 APIs or a partner's software. PrivateLink gives them a private door instead – more secure, and often cheaper.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **VPC endpoint** | The private door inside your VPC. |
| **Interface endpoint** | A network card with a private IP in your subnet, powered by PrivateLink. |
| **Gateway endpoint** | A free route-table entry for S3 and DynamoDB only (not PrivateLink, but similar idea). |
| **Endpoint service** | Your own service shared privately with other VPCs or accounts. |

## How it works (step by step)

1. You create an **interface endpoint** for a service (e.g. Secrets Manager) in your subnets.
2. AWS places a private network card in each subnet.
3. With private DNS on, the service's normal name now points to that private IP.
4. Your servers reach the service without the internet.

## When to use it

- Private subnets that call AWS APIs.
- Offering your own service to customers' VPCs privately.

## When NOT to use it (and what to use instead)

- **S3 or DynamoDB from inside a VPC.** → A **gateway endpoint** is free.
- **Connecting whole networks together.** → [Transit Gateway](transit-gateway.md) or VPC peering.

## Real-world example

**Scenario:** A health-tech company's app servers sit in private subnets with no internet.

**The problem:** They need to read passwords from Secrets Manager.

**How it helps:** An interface endpoint for Secrets Manager lets them reach it privately.

**What it looks like:**

```
 Private subnet: App EC2 ──► Interface endpoint (10.0.2.15) ──PrivateLink──► Secrets Manager
```

## Try it yourself

> ⚠️ **Cost warning:** Interface endpoints are charged per hour per AZ plus per GB. Gateway endpoints for S3/DynamoDB are free – try those first.

### Option A – Using the AWS Console (clicking in the website)

1. **VPC** → **Endpoints** → **Create endpoint**.
2. Search for `s3`, choose the **Gateway** type service.
3. Choose your VPC and its route tables → **Create endpoint** (free).

### Option B – Using the AWS CLI (typing commands)

```bash
# Free S3 gateway endpoint (replace the IDs)
aws ec2 create-vpc-endpoint --vpc-id vpc-0123456789abcdef0 \
  --service-name com.amazonaws.eu-west-2.s3 --route-table-ids rtb-0123456789abcdef0
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# Free gateway endpoint so the VPC reaches S3 privately
resource "aws_vpc_endpoint" "s3" {
  vpc_id            = "vpc-0123456789abcdef0"
  service_name      = "com.amazonaws.eu-west-2.s3"
  vpc_endpoint_type = "Gateway"
  route_table_ids   = ["rtb-0123456789abcdef0"]
}
```

### Clean up (delete what you made)

1. **VPC** → **Endpoints** → tick it → **Actions** → **Delete VPC endpoints**.

## How much does it cost?

Interface endpoints: per endpoint per AZ per hour, plus per GB processed. Gateway endpoints: free.

Official pricing: <https://aws.amazon.com/privatelink/pricing/>

## Security tips

- Add an **endpoint policy** to limit what can be done through it (e.g. only your own buckets).

## Common mistakes

- Forgetting to turn on private DNS, so traffic still goes the public way.

## Works well with

- [VPC](vpc.md), [S3](../storage/s3.md), [Secrets Manager](../security-identity-compliance/secrets-manager.md).

## Quick check (test yourself)

1. Which endpoint type is free?
   <details><summary>Answer</summary>Gateway endpoints, for S3 and DynamoDB.</details>
2. What does an interface endpoint create in your subnet?
   <details><summary>Answer</summary>A network card with a private IP address.</details>
3. Why use PrivateLink?
   <details><summary>Answer</summary>To reach services privately without the internet or a NAT gateway.</details>

## Learn more

- [AWS PrivateLink documentation](https://docs.aws.amazon.com/vpc/latest/privatelink/what-is-privatelink.html)
- [AWS PrivateLink pricing](https://aws.amazon.com/privatelink/pricing/)
