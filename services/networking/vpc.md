# Amazon Virtual Private Cloud (VPC)

**Category:** Networking & content delivery  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

A VPC is your own private, isolated network inside AWS, where you decide the IP address ranges, subnets, routes and firewall rules.

## Real-life comparison

A VPC is like a gated housing estate. You decide the street layout (subnets), which roads lead to the main road (route tables and internet gateway), and who the security guard lets in (security groups and network ACLs). Some houses face the main road (public subnets); others are tucked away at the back (private subnets).

## What problem does it solve?

In an office, the IT team builds a network with switches, routers and firewalls to keep servers safe. In AWS, the VPC does the same job in software. It keeps your resources separated from other customers and lets you control exactly what can reach what.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **CIDR block** | The range of private IP addresses in your VPC, e.g. `10.0.0.0/16` (about 65,000 addresses). |
| **Subnet** | A smaller section of the VPC, in one Availability Zone. |
| **Public subnet** | A subnet with a route to the internet gateway. Things here can have public IPs. |
| **Private subnet** | A subnet with no direct route from the internet. Safer for databases and app servers. |
| **Internet gateway (IGW)** | The door between your VPC and the internet. |
| **NAT gateway** | Lets private servers reach the internet (e.g. for updates) without the internet reaching them. |
| **Route table** | Rules saying where network traffic should go. |
| **Security group** | A firewall around each resource. Stateful: replies are allowed back automatically. |
| **Network ACL** | A firewall around a whole subnet. Stateless: you must allow both directions. |

## How it works (step by step)

1. You create a VPC with a CIDR block, e.g. `10.0.0.0/16`.
2. You split it into **subnets** in different AZs, e.g. `10.0.1.0/24` (public) and `10.0.2.0/24` (private).
3. You attach an **internet gateway** to the VPC.
4. In the public subnet's **route table**, you send internet traffic (`0.0.0.0/0`) to the internet gateway.
5. For private subnets that need outbound internet, you add a **NAT gateway** in a public subnet and route to it.
6. You launch resources (EC2, RDS) into subnets and protect each with a **security group**.

Every account comes with a **default VPC** in each Region so you can start quickly, but real projects build their own.

## When to use it

- Every time you run EC2, RDS, load balancers, containers and most other resources – they live in a VPC.
- Separating environments (test vs live) or teams.
- Connecting AWS to your office network (see [Site-to-Site VPN](site-to-site-vpn.md)).

## When NOT to use it (and what to use instead)

- You can't really avoid it for server-based resources. But fully managed services like [S3](../storage/s3.md), [DynamoDB](../databases/dynamodb.md) and [Lambda](../compute/lambda.md) (by default) don't need you to build one.
- **Connecting many VPCs together.** Simple peering gets messy. → Use [Transit Gateway](transit-gateway.md).

## Real-world example

**Scenario:** Nadia's start-up runs a web app with a database.

**The problem:** The database sits on a server with a public IP address. Anyone on the internet can try to connect to it.

**How VPC helps:** Nadia builds a VPC with public and private subnets across two AZs. The load balancer sits in the public subnets. The app servers and the database sit in private subnets. Only the load balancer can reach the app, and only the app can reach the database.

**What it looks like:**

```
                       Internet
                          │
                   Internet gateway
 ┌──────────────── VPC 10.0.0.0/16 ─────────────────┐
 │  Public subnet (AZ a)      Public subnet (AZ b)  │
 │   [Load balancer] ──────────[Load balancer]      │
 │          │                        │              │
 │  Private subnet (AZ a)     Private subnet (AZ b) │
 │      [App EC2]                [App EC2]          │
 │          └──────────┬─────────────┘              │
 │                  [RDS database]                  │
 └──────────────────────────────────────────────────┘
```

## Try it yourself

