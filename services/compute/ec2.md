# Amazon Elastic Compute Cloud (EC2)

**Category:** Compute  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

EC2 lets you rent virtual servers (computers that run inside AWS's data centres) by the second, choosing their size and operating system.

## Real-life comparison

EC2 is like hiring a car. You pick the model (small run-around or big van), use it as long as you need, and hand it back. You're the driver, so you're responsible for how it's driven – but you never have to fix the engine.

## What problem does it solve?

Buying a physical server means paying thousands up front, waiting weeks for delivery, and guessing how powerful it needs to be. With EC2, you get a server in minutes, change its size later, and stop paying when you turn it off.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Instance** | One virtual server. |
| **Instance type** | The size of the server – how many CPUs and how much memory, e.g. `t3.micro`. |
| **AMI** (Amazon Machine Image) | A template with the operating system (and sometimes software) already installed. |
| **Key pair** | A pair of keys used to log in securely over SSH (instead of a password). |
| **Security group** | A virtual firewall that controls which traffic can reach the server. |
| **EBS volume** | The server's virtual hard drive. See [EBS](../storage/ebs.md). |
| **User data** | A script that runs automatically the first time the server starts. |

## How it works (step by step)

1. You choose an **AMI** (e.g. Amazon Linux or Windows Server).
2. You choose an **instance type** (how big).
3. You choose the network (VPC and subnet) and a **security group** (firewall rules).
4. You choose or create a **key pair** to log in.
5. AWS starts the server on a physical machine in the Availability Zone you picked.
6. You connect (SSH for Linux, RDP for Windows, or Session Manager in the browser) and use it like any computer.
7. You **stop** it to pause billing for compute, or **terminate** it to delete it.

## When to use it

- You need full control over the operating system and software.
- Running websites, game servers, business apps or learning Linux.
- Moving an existing server from an office into AWS.

## When NOT to use it (and what to use instead)

- **Short tasks that run when something happens.** → Use [Lambda](lambda.md) – no server to manage.
- **A simple website with a fixed price.** → Use [Lightsail](lightsail.md).
- **You want a database without managing a server.** → Use [RDS](../databases/rds.md).
- **You don't want to patch operating systems at all.** → Use [Fargate](../containers/fargate.md) or [Lambda](lambda.md).

## Real-world example

**Scenario:** Leo runs a small recruitment agency with a custom web app built by a freelancer.

**The problem:** The app runs on an old PC under a desk in the office. When the office loses power, the site goes down.

**How EC2 helps:** Leo launches an EC2 instance in London, installs the app, and points his domain at it. The server runs in an AWS data centre with backup power. If traffic grows, he can switch to a bigger instance type in a few minutes.

**What it looks like:**

```
 Candidate's browser ──internet──► Security group (allow 443 only)
                                          │
                                          ▼
                                 EC2 instance (t3.small)
                                          │
                                   EBS volume (disk)
```

## Try it yourself

> ⚠️ **Cost warning:** Small instance types such as `t3.micro` are included in the Free Tier for new accounts, within limits (check the [Free Tier page](https://aws.amazon.com/free/)). Bigger types cost money every second they run. **Terminate the instance at the end.**

**Before you start:** An AWS account with MFA turned on (see [START-HERE.md](../../START-HERE.md)).

### Option A – Using the AWS Console (clicking in the website)

1. Open **EC2** in the Console. Check the Region is **eu-west-2** (London).
2. Click **Launch instance**.
3. **Name:** `my-first-server`.
4. **AMI:** leave **Amazon Linux 2023** selected.
5. **Instance type:** choose **t3.micro** (look for "Free tier eligible").
6. **Key pair:** choose **Proceed without a key pair** – you'll connect through the browser instead.
7. **Network settings:** leave the defaults. Untick **Allow SSH traffic from** (you won't need it).
8. Click **Launch instance**, then **View all instances**.
9. Wait until **Instance state** shows **Running** and **Status check** shows **2/2 checks passed**.
10. Tick the instance → **Connect** → **EC2 Instance Connect** → **Connect**. (If this fails because SSH is closed, use the **Session Manager** tab instead; it needs an IAM role – see [Systems Manager](../management-governance/systems-manager.md).)
11. In the terminal, type `cat /etc/os-release` to see the operating system.

### Option B – Using the AWS CLI (typing commands)

```bash
# Find the ID of the latest Amazon Linux 2023 image in London
AMI_ID=$(aws ssm get-parameter --region eu-west-2 \
  --name /aws/service/ami-amazon-linux-latest/al2023-ami-kernel-default-x86_64 \
  --query 'Parameter.Value' --output text)

# Launch one small server with that image and a Name tag
aws ec2 run-instances --region eu-west-2 \
  --image-id "$AMI_ID" --instance-type t3.micro --count 1 \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=my-first-server}]'

# List your servers and their state
aws ec2 describe-instances --region eu-west-2 \
  --query 'Reservations[].Instances[].[InstanceId,State.Name,Tags[?Key==`Name`]|[0].Value]' \
  --output table
```

### Option C – Using Terraform (infrastructure as code)

Written for the AWS provider `~> 6.0`.

```hcl
provider "aws" {
  region = "eu-west-2"
}

# Look up the latest Amazon Linux 2023 image
data "aws_ssm_parameter" "al2023" {
  name = "/aws/service/ami-amazon-linux-latest/al2023-ami-kernel-default-x86_64"
}

# One small server
resource "aws_instance" "web" {
  ami           = data.aws_ssm_parameter.al2023.value
  instance_type = "t3.micro"

  # Require the more secure IMDSv2 for instance metadata
  metadata_options {
    http_tokens = "required"
  }

  tags = {
    Name = "my-first-server"
  }
}
```

### Clean up (delete what you made)

1. In **Instances**, tick `my-first-server`.
2. **Instance state** → **Terminate (delete) instance** → confirm.
3. Wait until the state is **Terminated**. The disk is deleted with it by default.
4. CLI: `aws ec2 terminate-instances --instance-ids i-0123456789abcdef0`
5. Terraform: `terraform destroy`

## How much does it cost?

- **Compute time** – per second (Linux) or per hour, based on instance type, while running.
- **Storage** – EBS disks are charged per GB per month, even when stopped.
- **Data transfer out** to the internet.
- **Ways to pay less:** Savings Plans and Reserved Instances (commit to 1 or 3 years) or **Spot Instances** (spare capacity, much cheaper, but AWS can take it back with 2 minutes' warning).

Official pricing: <https://aws.amazon.com/ec2/pricing/>

## Security tips

- **Only open the ports you need** in security groups. Never open SSH (port 22) or RDP (3389) to `0.0.0.0/0` (the whole internet).
- Prefer **Session Manager** to SSH – no open ports or keys to lose.
- Give the server an **IAM role** instead of storing access keys on it.
- Keep the operating system updated (that's your job under the shared responsibility model).
- Require **IMDSv2** for instance metadata.

## Common mistakes

- **Leaving instances running** after testing.
- **Losing the key pair file** – AWS can't give it back to you.
- **Stopping instead of terminating** – a stopped server still costs money for its disk.
- **Opening port 22 to the whole internet** – bots try to break in within minutes.

## Works well with

- [EBS](../storage/ebs.md) – the server's disks.
- [VPC](../networking/vpc.md) – the network the server lives in.
- [Elastic Load Balancing](../networking/elastic-load-balancing.md) – shares traffic across several servers.
- [Auto Scaling](auto-scaling.md) – adds or removes servers automatically.
- [CloudWatch](../management-governance/cloudwatch.md) – monitors CPU and sends alarms.

## Quick check (test yourself)

1. What is an AMI?
   <details><summary>Answer</summary>A template that holds the operating system (and maybe software) used to start a server.</details>
2. Do you pay anything for a stopped EC2 instance?
   <details><summary>Answer</summary>You don't pay for compute, but you still pay for its EBS disk.</details>
3. What controls which network traffic can reach your instance?
   <details><summary>Answer</summary>Its security group (a virtual firewall).</details>

## Learn more

- [Amazon EC2 User Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
- [Amazon EC2 pricing](https://aws.amazon.com/ec2/pricing/)
