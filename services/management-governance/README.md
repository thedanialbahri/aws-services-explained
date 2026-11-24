# Management & governance

These services help you **watch**, **record**, **build** and **control** everything in your AWS accounts.

**Real-life comparison:** Running AWS without these is like running a factory with no CCTV, no visitor log, no instruction manuals and no safety inspector. CloudWatch is the dashboard of gauges, CloudTrail is the visitor log, CloudFormation is the instruction manual, and Config is the safety inspector.

## Services in this category

| Service | Level | What it does |
|---------|-------|--------------|
| [Amazon CloudWatch](cloudwatch.md) | 🟢 | Collects metrics and logs, and sends alarms |
| [AWS CloudTrail](cloudtrail.md) | 🟢 | Records who did what in your account |
| [AWS Trusted Advisor](trusted-advisor.md) | 🟢 | Checks your account and suggests improvements |
| [AWS Health Dashboard](health-dashboard.md) | 🟢 | Shows AWS problems that affect you |
| [AWS Config](config.md) | 🟡 | Records settings over time and checks them against rules |
| [AWS Systems Manager](systems-manager.md) | 🟡 | Manage, patch and connect to many servers from one place |
| [AWS CloudFormation](cloudformation.md) | 🟡 | Builds AWS resources from template files |
| [AWS Control Tower](control-tower.md) | 🔴 | Sets up a secure multi-account environment with guardrails |
| [AWS Service Catalog](service-catalog.md) | 🔴 | A shop of approved resources teams can launch |

> 💡 **Terraform** isn't an AWS service, but it does the same job as CloudFormation and works across many clouds. Many pages in this repo include Terraform examples.

[← Back to the main index](../../README.md)
