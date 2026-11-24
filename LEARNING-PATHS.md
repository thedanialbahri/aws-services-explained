# Learning paths

Not sure where to start? Pick a path and follow it in order. Tick off each item as you go.

Before any path, read [START-HERE.md](START-HERE.md) and do [Project 1: Billing alarm](examples/billing-alarm-dashboard.md) so you're protected from surprise bills.

---

## Path 1 – Absolute beginner

**Goal:** Understand the core services that almost every AWS project uses. About 15 pages.

1. [ ] [START-HERE](START-HERE.md) – the cloud, Regions, shared responsibility, safe account setup
2. [ ] [IAM](services/security-identity-compliance/iam.md) – who can do what
3. [ ] [IAM Identity Center](services/security-identity-compliance/iam-identity-center.md) – safe logins
4. [ ] [Budgets](services/cost-management/budgets.md) – avoid surprise bills
5. [ ] [S3](services/storage/s3.md) – storing files
6. [ ] [EC2](services/compute/ec2.md) – virtual servers
7. [ ] [EBS](services/storage/ebs.md) – server disks
8. [ ] [VPC](services/networking/vpc.md) – your private network
9. [ ] [Elastic Load Balancing](services/networking/elastic-load-balancing.md) – sharing traffic
10. [ ] [Auto Scaling](services/compute/auto-scaling.md) – the right number of servers
11. [ ] [RDS](services/databases/rds.md) – managed databases
12. [ ] [DynamoDB](services/databases/dynamodb.md) – NoSQL
13. [ ] [Lambda](services/compute/lambda.md) – serverless code
14. [ ] [CloudWatch](services/management-governance/cloudwatch.md) – monitoring
15. [ ] [Route 53](services/networking/route-53.md) and [CloudFront](services/networking/cloudfront.md) – domains and fast delivery
16. [ ] [SNS](services/application-integration/sns.md) and [SQS](services/application-integration/sqs.md) – messages

**Then build:** [Project 2: Static website](examples/static-website.md).

---

## Path 2 – Certification prep

### AWS Certified Cloud Practitioner (CLF)

Grouped by the exam's main areas. Check the [official exam guide](https://aws.amazon.com/certification/certified-cloud-practitioner/) for the current domains and weightings.

**Cloud concepts**
- [ ] [START-HERE](START-HERE.md) (benefits of cloud, Regions/AZs)

**Security and compliance**
- [ ] [IAM](services/security-identity-compliance/iam.md), [IAM Identity Center](services/security-identity-compliance/iam-identity-center.md), [Organizations](services/security-identity-compliance/organizations.md)
- [ ] [Shield](services/security-identity-compliance/shield.md), [WAF](services/security-identity-compliance/waf.md), [GuardDuty](services/security-identity-compliance/guardduty.md), [Inspector](services/security-identity-compliance/inspector.md), [Macie](services/security-identity-compliance/macie.md), [Security Hub](services/security-identity-compliance/security-hub.md)
- [ ] [KMS](services/security-identity-compliance/kms.md), [Secrets Manager](services/security-identity-compliance/secrets-manager.md), [Artifact](services/security-identity-compliance/artifact.md)
- [ ] [CloudTrail](services/management-governance/cloudtrail.md), [Config](services/management-governance/config.md), [Trusted Advisor](services/management-governance/trusted-advisor.md)

**Cloud technology and services**
- [ ] Compute: [EC2](services/compute/ec2.md), [Lambda](services/compute/lambda.md), [Elastic Beanstalk](services/compute/elastic-beanstalk.md), [Lightsail](services/compute/lightsail.md), [ECS](services/containers/ecs.md), [Fargate](services/containers/fargate.md)
- [ ] Storage: [S3](services/storage/s3.md), [S3 Glacier](services/storage/s3-glacier.md), [EBS](services/storage/ebs.md), [EFS](services/storage/efs.md), [Storage Gateway](services/storage/storage-gateway.md)
- [ ] Databases: [RDS](services/databases/rds.md), [Aurora](services/databases/aurora.md), [DynamoDB](services/databases/dynamodb.md), [Redshift](services/databases/redshift.md)
- [ ] Networking: [VPC](services/networking/vpc.md), [Route 53](services/networking/route-53.md), [CloudFront](services/networking/cloudfront.md), [Direct Connect](services/networking/direct-connect.md), [Site-to-Site VPN](services/networking/site-to-site-vpn.md)
- [ ] Global infrastructure: [Local Zones](services/compute/local-zones.md), [Outposts](services/compute/outposts.md), [Wavelength](services/compute/wavelength.md)

**Billing, pricing and support**
- [ ] [Billing](services/cost-management/billing.md), [Budgets](services/cost-management/budgets.md), [Cost Explorer](services/cost-management/cost-explorer.md), [Pricing Calculator](services/cost-management/pricing-calculator.md), [Savings Plans](services/cost-management/savings-plans.md), [Reserved Instances](services/cost-management/reserved-instances.md)

### AWS Certified Solutions Architect – Associate (SAA)

