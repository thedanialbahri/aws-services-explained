# AWS Services Explained Simply

**Every AWS service in plain English: what it is, what it does, when to use it, and a real example of it being used.**

This is a free learning resource for:

- 🧑‍🎓 complete beginners who have never used the cloud
- 🛠️ people with IT support experience who want to move into cloud
- 📜 anyone studying for AWS certifications (Cloud Practitioner, Solutions Architect Associate)
- ⚡ engineers who need a quick refresher on a service

Every service page follows the same layout, takes about 5 minutes to read, and includes a hands-on "Try it yourself" section with clean-up steps.

> **Disclaimer:** *This is a community learning resource and is not official AWS documentation. AWS services and prices change, so always check the official docs.*

---

## 🚀 Start here

1. **New to the cloud?** Read [START-HERE.md](START-HERE.md) first. It explains the cloud, AWS, Regions, and how to set up a safe account.
2. **Not sure what to read next?** Follow a [learning path](LEARNING-PATHS.md).
3. **Stuck on a word?** Look it up in the [glossary](GLOSSARY.md).

## How to read this index

| Symbol | Meaning |
|--------|---------|
| 🟢 | **Beginner** – start here |
| 🟡 | **Intermediate** – read after the beginner services |
| 🔴 | **Advanced / specialist** – for specific jobs or deeper study |
| ✅ | **Page written** – first draft, still being checked against the AWS docs |
| ⛔ | **Closed to new customers or shutting down** |

---

## 📚 Services by category

