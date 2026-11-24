# AWS Elastic Beanstalk

**Category:** Compute  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Elastic Beanstalk takes your web app code and automatically sets up the servers, load balancer and scaling needed to run it.

## Real-life comparison

It's like a furnished flat with a letting agent. You bring your suitcase (your code); the agent has already set up the furniture, utilities and repairs (servers, load balancer, monitoring). You can still change things if you want.

## What problem does it solve?

Running a web app on EC2 means building servers, a load balancer, Auto Scaling and monitoring yourself. Beanstalk does all that from one upload, so developers can focus on code.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Application** | Your project in Beanstalk. |
| **Environment** | One running copy of your app, e.g. "test" or "live". |
| **Platform** | The language and version, e.g. Python, Node.js, Java, .NET, Docker. |
| **Application version** | One uploaded bundle of your code. |

## How it works (step by step)

1. You choose a **platform** (e.g. Python 3).
2. You upload your code as a zip, or with the `eb` command-line tool.
3. Beanstalk creates EC2 servers, a load balancer, Auto Scaling and CloudWatch alarms.
4. Your app gets a web address.
5. To update, you upload a new version and Beanstalk rolls it out.

## When to use it

- Standard web apps when you don't want to build infrastructure by hand.
- Teams moving an existing app to AWS quickly.

## When NOT to use it (and what to use instead)

- **You want full control written as code.** → [EC2](ec2.md) + [Terraform/CloudFormation](../management-governance/cloudformation.md).
- **Containerised apps with no servers to manage.** → [ECS](../containers/ecs.md) Express Mode or [ECS on Fargate](../containers/fargate.md).
- **Event-driven code.** → [Lambda](lambda.md).

## Real-world example

**Scenario:** Two student developers built a Python Flask app for booking tutoring sessions.

**The problem:** They don't know how to set up load balancers and scaling.

**How Beanstalk helps:** They create a Python environment and upload a zip. Beanstalk builds everything and gives them a URL.

**What it looks like:**

```
 Users ──► Load balancer ──► EC2 servers (Auto Scaling) ◄── created by Beanstalk
```

## Try it yourself

> ⚠️ **Cost warning:** Beanstalk is free, but the EC2 servers and load balancer it creates are not. Choose a single-instance environment and terminate it at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Elastic Beanstalk** → **Create application**.
2. Choose **Web server environment**, name it `demo-app`.
3. Choose platform **Python**, and **Sample application**.
4. Under **Presets**, choose **Single instance (free tier eligible)**.
5. Click through, letting it create the service role and EC2 instance profile, then **Submit**.
6. When the health is **Ok**, click the environment URL to see the sample page.

### Option B – Using the AWS CLI (typing commands)

```bash
# List environments and their health
aws elasticbeanstalk describe-environments \
  --query 'Environments[].[EnvironmentName,Health,CNAME]' --output table
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_elastic_beanstalk_environment`, but it duplicates what Beanstalk does for you. For learning, use the Console.

### Clean up (delete what you made)

1. Open the environment → **Actions** → **Terminate environment**.
2. Delete the application.
3. Check **EC2** shows no leftover servers.

## How much does it cost?

No extra charge for Beanstalk. You pay for the EC2, load balancer, storage and other resources it creates.

Official pricing: <https://aws.amazon.com/elasticbeanstalk/pricing/>

## Security tips

- Use HTTPS on the load balancer with a certificate from [ACM](../security-identity-compliance/certificate-manager.md).
- Store secrets in environment properties linked to [Secrets Manager](../security-identity-compliance/secrets-manager.md), not in code.

## Common mistakes

- Editing servers by hand – Beanstalk may replace them and your changes are lost.
- Forgetting to terminate test environments.

## Works well with

- [EC2](ec2.md), [Auto Scaling](auto-scaling.md), [Elastic Load Balancing](../networking/elastic-load-balancing.md) – what it builds.
- [RDS](../databases/rds.md) – a separate database for your app.

## Quick check (test yourself)

1. Does Beanstalk cost extra?
   <details><summary>Answer</summary>No, you pay only for the resources it creates.</details>
2. What is an environment?
   <details><summary>Answer</summary>One running copy of your app, such as test or live.</details>
3. Why shouldn't you change servers by hand?
   <details><summary>Answer</summary>Beanstalk can replace them, and manual changes are lost.</details>

## Learn more

- [Elastic Beanstalk Developer Guide](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/Welcome.html)
- [Elastic Beanstalk pricing](https://aws.amazon.com/elasticbeanstalk/pricing/)
