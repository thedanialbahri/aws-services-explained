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
| 📝 | **Planned** – page not written yet ([help write it!](CONTRIBUTING.md)) |
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

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| Amazon EC2 | 🟢 | Rent virtual servers by the hour or second | 📝 |
| AWS Lambda | 🟢 | Run small pieces of code without managing a server | 📝 |
| Amazon EC2 Auto Scaling | 🟢 | Adds or removes servers automatically as demand changes | 📝 |
| Amazon Lightsail | 🟢 | Simple, fixed-price virtual servers for small websites | 📝 |
| AWS Elastic Beanstalk | 🟡 | Upload your app code; AWS sets up the servers for you | 📝 |
| AWS Batch | 🟡 | Runs large numbers of background jobs in a queue | 📝 |
| AWS Outposts | 🔴 | AWS hardware installed in your own building | 📝 |
| AWS Wavelength | 🔴 | Runs apps inside mobile (5G) networks for very low delay | 📝 |
| AWS Local Zones | 🔴 | Small AWS sites in big cities, closer to users | 📝 |

### Containers

Services that run apps packaged as containers (a box holding an app and everything it needs to run).

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| Amazon ECS | 🟡 | AWS's own system for running containers | 📝 |
| Amazon EKS | 🔴 | Runs Kubernetes (a popular open-source container system) for you | 📝 |
| AWS Fargate | 🟡 | Runs containers without you managing any servers | 📝 |
| Amazon ECR | 🟡 | Stores your container images, like a library | 📝 |
| AWS App Runner | 🟡 | Turns your code or container into a running web app in a few clicks | 📝 |

### Storage

Services that keep your files and data.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| Amazon S3 | 🟢 | Stores any number of files, reachable from anywhere | 📝 |
| Amazon EBS | 🟢 | A virtual hard drive for an EC2 server | 📝 |
| Amazon EFS | 🟡 | A shared network drive many Linux servers can use at once | 📝 |
| Amazon S3 Glacier | 🟢 | Very cheap storage for files you rarely need | 📝 |
| Amazon FSx | 🔴 | Managed file systems for Windows, Lustre, NetApp and OpenZFS | 📝 |
| AWS Storage Gateway | 🟡 | Connects your office storage to AWS storage | 📝 |
| AWS Backup | 🟡 | Backs up many AWS services from one place | 📝 |
| AWS Snow Family | 🔴 | Physical devices posted to you to move huge amounts of data | 📝 |

### Databases

Services that store organised data your apps can search and update.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| Amazon RDS | 🟢 | Managed relational databases (MySQL, PostgreSQL, SQL Server and more) | 📝 |
| Amazon DynamoDB | 🟢 | Fast NoSQL database that scales without servers | 📝 |
| Amazon Aurora | 🟡 | AWS's own MySQL- and PostgreSQL-compatible database | 📝 |
| Amazon ElastiCache | 🟡 | In-memory cache that makes apps faster | 📝 |
| Amazon Redshift | 🟡 | Data warehouse for analysing large amounts of data | 📝 |
| Amazon MemoryDB | 🔴 | Durable in-memory database compatible with Redis/Valkey | 📝 |
| Amazon DocumentDB | 🔴 | Document database compatible with MongoDB | 📝 |
| Amazon Neptune | 🔴 | Graph database for data about connections (like a social network) | 📝 |
| Amazon Keyspaces | 🔴 | Managed database compatible with Apache Cassandra | 📝 |
| Amazon Timestream | 🔴 | Database for time-stamped data, like sensor readings | 📝 |

### Networking & content delivery

