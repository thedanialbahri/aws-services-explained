# Containers

A **container** packages an app with everything it needs to run (code, libraries, settings) into one standard box that runs the same way anywhere.

**Real-life comparison:** Shipping containers changed world trade because every ship, lorry and crane could handle the same box. Software containers do the same: build once, run on a laptop, a server or the cloud.

## Key words

| Word | Plain English |
|------|---------------|
| **Image** | The packaged app – a template for containers. |
| **Container** | A running copy of an image. |
| **Docker** | The most popular tool for building and running containers. |
| **Registry** | A store of images ([ECR](ecr.md)). |
| **Orchestrator** | A system that runs and manages many containers ([ECS](ecs.md), [EKS](eks.md)). |

## Services in this category

| Service | Level | What it does |
|---------|-------|--------------|
| [Amazon ECS](ecs.md) | 🟡 | AWS's own system for running containers |
| [AWS Fargate](fargate.md) | 🟡 | Runs containers without you managing any servers |
| [Amazon ECR](ecr.md) | 🟡 | Stores your container images |
| [AWS App Runner](app-runner.md) | 🟡 | Turns your code or container into a running web app in a few clicks |
| [Amazon EKS](eks.md) | 🔴 | Runs Kubernetes for you |

## Which one should I use?

- **Simplest way to run a web container?** → [App Runner](app-runner.md) or [ECS on Fargate](fargate.md)
- **Your team already uses Kubernetes?** → [EKS](eks.md)
- **Want AWS-native and simpler than Kubernetes?** → [ECS](ecs.md)

[← Back to the main index](../../README.md)
