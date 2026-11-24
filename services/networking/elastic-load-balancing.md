# Elastic Load Balancing (ELB)

**Category:** Networking & content delivery  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Elastic Load Balancing shares incoming traffic across several servers, and stops sending traffic to any server that isn't healthy.

## Real-life comparison

A load balancer is like the person at the front of a queue in a bank who says "next customer to desk 3". They spread customers across open desks, and if a desk closes, they stop sending people there.

## What problem does it solve?

One server can be overloaded or fail. With several servers, you need something to spread visitors between them and give users one address to use. ELB does that, checks each server's health, and handles HTTPS for you.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Application Load Balancer (ALB)** | For websites and APIs (HTTP/HTTPS). Can route by URL path or host name. |
| **Network Load Balancer (NLB)** | For very fast, high-volume TCP/UDP traffic. |
| **Gateway Load Balancer (GWLB)** | For sending traffic through security appliances like firewalls. |
| **Listener** | Waits for traffic on a port, e.g. 443 for HTTPS. |
| **Target group** | The list of servers (or containers, or Lambda functions) that receive traffic. |
| **Health check** | A regular test request to each target. |
| **Classic Load Balancer** | The older generation – avoid for new projects. |

## How it works (step by step)

1. You create a load balancer in **public subnets** in at least two AZs.
2. You add a **listener** (e.g. HTTPS on port 443) with a certificate.
3. You create a **target group** and register your servers.
4. The load balancer runs **health checks** on each server.
5. Users connect to the load balancer's address. It forwards each request to a healthy server.
6. If a server fails its health check, traffic goes to the others until it recovers.

## When to use it

- Any website or API running on more than one server or container.
- With [Auto Scaling](../compute/auto-scaling.md), so new servers get traffic automatically.
- Ending HTTPS in one place instead of on every server.

## When NOT to use it (and what to use instead)

- **A single small server with very little traffic.** A load balancer has an hourly cost. [Lightsail](../compute/lightsail.md) may be simpler.
- **Serverless APIs.** → [API Gateway](api-gateway.md) in front of [Lambda](../compute/lambda.md).
- **Serving static files worldwide.** → [CloudFront](cloudfront.md).

## Real-world example

**Scenario:** An online school's website runs on two EC2 servers.

**The problem:** During exam results day, one server is overwhelmed while the other is idle, and when one crashed, half the students got errors.

**How ELB helps:** An ALB with HTTPS spreads students evenly, and health checks stop traffic going to the crashed server. With Auto Scaling, more servers join automatically when busy.

**What it looks like:**

```
            Students
               │ HTTPS :443
               ▼
   Application Load Balancer (public subnets, AZ a + b)
          ┌────┴─────┐  health checks
          ▼          ▼
      EC2 (AZ a)  EC2 (AZ b)   ← target group (private subnets)
```

## Try it yourself

> ⚠️ **Cost warning:** Load balancers are charged per hour plus a usage charge. New accounts may get some free hours (check the [Free Tier page](https://aws.amazon.com/free/)). **Delete the load balancer the same day.**

**Before you start:** Two EC2 instances running a simple web server in different AZs of your default VPC.

### Option A – Using the AWS Console (clicking in the website)

1. Open **EC2** → **Target Groups** → **Create target group**.
2. Choose **Instances**, name `demo-tg`, protocol **HTTP**, port **80**. Click **Next**.
3. Tick your two instances → **Include as pending below** → **Create target group**.
4. Go to **Load Balancers** → **Create load balancer** → **Application Load Balancer**.
5. Name `demo-alb`, **Internet-facing**, choose **at least two AZs**.
6. Choose a security group that allows HTTP (port 80) from the internet.
7. **Listener:** HTTP port 80 → forward to `demo-tg`. Click **Create load balancer**.
8. When it's **Active**, copy its **DNS name** into your browser. Refresh a few times – you may see responses from both servers.

### Option B – Using the AWS CLI (typing commands)

```bash
# Check the health of each server in a target group (replace the ARN)
aws elbv2 describe-target-health \
  --target-group-arn arn:aws:elasticloadbalancing:eu-west-2:123456789012:targetgroup/demo-tg/0123456789abcdef

# List load balancers and their DNS names
aws elbv2 describe-load-balancers \
  --query 'LoadBalancers[].[LoadBalancerName,DNSName,State.Code]' --output table
```

### Option C – Using Terraform (infrastructure as code)

A full ALB + EC2 + RDS setup is in the [classic web app project](../../examples/classic-web-app.md).

### Clean up (delete what you made)

1. **Load Balancers** → tick `demo-alb` → **Actions** → **Delete load balancer**.
2. **Target Groups** → tick `demo-tg` → **Actions** → **Delete**.
3. Terminate the test EC2 instances.

## How much does it cost?

- **Per hour** the load balancer exists.
- **Per LCU-hour** (Load Balancer Capacity Unit) – a measure of how much work it does (connections, bandwidth, rules).
- Public IPv4 addresses used by the load balancer are charged too.

Official pricing: <https://aws.amazon.com/elasticloadbalancing/pricing/>

## Security tips

- Use **HTTPS** listeners with certificates from [ACM](../security-identity-compliance/certificate-manager.md) and redirect HTTP to HTTPS.
- Put the servers in **private subnets** and only allow traffic from the load balancer's security group.
- Attach [AWS WAF](../security-identity-compliance/waf.md) to an ALB to block common attacks.

## Common mistakes

- Health check path returns an error (e.g. `/health` doesn't exist), so every target is marked unhealthy.
- The servers' security group doesn't allow traffic from the load balancer.
- Choosing only one AZ.

## Works well with

- [EC2](../compute/ec2.md) and [Auto Scaling](../compute/auto-scaling.md).
- [ECS](../containers/ecs.md) – load balance containers.
- [Route 53](route-53.md) – point your domain at the load balancer with an alias record.

## Quick check (test yourself)

1. Which load balancer type would you choose for a normal website?
   <details><summary>Answer</summary>An Application Load Balancer (ALB).</details>
2. What happens when a server fails its health check?
   <details><summary>Answer</summary>The load balancer stops sending it traffic until it's healthy again.</details>
3. What is a target group?
   <details><summary>Answer</summary>The list of servers, containers or functions that receive traffic from the load balancer.</details>

## Learn more

- [Elastic Load Balancing documentation](https://docs.aws.amazon.com/elasticloadbalancing/)
- [Elastic Load Balancing pricing](https://aws.amazon.com/elasticloadbalancing/pricing/)
