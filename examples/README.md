# Hands-on examples

Small projects that join several AWS services together. Each one has a diagram, numbered steps and clean-up instructions.

| Project | Services used | Level | Rough time |
|---------|---------------|-------|------------|
| [1. Billing alarm and monitoring dashboard](billing-alarm-dashboard.md) | Budgets + CloudWatch + SNS | 🟢 | 30 min |
| [2. Host a static website](static-website.md) | S3 + CloudFront + Route 53 | 🟢 | 45 min |
| [3. Automatic image resizer](image-resizer.md) | S3 + Lambda | 🟡 | 1 hour |
| [4. Serverless contact form](serverless-contact-form.md) | API Gateway + Lambda + DynamoDB + SES | 🟡 | 1.5 hours |
| [5. Classic web app](classic-web-app.md) | VPC + EC2 + Application Load Balancer + RDS | 🟡 | 2 hours |

**Do project 1 first** – it protects you from surprise bills while you do the others.

> ⚠️ **Cost warning:** Some projects use services that cost money outside the Free Tier (load balancers, RDS, public IPv4 addresses). Always follow the clean-up steps at the end of each project.

> 🧪 **About the code:** The Terraform and CLI examples are written for Terraform 1.x and the AWS provider `~> 6.0`. They are first drafts – run `terraform plan` and read it before you `apply`, and please open an issue if something doesn't work.

[← Back to the main index](../README.md)