Check the [official exam guide](https://aws.amazon.com/certification/certified-solutions-architect-associate/) for the current domains.

**Design secure architectures**
- [ ] [IAM](services/security-identity-compliance/iam.md), [Organizations](services/security-identity-compliance/organizations.md), [Control Tower](services/management-governance/control-tower.md)
- [ ] [VPC](services/networking/vpc.md), [PrivateLink](services/networking/privatelink.md), [KMS](services/security-identity-compliance/kms.md), [Secrets Manager](services/security-identity-compliance/secrets-manager.md), [Cognito](services/security-identity-compliance/cognito.md), [WAF](services/security-identity-compliance/waf.md)

**Design resilient architectures**
- [ ] [Elastic Load Balancing](services/networking/elastic-load-balancing.md), [Auto Scaling](services/compute/auto-scaling.md), [Route 53](services/networking/route-53.md)
- [ ] [RDS](services/databases/rds.md) (Multi-AZ, read replicas), [Aurora](services/databases/aurora.md), [AWS Backup](services/storage/backup.md)
- [ ] [SQS](services/application-integration/sqs.md), [SNS](services/application-integration/sns.md), [EventBridge](services/application-integration/eventbridge.md), [Step Functions](services/application-integration/step-functions.md)

**Design high-performing architectures**
- [ ] [CloudFront](services/networking/cloudfront.md), [Global Accelerator](services/networking/global-accelerator.md), [ElastiCache](services/databases/elasticache.md)
- [ ] [EBS](services/storage/ebs.md), [EFS](services/storage/efs.md), [FSx](services/storage/fsx.md), [S3](services/storage/s3.md)
- [ ] [DynamoDB](services/databases/dynamodb.md), [Kinesis](services/analytics/kinesis.md), [Athena](services/analytics/athena.md), [Glue](services/analytics/glue.md)
- [ ] [Lambda](services/compute/lambda.md), [ECS](services/containers/ecs.md), [EKS](services/containers/eks.md), [Fargate](services/containers/fargate.md)

**Design cost-optimised architectures**
- [ ] [S3 Glacier](services/storage/s3-glacier.md), [Savings Plans](services/cost-management/savings-plans.md), [Reserved Instances](services/cost-management/reserved-instances.md), [Cost Explorer](services/cost-management/cost-explorer.md)
- [ ] Migration: [DMS](services/migration-transfer/database-migration-service.md), [DataSync](services/migration-transfer/datasync.md), [Application Migration Service](services/migration-transfer/application-migration-service.md), [Transit Gateway](services/networking/transit-gateway.md), [Direct Connect](services/networking/direct-connect.md)

---

## Path 3 – Job-ready cloud engineer

**Goal:** Be able to build, secure, monitor and automate real environments. Read **and build**.

| Week | Read | Build |
|------|------|-------|
| 1 | [IAM](services/security-identity-compliance/iam.md), [IAM Identity Center](services/security-identity-compliance/iam-identity-center.md), [AWS CLI](services/developer-tools/cli.md) | Set up SSO and the CLI. [Project 1](examples/billing-alarm-dashboard.md) |
| 2 | [VPC](services/networking/vpc.md), [EC2](services/compute/ec2.md), [Systems Manager](services/management-governance/systems-manager.md) | Build a VPC with public/private subnets; connect to EC2 with Session Manager |
| 3 | [S3](services/storage/s3.md), [CloudFront](services/networking/cloudfront.md), [Route 53](services/networking/route-53.md) | [Project 2: Static website](examples/static-website.md) – Console, then Terraform |
| 4 | [Elastic Load Balancing](services/networking/elastic-load-balancing.md), [Auto Scaling](services/compute/auto-scaling.md), [RDS](services/databases/rds.md) | [Project 5: Classic web app](examples/classic-web-app.md) with Terraform |
| 5 | [Lambda](services/compute/lambda.md), [API Gateway](services/networking/api-gateway.md), [DynamoDB](services/databases/dynamodb.md) | [Project 4: Serverless contact form](examples/serverless-contact-form.md) |
| 6 | [CloudWatch](services/management-governance/cloudwatch.md), [CloudTrail](services/management-governance/cloudtrail.md), [GuardDuty](services/security-identity-compliance/guardduty.md) | Alarms and dashboards for Projects 4 and 5 |
| 7 | [CloudFormation](services/management-governance/cloudformation.md), [CodePipeline](services/developer-tools/codepipeline.md), [CodeBuild](services/developer-tools/codebuild.md) | A pipeline that runs `terraform plan` on every push |
| 8 | [ECS](services/containers/ecs.md), [ECR](services/containers/ecr.md), [Fargate](services/containers/fargate.md) | Containerise Project 4's back end and run it on Fargate |

**Terraform tips along the way:**
- Keep each project in its own folder and Git repo.
- Use remote state (an S3 bucket with state locking) once you're comfortable.
- Always run `terraform plan` before `apply`, and `terraform destroy` when finished.

[← Back to the main index](README.md)
