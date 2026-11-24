# Compute

**Compute** means the processing power that runs your code – the "brains" of an application.

**Real-life comparison:** If storage is the filing cabinet, compute is the person at the desk doing the work. AWS lets you hire that worker in different ways: a full-time employee (a server that's always on), or a freelancer who only turns up when there's a job (serverless).

## The main ways to run code on AWS

| Way | Plain English | AWS service |
|-----|---------------|-------------|
| **Virtual servers** | Your own computer in the cloud. You manage the operating system. | [EC2](ec2.md), [Lightsail](lightsail.md) |
| **Serverless functions** | Upload code; AWS runs it only when needed. No servers to manage. | [Lambda](lambda.md) |
| **Containers** | Apps packed in a standard box that runs anywhere. | See [Containers](../containers/README.md) |
| **Platform** | Upload your app; AWS sets up the servers around it. | [Elastic Beanstalk](elastic-beanstalk.md) |

## Services in this category

| Service | Level | What it does |
|---------|-------|--------------|
| [Amazon EC2](ec2.md) | 🟢 | Rent virtual servers by the hour or second |
| [AWS Lambda](lambda.md) | 🟢 | Run small pieces of code without managing a server |
| [Amazon EC2 Auto Scaling](auto-scaling.md) | 🟢 | Adds or removes servers automatically as demand changes |
| [Amazon Lightsail](lightsail.md) | 🟢 | Simple, fixed-price virtual servers for small websites |
| [AWS Elastic Beanstalk](elastic-beanstalk.md) | 🟡 | Upload your app code; AWS sets up the servers for you |
| [AWS Batch](batch.md) | 🟡 | Runs large numbers of background jobs in a queue |
| [AWS Outposts](outposts.md) | 🔴 | AWS hardware installed in your own building |
| [AWS Wavelength](wavelength.md) | 🔴 | Runs apps inside mobile (5G) networks for very low delay |
| [AWS Local Zones](local-zones.md) | 🔴 | Small AWS sites in big cities, closer to users |

## Which one should I use?

- **Learning, or need full control of a server?** → [EC2](ec2.md)
- **A simple website or WordPress blog with a fixed monthly price?** → [Lightsail](lightsail.md)
- **Code that runs when something happens (a file upload, an API call)?** → [Lambda](lambda.md)
- **A web app and you don't want to set up servers yourself?** → [Elastic Beanstalk](elastic-beanstalk.md) or [App Runner](../containers/app-runner.md)

[← Back to the main index](../../README.md)