> ⚠️ **Cost warning:** VPCs, subnets, route tables and internet gateways are free. **NAT gateways and public IPv4 addresses cost money per hour.** This exercise skips NAT gateways. Delete everything at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Open **VPC** in the Console (Region **eu-west-2**).
2. Click **Create VPC** and choose **VPC and more** (this builds a whole layout for you).
3. **Name tag auto-generation:** `demo`.
4. **IPv4 CIDR:** `10.0.0.0/16`.
5. **Number of AZs:** 2. **Public subnets:** 2. **Private subnets:** 2.
6. **NAT gateways:** **None** (to avoid charges).
7. **VPC endpoints:** **None**.
8. Look at the **Preview** diagram on the right – it shows how the pieces connect.
9. Click **Create VPC**.
10. Open **Route tables** and compare a public one (has a route to `igw-...`) with a private one (doesn't).

### Option B – Using the AWS CLI (typing commands)

```bash
# Create the VPC and save its ID
VPC_ID=$(aws ec2 create-vpc --cidr-block 10.0.0.0/16 \
  --query 'Vpc.VpcId' --output text)

# Create one public subnet in AZ a
SUBNET_ID=$(aws ec2 create-subnet --vpc-id $VPC_ID --cidr-block 10.0.1.0/24 \
  --availability-zone eu-west-2a --query 'Subnet.SubnetId' --output text)

# Create an internet gateway and attach it to the VPC
IGW_ID=$(aws ec2 create-internet-gateway --query 'InternetGateway.InternetGatewayId' --output text)
aws ec2 attach-internet-gateway --vpc-id $VPC_ID --internet-gateway-id $IGW_ID

# Create a route table, send internet traffic to the gateway, and link it to the subnet
RT_ID=$(aws ec2 create-route-table --vpc-id $VPC_ID --query 'RouteTable.RouteTableId' --output text)
aws ec2 create-route --route-table-id $RT_ID --destination-cidr-block 0.0.0.0/0 --gateway-id $IGW_ID
aws ec2 associate-route-table --route-table-id $RT_ID --subnet-id $SUBNET_ID
```

### Option C – Using Terraform (infrastructure as code)

Written for the AWS provider `~> 6.0`.

```hcl
# The VPC
resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  tags = { Name = "demo-vpc" }
}

# One public and one private subnet in AZ a
resource "aws_subnet" "public_a" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.1.0/24"
  availability_zone = "eu-west-2a"
  tags = { Name = "demo-public-a" }
}

resource "aws_subnet" "private_a" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.2.0/24"
  availability_zone = "eu-west-2a"
  tags = { Name = "demo-private-a" }
}

# The door to the internet
resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.main.id
}

# Public route table: send all internet traffic to the gateway
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id
  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.igw.id
  }
}

# Link the public route table to the public subnet
resource "aws_route_table_association" "public_a" {
  subnet_id      = aws_subnet.public_a.id
  route_table_id = aws_route_table.public.id
}
```

### Clean up (delete what you made)

1. Make sure no EC2 instances or other resources are running in the VPC.
2. **VPC** → **Your VPCs** → tick `demo-vpc` → **Actions** → **Delete VPC**. This removes its subnets, route tables and internet gateway too.
3. Terraform: `terraform destroy`.

## How much does it cost?

- **Free:** the VPC, subnets, route tables, internet gateways, security groups.
- **Charged:** NAT gateways (per hour + per GB), public IPv4 addresses (per hour), VPN connections, some VPC endpoints, and data moving between AZs.

Official pricing: <https://aws.amazon.com/vpc/pricing/>

## Security tips

- Put databases and app servers in **private subnets**.
- In security groups, allow traffic **from other security groups** (e.g. "the app servers") instead of IP ranges where possible.
- Turn on **VPC Flow Logs** to record traffic for troubleshooting and investigations.
- Never allow `0.0.0.0/0` on admin ports (22, 3389) or database ports.

## Common mistakes

- **Overlapping CIDR ranges** between VPCs or with your office – you can't connect them later.
- **Forgetting the route** to the internet gateway, so a "public" subnet has no internet.
- **Leaving a NAT gateway running** in a test VPC – it costs money every hour.
- **Making subnets too small** – you can't easily resize them.

## Works well with

- [EC2](../compute/ec2.md) and [RDS](../databases/rds.md) – live inside your subnets.
- [Elastic Load Balancing](elastic-load-balancing.md) – sits in public subnets.
- [Site-to-Site VPN](site-to-site-vpn.md) and [Transit Gateway](transit-gateway.md) – connect VPCs to other networks.

## Quick check (test yourself)

1. What makes a subnet "public"?
   <details><summary>Answer</summary>Its route table has a route to an internet gateway.</details>
2. What lets servers in a private subnet download updates without being reachable from the internet?
   <details><summary>Answer</summary>A NAT gateway.</details>
3. What's the difference between a security group and a network ACL?
   <details><summary>Answer</summary>A security group protects individual resources and is stateful. A network ACL protects a whole subnet and is stateless.</details>

## Learn more

- [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
- [Amazon VPC pricing](https://aws.amazon.com/vpc/pricing/)
