# Amazon EC2 Auto Scaling (Auto Scaling)

**Category:** Compute  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Auto Scaling automatically adds EC2 servers when your app is busy, removes them when it's quiet, and replaces any that break.

## Real-life comparison

Auto Scaling is like a supermarket manager who opens more tills when queues get long and closes them when the shop is quiet. If a till breaks, they open another one straight away.

## What problem does it solve?

If you run a fixed number of servers, you either pay for too many when it's quiet or crash when it's busy. And if a server fails at 3am, someone has to notice and fix it. Auto Scaling keeps the right number of healthy servers running, automatically.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Auto Scaling group (ASG)** | A group of identical EC2 servers managed together. |
| **Launch template** | The recipe for each new server (AMI, instance type, security group, user data). |
| **Minimum / desired / maximum** | The fewest, the normal and the most servers the group may have. |
| **Scaling policy** | The rule for when to add or remove servers, e.g. "keep average CPU at 50%". |
| **Health check** | A regular test to see if each server is working. |

## How it works (step by step)

1. You create a **launch template** (the recipe).
2. You create an **Auto Scaling group** using that template, across two or more AZs.
3. You set **minimum**, **desired** and **maximum** sizes.
4. You add a **scaling policy**, such as "target average CPU 50%".
5. [CloudWatch](../management-governance/cloudwatch.md) watches the servers. When CPU rises, the group launches more; when it drops, it removes some.
6. If a health check fails, the group terminates that server and launches a replacement.

## When to use it

- Web apps with busy and quiet times.
- Keeping at least one healthy server running at all times (self-healing).
- Spreading servers across AZs for resilience.

## When NOT to use it (and what to use instead)

- **Serverless apps.** Lambda scales by itself. → [Lambda](lambda.md)
- **Containers.** → Use the scaling built into [ECS](../containers/ecs.md) or [EKS](../containers/eks.md).
- **A server that stores important data on its own disk.** Servers in a group can be replaced at any time – keep data in [RDS](../databases/rds.md), [S3](../storage/s3.md) or [EFS](../storage/efs.md).

## Real-world example

**Scenario:** A concert ticket website is quiet most days, but extremely busy when tickets for a big tour go on sale.

**The problem:** Two servers are fine normally but crash on sale days.

**How Auto Scaling helps:** The site runs in an Auto Scaling group (min 2, max 20) behind a load balancer. On sale day, CPU rises, and the group adds servers within minutes. Afterwards, it shrinks back to 2.

**What it looks like:**

```
               Application Load Balancer
          ┌──────────────┼──────────────┐
 Auto Scaling group (min 2, desired 2, max 20)
   [EC2] [EC2]  ... adds more when CPU > 50% ...
     AZ a   AZ b
```

## Try it yourself

> ⚠️ **Cost warning:** Auto Scaling itself is free, but you pay for the EC2 servers it launches. Use `t3.micro` and set the maximum to 2. **Delete the group at the end – otherwise it will keep replacing servers you terminate.**

### Option A – Using the AWS Console (clicking in the website)

1. Open **EC2** → **Launch Templates** → **Create launch template**.
2. Name it `demo-template`, choose **Amazon Linux 2023** and **t3.micro**, and click **Create launch template**.
3. Go to **Auto Scaling Groups** → **Create Auto Scaling group**.
4. Name it `demo-asg` and choose `demo-template`. Click **Next**.
5. Choose your default VPC and **two subnets** in different AZs. Click **Next** until **Group size**.
6. Set **Desired 1**, **Min 1**, **Max 2**.
7. Choose **Target tracking scaling policy**, **Average CPU utilisation**, target **50**.
8. Click through to **Create Auto Scaling group**.
9. Go to **Instances** – one server has started. Terminate it and watch the group launch a replacement.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create the group from an existing launch template (replace subnet IDs)
aws autoscaling create-auto-scaling-group \
  --auto-scaling-group-name demo-asg \
  --launch-template LaunchTemplateName=demo-template,Version='$Latest' \
  --min-size 1 --max-size 2 --desired-capacity 1 \
  --vpc-zone-identifier "subnet-aaaa1111,subnet-bbbb2222"

# Keep average CPU around 50%
aws autoscaling put-scaling-policy --auto-scaling-group-name demo-asg \
  --policy-name cpu50 --policy-type TargetTrackingScaling \
  --target-tracking-configuration '{"PredefinedMetricSpecification":{"PredefinedMetricType":"ASGAverageCPUUtilization"},"TargetValue":50.0}'
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# The group, using an existing launch template and two subnets
resource "aws_autoscaling_group" "demo" {
  name                = "demo-asg"
  min_size            = 1
  max_size            = 2
  desired_capacity    = 1
  vpc_zone_identifier = ["subnet-aaaa1111", "subnet-bbbb2222"]

  launch_template {
    name    = "demo-template"
    version = "$Latest"
  }
}

# Target tracking: keep average CPU at 50%
resource "aws_autoscaling_policy" "cpu50" {
  name                   = "cpu50"
  autoscaling_group_name = aws_autoscaling_group.demo.name
  policy_type            = "TargetTrackingScaling"
  target_tracking_configuration {
    predefined_metric_specification {
      predefined_metric_type = "ASGAverageCPUUtilization"
    }
    target_value = 50
  }
}
```

### Clean up (delete what you made)

1. **Auto Scaling Groups** → tick `demo-asg` → **Actions** → **Delete**. This also terminates its servers.
2. **Launch Templates** → tick `demo-template` → **Actions** → **Delete template**.
3. Check **Instances** shows no running servers from the group.

## How much does it cost?

Auto Scaling is free. You pay for the EC2 servers, disks and CloudWatch features it uses.

Official pricing: <https://aws.amazon.com/ec2/autoscaling/pricing/>

## Security tips

- Put security settings (security groups, IAM role, IMDSv2) in the **launch template**, so every new server gets them.
- Use servers in private subnets behind a load balancer.

## Common mistakes

- Terminating servers by hand and wondering why they keep coming back – delete the group instead.
- Storing data on the servers' own disks – it's lost when they're replaced.
- Setting the maximum too high and getting a surprise bill.

## Works well with

- [EC2](ec2.md) – the servers being scaled.
- [Elastic Load Balancing](../networking/elastic-load-balancing.md) – sends traffic to the healthy servers.
- [CloudWatch](../management-governance/cloudwatch.md) – supplies the metrics for scaling.

## Quick check (test yourself)

1. What is a launch template?
   <details><summary>Answer</summary>The recipe Auto Scaling uses to create each new server.</details>
2. What happens if a server in the group fails its health check?
   <details><summary>Answer</summary>The group terminates it and launches a replacement.</details>
3. Does Auto Scaling cost extra?
   <details><summary>Answer</summary>No. You only pay for the resources it launches.</details>

## Learn more

- [Amazon EC2 Auto Scaling User Guide](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)
- [Auto Scaling pricing](https://aws.amazon.com/ec2/autoscaling/pricing/)