Services that connect things together and deliver content quickly.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| Amazon VPC | 🟢 | Your own private network inside AWS | 📝 |
| Amazon Route 53 | 🟢 | Domain names and DNS (the internet's phone book) | 📝 |
| Amazon CloudFront | 🟢 | Delivers your website and files fast from locations near users | 📝 |
| Elastic Load Balancing | 🟢 | Shares incoming traffic across several servers | 📝 |
| Amazon API Gateway | 🟡 | Creates and protects APIs (doors other programs use to talk to your app) | 📝 |
| AWS Site-to-Site VPN | 🟡 | Encrypted connection between your office and AWS over the internet | 📝 |
| AWS Direct Connect | 🔴 | Private physical cable from your building to AWS | 📝 |
| AWS Transit Gateway | 🔴 | A central hub that connects many networks together | 📝 |
| AWS PrivateLink | 🔴 | Reach services privately without using the public internet | 📝 |
| AWS Global Accelerator | 🔴 | Sends users over AWS's global network for faster, steadier connections | 📝 |

### Security, identity & compliance

Services that control access and protect your account and data.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| AWS IAM | 🟢 | Controls who can do what in your AWS account | 📝 |
| AWS IAM Identity Center | 🟢 | One login for people across many AWS accounts | 📝 |
| AWS Organizations | 🟡 | Manage many AWS accounts together | 📝 |
| Amazon Cognito | 🟡 | Sign-up and sign-in for your app's users | 📝 |
| AWS KMS | 🟡 | Creates and controls encryption keys | 📝 |
| AWS Secrets Manager | 🟡 | Stores passwords and API keys safely | 📝 |
| AWS Certificate Manager | 🟡 | Free SSL/TLS certificates (the padlock in your browser) | 📝 |
| AWS WAF | 🟡 | A web firewall that blocks bad web requests | 📝 |
| AWS Shield | 🟡 | Protects against DDoS attacks (floods of fake traffic) | 📝 |
| Amazon GuardDuty | 🟡 | Watches your account for suspicious activity | 📝 |
| Amazon Inspector | 🟡 | Scans servers, containers and Lambda for known weaknesses | 📝 |
| Amazon Macie | 🔴 | Finds sensitive data (like card numbers) in S3 | 📝 |
| AWS Security Hub | 🟡 | One dashboard for security findings across services | 📝 |
| Amazon Detective | 🔴 | Helps investigate the cause of a security problem | 📝 |
| AWS Firewall Manager | 🔴 | Sets firewall rules across many accounts at once | 📝 |
| AWS Artifact | 🟢 | Download AWS's compliance reports and agreements | 📝 |

### Management & governance

Services that monitor, record and organise what's happening in your account.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| Amazon CloudWatch | 🟢 | Collects metrics and logs, and sends alarms | 📝 |
| AWS CloudTrail | 🟢 | Records who did what in your account (an audit log) | 📝 |
| AWS Trusted Advisor | 🟢 | Checks your account and suggests improvements | 📝 |
| AWS Health Dashboard | 🟢 | Shows AWS problems that affect you | 📝 |
| AWS Config | 🟡 | Records settings over time and checks them against rules | 📝 |
| AWS Systems Manager | 🟡 | Manage, patch and connect to many servers from one place | 📝 |
| AWS CloudFormation | 🟡 | Builds AWS resources from template files (infrastructure as code) | 📝 |
| AWS Control Tower | 🔴 | Sets up a secure multi-account environment with guardrails | 📝 |
| AWS Service Catalog | 🔴 | A shop of approved resources teams can launch | 📝 |

### Cost management

Services that help you understand and control your bill.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| AWS Billing and Cost Management | 🟢 | Shows your bills and payments | 📝 |
| AWS Budgets | 🟢 | Sends alerts when spending goes over a limit | 📝 |
| AWS Cost Explorer | 🟢 | Charts of what you've spent and on what | 📝 |
| AWS Pricing Calculator | 🟢 | Estimates the cost of something before you build it | 📝 |
| Savings Plans | 🟡 | Lower prices in exchange for committing to spend over 1 or 3 years | 📝 |
| Reserved Instances | 🟡 | Lower prices for committing to specific resources over 1 or 3 years | 📝 |

### Developer tools

Services that help you write, test, build and release code.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| AWS CLI | 🟢 | Control AWS by typing commands | 📝 |
| AWS CloudShell | 🟢 | A terminal in your browser, already logged in to AWS | 📝 |
| AWS SDKs | 🟡 | Code libraries for using AWS from your own programs | 📝 |
| AWS CDK | 🟡 | Write infrastructure as code using programming languages | 📝 |
| AWS CodeCommit | 🟡 | Private Git repositories hosted by AWS | 📝 |
| AWS CodeBuild | 🟡 | Builds and tests your code automatically | 📝 |
| AWS CodeDeploy | 🟡 | Releases new versions of your app to servers | 📝 |
| AWS CodePipeline | 🟡 | Joins build, test and release steps into one automatic process | 📝 |
| AWS CodeArtifact | 🔴 | Stores software packages your code depends on | 📝 |
| AWS X-Ray | 🔴 | Traces requests through your app to find slow or broken parts | 📝 |
| AWS Cloud9 | 🟡 | Browser-based code editor | ⛔ 📝 <!-- TODO: verify --> |

### Application integration

Services that let different parts of an app send messages to each other.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| Amazon SQS | 🟢 | A queue that holds messages until a program is ready for them | 📝 |
| Amazon SNS | 🟢 | Sends one message to many subscribers (email, SMS, apps) | 📝 |
| Amazon EventBridge | 🟡 | Routes events between services based on rules | 📝 |
| AWS Step Functions | 🟡 | Joins steps into a visual workflow | 📝 |
| Amazon MQ | 🔴 | Managed message brokers (ActiveMQ and RabbitMQ) | 📝 |
| AWS AppSync | 🔴 | Managed GraphQL APIs for apps | 📝 |

### Analytics

Services that collect, process and make sense of data.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| Amazon Athena | 🟡 | Ask questions of files in S3 using SQL | 📝 |
| Amazon QuickSight | 🟡 | Dashboards and charts for business data | 📝 |
| Amazon Kinesis | 🟡 | Collects and processes data streams in real time | 📝 |
| AWS Glue | 🟡 | Finds, cleans and moves data between stores | 📝 |
| Amazon OpenSearch Service | 🟡 | Search and analyse logs and text | 📝 |
| Amazon EMR | 🔴 | Runs big data tools like Apache Spark | 📝 |
| AWS Lake Formation | 🔴 | Builds and secures a data lake | 📝 |
| Amazon MSK | 🔴 | Managed Apache Kafka for streaming data | 📝 |
| AWS Data Exchange | 🔴 | Find and subscribe to third-party data sets | 📝 |

### Machine learning & AI

Services that add AI to apps or help you build your own models.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| Amazon Bedrock | 🟡 | Use ready-made generative AI models through one API | 📝 |
| Amazon Q | 🟡 | AI assistant for work and for building on AWS | 📝 |
| Amazon Rekognition | 🟡 | Finds objects, text and faces in images and video | 📝 |
| Amazon Comprehend | 🟡 | Understands text, e.g. finds topics and feelings | 📝 |
| Amazon Polly | 🟢 | Turns text into speech | 📝 |
| Amazon Transcribe | 🟢 | Turns speech into text | 📝 |
| Amazon Translate | 🟢 | Translates text between languages | 📝 |
| Amazon Textract | 🟡 | Reads text and tables from scanned documents | 📝 |
| Amazon Lex | 🟡 | Builds chatbots and voice bots | 📝 |
| Amazon Kendra | 🔴 | Intelligent search across company documents | 📝 |
| Amazon Personalize | 🔴 | Product and content recommendations | 📝 |
| Amazon SageMaker | 🔴 | Build, train and run your own machine learning models | 📝 |
| Amazon Forecast | 🔴 | Predicts future values from past data | ⛔ 📝 |

### Migration & transfer

Services that move servers, databases and files into AWS.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| AWS Application Migration Service | 🟡 | Copies whole servers into AWS | 📝 |
| AWS Database Migration Service | 🟡 | Moves databases into AWS with little downtime | 📝 |
| AWS DataSync | 🟡 | Copies large amounts of files to and from AWS | 📝 |
| AWS Transfer Family | 🟡 | SFTP/FTP file transfer straight into S3 or EFS | 📝 |
| AWS Migration Hub | 🔴 | Tracks progress of a migration in one place | 📝 <!-- TODO: verify current status --> |

### End-user computing

Services that give people desktops and apps over the internet.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| Amazon WorkSpaces | 🟡 | Cloud desktops (Windows or Linux) you log in to from anywhere | 📝 |
| Amazon AppStream 2.0 | 🔴 | Streams individual desktop apps to a web browser | 📝 |

### Front-end web & mobile

Services for building and testing websites and mobile apps.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| AWS Amplify | 🟢 | Build and host web and mobile apps quickly | 📝 |
| AWS Device Farm | 🟡 | Test your app on real phones and browsers | 📝 |
| Amazon Location Service | 🟡 | Maps, addresses and tracking for your app | 📝 |

### Internet of Things (IoT)

Services that connect and manage physical devices like sensors.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| AWS IoT Core | 🟡 | Connects devices to AWS securely | 📝 |
| AWS IoT Greengrass | 🔴 | Runs AWS code on devices themselves | 📝 |
| AWS IoT SiteWise | 🔴 | Collects and monitors data from industrial equipment | 📝 |
| AWS IoT Events | 🔴 | Reacted to events from devices – **shut down May 2026** | ⛔ 📝 |

### Business applications

Ready-made apps for communication and customer service.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| Amazon SES | 🟢 | Sends and receives email from your app | 📝 |
| Amazon Connect | 🟡 | Cloud contact centre (phone and chat support) | 📝 |
| Amazon WorkMail | 🟡 | Business email and calendar – **shutting down** | ⛔ 📝 |
| Amazon Chime | 🟡 | Online meetings and chat – **shutting down** | ⛔ 📝 <!-- TODO: verify date --> |

### Media services

Services for video and live streaming.

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| AWS Elemental MediaConvert | 🟡 | Converts video files into formats for phones, TVs and the web | 📝 |
| Amazon IVS | 🟡 | Add live video streaming to your app | 📝 |
| Amazon Kinesis Video Streams | 🔴 | Streams video from cameras into AWS for processing | 📝 |
| Amazon Elastic Transcoder | 🟡 | Old video converter – **shut down November 2025**, use MediaConvert | ⛔ 📝 |

### Specialist (blockchain, quantum, satellite)

| Service | Level | What it does | Page |
|---------|-------|--------------|------|
| Amazon Managed Blockchain | 🔴 | Run blockchain networks without managing the servers | 📝 |
| Amazon Braket | 🔴 | Try quantum computing | 📝 |
| AWS Ground Station | 🔴 | Control satellites and download their data | 📝 |

> This index starts from the checklist in the project brief. The full list of current services is on the official [AWS products page](https://aws.amazon.com/products/). More services will be added category by category.

---

## 🧪 Hands-on examples

Small projects that join several services together. Coming soon in [`examples/`](examples/):

- Host a static website (S3 + CloudFront + Route 53)
- Serverless contact form (API Gateway + Lambda + DynamoDB + SES)
- Classic web app (VPC + EC2 + Application Load Balancer + RDS)
- Automatic image resizer (S3 + Lambda)
- Billing alarm and monitoring dashboard (Budgets + CloudWatch + SNS)

## 🤝 How to contribute

Found a mistake? Want to write a page? You're welcome to help, whatever your level.

Read [CONTRIBUTING.md](CONTRIBUTING.md) for the step-by-step guide. Every service page uses the same [template](templates/service-template.md).

## 📄 Licence

- **Code** (CLI commands, Terraform, scripts): [MIT](LICENSE)
- **Written content**: [CC BY 4.0](LICENSE)

## ⚠️ Disclaimer

*This is a community learning resource and is not official AWS documentation. AWS services and prices change, so always check the official docs.*

AWS and all related names are trademarks of Amazon.com, Inc. or its affiliates. This project is not affiliated with or endorsed by AWS.