- [Compute](#compute)
- [Containers](#containers)
- [Storage](#storage)
- [Databases](#databases)
- [Networking & content delivery](#networking--content-delivery)
- [Security, identity & compliance](#security-identity--compliance)
- [Management & governance](#management--governance)
- [Cost management](#cost-management)
- [Developer tools](#developer-tools)
- [Application integration](#application-integration)
- [Analytics](#analytics)
- [Machine learning & AI](#machine-learning--ai)
- [Migration & transfer](#migration--transfer)
- [End-user computing](#end-user-computing)
- [Front-end web & mobile](#front-end-web--mobile)
- [Internet of Things (IoT)](#internet-of-things-iot)
- [Business applications](#business-applications)
- [Media services](#media-services)
- [Specialist (blockchain, quantum, satellite)](#specialist-blockchain-quantum-satellite)

### Compute

Services that run your code and applications.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [Amazon EC2](services/compute/ec2.md) | 🟢 | Rent virtual servers by the hour or second | ✅ |
| [AWS Lambda](services/compute/lambda.md) | 🟢 | Run small pieces of code without managing a server | ✅ |
| [Amazon EC2 Auto Scaling](services/compute/auto-scaling.md) | 🟢 | Adds or removes servers automatically as demand changes | ✅ |
| [Amazon Lightsail](services/compute/lightsail.md) | 🟢 | Simple, fixed-price virtual servers for small websites | ✅ |
| [AWS Elastic Beanstalk](services/compute/elastic-beanstalk.md) | 🟡 | Upload your app code; AWS sets up the servers for you | ✅ |
| [AWS Batch](services/compute/batch.md) | 🟡 | Runs large numbers of background jobs in a queue | ✅ |
| [AWS Outposts](services/compute/outposts.md) | 🔴 | AWS hardware installed in your own building | ✅ |
| [AWS Wavelength](services/compute/wavelength.md) | 🔴 | Runs apps inside mobile (5G) networks for very low delay | ✅ |
| [AWS Local Zones](services/compute/local-zones.md) | 🔴 | Small AWS sites in big cities, closer to users | ✅ |

### Containers

Services that run apps packaged as containers (a box holding an app and everything it needs to run).

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [Amazon ECS](services/containers/ecs.md) | 🟡 | AWS's own system for running containers | ✅ |
| [Amazon EKS](services/containers/eks.md) | 🔴 | Runs Kubernetes (a popular open-source container system) for you | ✅ |
| [AWS Fargate](services/containers/fargate.md) | 🟡 | Runs containers without you managing any servers | ✅ |
| [Amazon ECR](services/containers/ecr.md) | 🟡 | Stores your container images, like a library | ✅ |
| [AWS App Runner](services/containers/app-runner.md) | 🟡 | Turns your code or container into a running web app in a few clicks | ✅ |

### Storage

Services that keep your files and data.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [Amazon S3](services/storage/s3.md) | 🟢 | Stores any number of files, reachable from anywhere | ✅ |
| [Amazon EBS](services/storage/ebs.md) | 🟢 | A virtual hard drive for an EC2 server | ✅ |
| [Amazon EFS](services/storage/efs.md) | 🟡 | A shared network drive many Linux servers can use at once | ✅ |
| [Amazon S3 Glacier](services/storage/s3-glacier.md) | 🟢 | Very cheap storage for files you rarely need | ✅ |
| [Amazon FSx](services/storage/fsx.md) | 🔴 | Managed file systems for Windows, Lustre, NetApp and OpenZFS | ✅ |
| [AWS Storage Gateway](services/storage/storage-gateway.md) | 🟡 | Connects your office storage to AWS storage | ✅ |
| [AWS Backup](services/storage/backup.md) | 🟡 | Backs up many AWS services from one place | ✅ |
| [AWS Snow Family](services/storage/snow-family.md) | 🔴 | Physical devices posted to you to move huge amounts of data | ⛔ |

### Databases

Services that store organised data your apps can search and update.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [Amazon RDS](services/databases/rds.md) | 🟢 | Managed relational databases (MySQL, PostgreSQL, SQL Server and more) | ✅ |
| [Amazon DynamoDB](services/databases/dynamodb.md) | 🟢 | Fast NoSQL database that scales without servers | ✅ |
| [Amazon Aurora](services/databases/aurora.md) | 🟡 | AWS's own MySQL- and PostgreSQL-compatible database | ✅ |
| [Amazon ElastiCache](services/databases/elasticache.md) | 🟡 | In-memory cache that makes apps faster | ✅ |
| [Amazon Redshift](services/databases/redshift.md) | 🟡 | Data warehouse for analysing large amounts of data | ✅ |
| [Amazon MemoryDB](services/databases/memorydb.md) | 🔴 | Durable in-memory database compatible with Redis/Valkey | ✅ |
| [Amazon DocumentDB](services/databases/documentdb.md) | 🔴 | Document database compatible with MongoDB | ✅ |
| [Amazon Neptune](services/databases/neptune.md) | 🔴 | Graph database for data about connections (like a social network) | ✅ |
| [Amazon Keyspaces](services/databases/keyspaces.md) | 🔴 | Managed database compatible with Apache Cassandra | ✅ |
| [Amazon Timestream](services/databases/timestream.md) | 🔴 | Database for time-stamped data, like sensor readings | ✅ |

### Networking & content delivery

Services that connect things together and deliver content quickly.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [Amazon VPC](services/networking/vpc.md) | 🟢 | Your own private network inside AWS | ✅ |
| [Amazon Route 53](services/networking/route-53.md) | 🟢 | Domain names and DNS (the internet's phone book) | ✅ |
| [Amazon CloudFront](services/networking/cloudfront.md) | 🟢 | Delivers your website and files fast from locations near users | ✅ |
| [Elastic Load Balancing](services/networking/elastic-load-balancing.md) | 🟢 | Shares incoming traffic across several servers | ✅ |
| [Amazon API Gateway](services/networking/api-gateway.md) | 🟡 | Creates and protects APIs (doors other programs use to talk to your app) | ✅ |
| [AWS Site-to-Site VPN](services/networking/site-to-site-vpn.md) | 🟡 | Encrypted connection between your office and AWS over the internet | ✅ |
| [AWS Direct Connect](services/networking/direct-connect.md) | 🔴 | Private physical cable from your building to AWS | ✅ |
| [AWS Transit Gateway](services/networking/transit-gateway.md) | 🔴 | A central hub that connects many networks together | ✅ |
| [AWS PrivateLink](services/networking/privatelink.md) | 🔴 | Reach services privately without using the public internet | ✅ |
| [AWS Global Accelerator](services/networking/global-accelerator.md) | 🔴 | Sends users over AWS's global network for faster, steadier connections | ✅ |

### Security, identity & compliance

Services that control access and protect your account and data.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [AWS IAM](services/security-identity-compliance/iam.md) | 🟢 | Controls who can do what in your AWS account | ✅ |
| [AWS IAM Identity Center](services/security-identity-compliance/iam-identity-center.md) | 🟢 | One login for people across many AWS accounts | ✅ |
| [AWS Organizations](services/security-identity-compliance/organizations.md) | 🟡 | Manage many AWS accounts together | ✅ |
| [Amazon Cognito](services/security-identity-compliance/cognito.md) | 🟡 | Sign-up and sign-in for your app's users | ✅ |
| [AWS KMS](services/security-identity-compliance/kms.md) | 🟡 | Creates and controls encryption keys | ✅ |
| [AWS Secrets Manager](services/security-identity-compliance/secrets-manager.md) | 🟡 | Stores passwords and API keys safely | ✅ |
| [AWS Certificate Manager](services/security-identity-compliance/certificate-manager.md) | 🟡 | Free SSL/TLS certificates (the padlock in your browser) | ✅ |
| [AWS WAF](services/security-identity-compliance/waf.md) | 🟡 | A web firewall that blocks bad web requests | ✅ |
| [AWS Shield](services/security-identity-compliance/shield.md) | 🟡 | Protects against DDoS attacks (floods of fake traffic) | ✅ |
| [Amazon GuardDuty](services/security-identity-compliance/guardduty.md) | 🟡 | Watches your account for suspicious activity | ✅ |
| [Amazon Inspector](services/security-identity-compliance/inspector.md) | 🟡 | Scans servers, containers and Lambda for known weaknesses | ✅ |
| [Amazon Macie](services/security-identity-compliance/macie.md) | 🔴 | Finds sensitive data (like card numbers) in S3 | ✅ |
| [AWS Security Hub](services/security-identity-compliance/security-hub.md) | 🟡 | One dashboard for security findings across services | ✅ |
| [Amazon Detective](services/security-identity-compliance/detective.md) | 🔴 | Helps investigate the cause of a security problem | ✅ |
| [AWS Firewall Manager](services/security-identity-compliance/firewall-manager.md) | 🔴 | Sets firewall rules across many accounts at once | ✅ |
| [AWS Artifact](services/security-identity-compliance/artifact.md) | 🟢 | Download AWS's compliance reports and agreements | ✅ |

### Management & governance

Services that monitor, record and organise what's happening in your account.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [Amazon CloudWatch](services/management-governance/cloudwatch.md) | 🟢 | Collects metrics and logs, and sends alarms | ✅ |
| [AWS CloudTrail](services/management-governance/cloudtrail.md) | 🟢 | Records who did what in your account (an audit log) | ✅ |
| [AWS Trusted Advisor](services/management-governance/trusted-advisor.md) | 🟢 | Checks your account and suggests improvements | ✅ |
| [AWS Health Dashboard](services/management-governance/health-dashboard.md) | 🟢 | Shows AWS problems that affect you | ✅ |
| [AWS Config](services/management-governance/config.md) | 🟡 | Records settings over time and checks them against rules | ✅ |
| [AWS Systems Manager](services/management-governance/systems-manager.md) | 🟡 | Manage, patch and connect to many servers from one place | ✅ |
| [AWS CloudFormation](services/management-governance/cloudformation.md) | 🟡 | Builds AWS resources from template files (infrastructure as code) | ✅ |
| [AWS Control Tower](services/management-governance/control-tower.md) | 🔴 | Sets up a secure multi-account environment with guardrails | ✅ |
| [AWS Service Catalog](services/management-governance/service-catalog.md) | 🔴 | A shop of approved resources teams can launch | ✅ |

### Cost management

Services that help you understand and control your bill.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [AWS Billing and Cost Management](services/cost-management/billing.md) | 🟢 | Shows your bills and payments | ✅ |
| [AWS Budgets](services/cost-management/budgets.md) | 🟢 | Sends alerts when spending goes over a limit | ✅ |
| [AWS Cost Explorer](services/cost-management/cost-explorer.md) | 🟢 | Charts of what you've spent and on what | ✅ |
| [AWS Pricing Calculator](services/cost-management/pricing-calculator.md) | 🟢 | Estimates the cost of something before you build it | ✅ |
| [Savings Plans](services/cost-management/savings-plans.md) | 🟡 | Lower prices in exchange for committing to spend over 1 or 3 years | ✅ |
| [Reserved Instances](services/cost-management/reserved-instances.md) | 🟡 | Lower prices for committing to specific resources over 1 or 3 years | ✅ |

### Developer tools

Services that help you write, test, build and release code.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [AWS CLI](services/developer-tools/cli.md) | 🟢 | Control AWS by typing commands | ✅ |
| [AWS CloudShell](services/developer-tools/cloudshell.md) | 🟢 | A terminal in your browser, already logged in to AWS | ✅ |
| [AWS SDKs](services/developer-tools/sdks.md) | 🟡 | Code libraries for using AWS from your own programs | ✅ |
| [AWS CDK](services/developer-tools/cdk.md) | 🟡 | Write infrastructure as code using programming languages | ✅ |
| [AWS CodeCommit](services/developer-tools/codecommit.md) | 🟡 | Private Git repositories hosted by AWS | ✅ |
| [AWS CodeBuild](services/developer-tools/codebuild.md) | 🟡 | Builds and tests your code automatically | ✅ |
| [AWS CodeDeploy](services/developer-tools/codedeploy.md) | 🟡 | Releases new versions of your app to servers | ✅ |
| [AWS CodePipeline](services/developer-tools/codepipeline.md) | 🟡 | Joins build, test and release steps into one automatic process | ✅ |
| [AWS CodeArtifact](services/developer-tools/codeartifact.md) | 🔴 | Stores software packages your code depends on | ✅ |
| [AWS X-Ray](services/developer-tools/x-ray.md) | 🔴 | Traces requests through your app to find slow or broken parts | ✅ |
| [AWS Cloud9](services/developer-tools/cloud9.md) | 🟡 | Browser-based code editor | ⛔ |

### Application integration

Services that let different parts of an app send messages to each other.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [Amazon SQS](services/application-integration/sqs.md) | 🟢 | A queue that holds messages until a program is ready for them | ✅ |
| [Amazon SNS](services/application-integration/sns.md) | 🟢 | Sends one message to many subscribers (email, SMS, apps) | ✅ |
| [Amazon EventBridge](services/application-integration/eventbridge.md) | 🟡 | Routes events between services based on rules | ✅ |
| [AWS Step Functions](services/application-integration/step-functions.md) | 🟡 | Joins steps into a visual workflow | ✅ |
| [Amazon MQ](services/application-integration/mq.md) | 🔴 | Managed message brokers (ActiveMQ and RabbitMQ) | ✅ |
| [AWS AppSync](services/application-integration/appsync.md) | 🔴 | Managed GraphQL APIs for apps | ✅ |

### Analytics

Services that collect, process and make sense of data.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [Amazon Athena](services/analytics/athena.md) | 🟡 | Ask questions of files in S3 using SQL | ✅ |
| [Amazon QuickSight](services/analytics/quicksight.md) | 🟡 | Dashboards and charts for business data | ✅ |
| [Amazon Kinesis](services/analytics/kinesis.md) | 🟡 | Collects and processes data streams in real time | ✅ |
| [AWS Glue](services/analytics/glue.md) | 🟡 | Finds, cleans and moves data between stores | ✅ |
| [Amazon OpenSearch Service](services/analytics/opensearch.md) | 🟡 | Search and analyse logs and text | ✅ |
| [Amazon EMR](services/analytics/emr.md) | 🔴 | Runs big data tools like Apache Spark | ✅ |
| [AWS Lake Formation](services/analytics/lake-formation.md) | 🔴 | Builds and secures a data lake | ✅ |
| [Amazon MSK](services/analytics/msk.md) | 🔴 | Managed Apache Kafka for streaming data | ✅ |
| [AWS Data Exchange](services/analytics/data-exchange.md) | 🔴 | Find and subscribe to third-party data sets | ✅ |

### Machine learning & AI

Services that add AI to apps or help you build your own models.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [Amazon Bedrock](services/machine-learning-ai/bedrock.md) | 🟡 | Use ready-made generative AI models through one API | ✅ |
| [Amazon Q](services/machine-learning-ai/amazon-q.md) | 🟡 | AI assistant for work and for building on AWS | ✅ |
| [Amazon Rekognition](services/machine-learning-ai/rekognition.md) | 🟡 | Finds objects, text and faces in images and video | ✅ |
| [Amazon Comprehend](services/machine-learning-ai/comprehend.md) | 🟡 | Understands text, e.g. finds topics and feelings | ✅ |
| [Amazon Polly](services/machine-learning-ai/polly.md) | 🟢 | Turns text into speech | ✅ |
| [Amazon Transcribe](services/machine-learning-ai/transcribe.md) | 🟢 | Turns speech into text | ✅ |
| [Amazon Translate](services/machine-learning-ai/translate.md) | 🟢 | Translates text between languages | ✅ |
| [Amazon Textract](services/machine-learning-ai/textract.md) | 🟡 | Reads text and tables from scanned documents | ✅ |
| [Amazon Lex](services/machine-learning-ai/lex.md) | 🟡 | Builds chatbots and voice bots | ✅ |
| [Amazon Kendra](services/machine-learning-ai/kendra.md) | 🔴 | Intelligent search across company documents | ✅ |
| [Amazon Personalize](services/machine-learning-ai/personalize.md) | 🔴 | Product and content recommendations | ✅ |
| [Amazon SageMaker](services/machine-learning-ai/sagemaker.md) | 🔴 | Build, train and run your own machine learning models | ✅ |
| [Amazon Forecast](services/machine-learning-ai/forecast.md) | 🔴 | Predicts future values from past data | ⛔ |

### Migration & transfer

Services that move servers, databases and files into AWS.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [AWS Application Migration Service](services/migration-transfer/application-migration-service.md) | 🟡 | Copies whole servers into AWS | ✅ |
| [AWS Database Migration Service](services/migration-transfer/database-migration-service.md) | 🟡 | Moves databases into AWS with little downtime | ✅ |
| [AWS DataSync](services/migration-transfer/datasync.md) | 🟡 | Copies large amounts of files to and from AWS | ✅ |
| [AWS Transfer Family](services/migration-transfer/transfer-family.md) | 🟡 | SFTP/FTP file transfer straight into S3 or EFS | ✅ |
| [AWS Migration Hub](services/migration-transfer/migration-hub.md) | 🔴 | Tracks progress of a migration in one place | ✅ |

### End-user computing

Services that give people desktops and apps over the internet.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [Amazon WorkSpaces](services/end-user-computing/workspaces.md) | 🟡 | Cloud desktops (Windows or Linux) you log in to from anywhere | ✅ |
| [Amazon AppStream 2.0](services/end-user-computing/appstream.md) | 🔴 | Streams individual desktop apps to a web browser | ✅ |

### Front-end web & mobile

Services for building and testing websites and mobile apps.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [AWS Amplify](services/front-end-web-mobile/amplify.md) | 🟢 | Build and host web and mobile apps quickly | ✅ |
| [AWS Device Farm](services/front-end-web-mobile/device-farm.md) | 🟡 | Test your app on real phones and browsers | ✅ |
| [Amazon Location Service](services/front-end-web-mobile/location-service.md) | 🟡 | Maps, addresses and tracking for your app | ✅ |

### Internet of Things (IoT)

Services that connect and manage physical devices like sensors.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [AWS IoT Core](services/iot/iot-core.md) | 🟡 | Connects devices to AWS securely | ✅ |
| [AWS IoT Greengrass](services/iot/iot-greengrass.md) | 🔴 | Runs AWS code on devices themselves | ✅ |
| [AWS IoT SiteWise](services/iot/iot-sitewise.md) | 🔴 | Collects and monitors data from industrial equipment | ✅ |
| [AWS IoT Events](services/iot/iot-events.md) | 🔴 | Reacted to events from devices – **shut down May 2026** | ⛔ |

### Business applications

Ready-made apps for communication and customer service.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [Amazon SES](services/business-applications/ses.md) | 🟢 | Sends and receives email from your app | ✅ |
| [Amazon Connect](services/business-applications/connect.md) | 🟡 | Cloud contact centre (phone and chat support) | ✅ |
| [Amazon WorkMail](services/business-applications/workmail.md) | 🟡 | Business email and calendar – **shutting down** | ⛔ |
| [Amazon Chime](services/business-applications/chime.md) | 🟡 | Online meetings and chat – **shutting down** | ⛔ |

### Media services

Services for video and live streaming.

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [AWS Elemental MediaConvert](services/media-services/mediaconvert.md) | 🟡 | Converts video files into formats for phones, TVs and the web | ✅ |
| [Amazon IVS](services/media-services/ivs.md) | 🟡 | Add live video streaming to your app | ✅ |
| [Amazon Kinesis Video Streams](services/media-services/kinesis-video-streams.md) | 🔴 | Streams video from cameras into AWS for processing | ✅ |
| [Amazon Elastic Transcoder](services/media-services/elastic-transcoder.md) | 🟡 | Old video converter – **shut down November 2025**, use MediaConvert | ⛔ |

### Specialist (blockchain, quantum, satellite)

| Service | Level | What it does | Status |
|---------|-------|--------------|------|
| [Amazon Managed Blockchain](services/specialist/managed-blockchain.md) | 🔴 | Run blockchain networks without managing the servers | ✅ |
| [Amazon Braket](services/specialist/braket.md) | 🔴 | Try quantum computing | ✅ |
| [AWS Ground Station](services/specialist/ground-station.md) | 🔴 | Control satellites and download their data | ✅ |

> This index starts from the checklist in the project brief. The full list of current services is on the official [AWS products page](https://aws.amazon.com/products/). More services will be added category by category.

---

## 🧪 Hands-on examples

Small projects that join several services together (see [`examples/`](examples/README.md)):

1. [Billing alarm and monitoring dashboard](examples/billing-alarm-dashboard.md) (Budgets + CloudWatch + SNS) – **do this first**
2. [Host a static website](examples/static-website.md) (S3 + CloudFront + Route 53)
3. [Automatic image resizer](examples/image-resizer.md) (S3 + Lambda)
4. [Serverless contact form](examples/serverless-contact-form.md) (API Gateway + Lambda + DynamoDB + SES)
5. [Classic web app](examples/classic-web-app.md) (VPC + EC2 + Application Load Balancer + RDS)

## 🔎 Status of this content

- Every page is a **first draft** written on 2026-11-24. Each page's "Last checked" line says it still needs a human check against the AWS docs.
- Places where a fact needs confirming are marked `<!-- TODO: verify -->` in the page source.
- CLI and Terraform examples are written for the AWS provider `~> 6.0` but haven't all been run yet. Run `terraform plan` first, and please [open an issue](../../issues) if something is wrong.

## 🤝 How to contribute

Found a mistake? Want to write a page? You're welcome to help, whatever your level.

Read [CONTRIBUTING.md](CONTRIBUTING.md) for the step-by-step guide. Every service page uses the same [template](templates/service-template.md).

## 📄 Licence

- **Code** (CLI commands, Terraform, scripts): [MIT](LICENSE)
- **Written content**: [CC BY 4.0](LICENSE)

## ⚠️ Disclaimer

*This is a community learning resource and is not official AWS documentation. AWS services and prices change, so always check the official docs.*

AWS and all related names are trademarks of Amazon.com, Inc. or its affiliates. This project is not affiliated with or endorsed by AWS.
