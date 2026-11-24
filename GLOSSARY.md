# Glossary

Every technical word used in this repo, A–Z, in plain English. Each links to the page where it matters most.

[A](#a) · [B](#b) · [C](#c) · [D](#d) · [E](#e) · [F](#f) · [G](#g) · [H](#h) · [I](#i) · [J](#j) · [K](#k) · [L](#l) · [M](#m) · [N](#n) · [O](#o) · [P](#p) · [Q](#q) · [R](#r) · [S](#s) · [T](#t) · [U](#u) · [V](#v) · [W](#w)

## A

- **Access key** – A key ID and secret that programs use to sign in to AWS. Treat it like a password. → [IAM](services/security-identity-compliance/iam.md)
- **Alarm** – Watches a metric and acts (e.g. sends an email) when it crosses a limit. → [CloudWatch](services/management-governance/cloudwatch.md)
- **Alias record** – A Route 53 record that points a name at an AWS resource. → [Route 53](services/networking/route-53.md)
- **AMI (Amazon Machine Image)** – A template with an operating system used to start EC2 servers. → [EC2](services/compute/ec2.md)
- **API** – A way for programs to talk to each other, usually over web addresses. → [API Gateway](services/networking/api-gateway.md)
- **ARN (Amazon Resource Name)** – The unique ID of an AWS resource, e.g. `arn:aws:s3:::my-bucket`. → [IAM](services/security-identity-compliance/iam.md)
- **Auto Scaling group** – A group of EC2 servers that grows and shrinks automatically. → [Auto Scaling](services/compute/auto-scaling.md)
- **Availability Zone (AZ)** – One or more separate data centres inside a Region. → [START-HERE](START-HERE.md#3-how-aws-is-organised-regions-availability-zones-and-edge-locations)

## B

- **Bucket** – A container for files in S3. → [S3](services/storage/s3.md)
- **Bucket policy** – JSON rules saying who can use an S3 bucket. → [S3](services/storage/s3.md)
- **Budget** – A spending limit that sends alerts. → [Budgets](services/cost-management/budgets.md)

## C

- **Cache** – A fast, temporary copy of data kept close to where it's needed. → [CloudFront](services/networking/cloudfront.md), [ElastiCache](services/databases/elasticache.md)
- **CDN (Content Delivery Network)** – Servers around the world that keep copies of content near users. → [CloudFront](services/networking/cloudfront.md)
- **CI/CD** – Automatically building, testing and releasing code on every change. → [CodePipeline](services/developer-tools/codepipeline.md)
- **CIDR block** – A range of IP addresses, e.g. `10.0.0.0/16`. → [VPC](services/networking/vpc.md)
- **CLI (Command Line Interface)** – Controlling AWS by typing commands. → [AWS CLI](services/developer-tools/cli.md)
- **Cloud** – Using someone else's computers over the internet instead of your own. → [START-HERE](START-HERE.md)
- **Cold start** – A short delay when a Lambda function runs after a quiet period. → [Lambda](services/compute/lambda.md)
- **Container** – An app packaged with everything it needs to run anywhere. → [Containers](services/containers/README.md)
- **CVE** – The ID of a publicly known software vulnerability. → [Inspector](services/security-identity-compliance/inspector.md)

## D

- **Data lake** – One big store of raw and processed data, usually in S3. → [Lake Formation](services/analytics/lake-formation.md)
- **Data warehouse** – A database designed for reports and analysis. → [Redshift](services/databases/redshift.md)
- **DDoS** – An attack that floods a service with traffic to knock it offline. → [Shield](services/security-identity-compliance/shield.md)
- **Dead-letter queue (DLQ)** – Where messages go after failing too many times. → [SQS](services/application-integration/sqs.md)
- **DNS** – The system that turns names like example.com into IP addresses. → [Route 53](services/networking/route-53.md)
- **Docker** – The most popular tool for building and running containers. → [Containers](services/containers/README.md)

## E

- **Edge location** – A small AWS site in a city, used to deliver content quickly. → [START-HERE](START-HERE.md#edge-location)
- **Encryption** – Scrambling data so only someone with the key can read it. → [KMS](services/security-identity-compliance/kms.md)
- **Endpoint** – An address you connect to, e.g. a database endpoint. → [RDS](services/databases/rds.md)
- **ETL** – Extract, transform, load: moving and cleaning data. → [Glue](services/analytics/glue.md)
- **Event** – A message saying something happened. → [EventBridge](services/application-integration/eventbridge.md)

## F

- **Fan-out** – One message delivered to many subscribers. → [SNS](services/application-integration/sns.md)
- **FIFO** – First in, first out – strict order. → [SQS](services/application-integration/sqs.md)
- **Free Tier** – Free usage allowances for AWS accounts. → [START-HERE](START-HERE.md#5-create-your-aws-account-safely)

## G

- **Generative AI** – AI that creates new content from a prompt. → [Bedrock](services/machine-learning-ai/bedrock.md)
- **Guardrail** – A rule that limits what can be done or said. → [Control Tower](services/management-governance/control-tower.md), [Bedrock](services/machine-learning-ai/bedrock.md)

## H

- **Health check** – A regular test to see if something is working. → [Elastic Load Balancing](services/networking/elastic-load-balancing.md)
- **Hosted zone** – The container for one domain's DNS records. → [Route 53](services/networking/route-53.md)
- **HTTPS** – Encrypted web traffic (the padlock). → [Certificate Manager](services/security-identity-compliance/certificate-manager.md)

## I

- **IaC (infrastructure as code)** – Describing infrastructure in files so a tool can build it. → [CloudFormation](services/management-governance/cloudformation.md)
- **IAM role** – An identity with permissions but no password, used temporarily. → [IAM](services/security-identity-compliance/iam.md)
- **Instance** – One virtual server. → [EC2](services/compute/ec2.md)
- **Instance type** – The size of a server (CPU and memory). → [EC2](services/compute/ec2.md)
- **Internet gateway** – The door between a VPC and the internet. → [VPC](services/networking/vpc.md)
- **IOPS** – How many disk reads and writes per second. → [EBS](services/storage/ebs.md)

## J

- **JSON** – A simple text format for data, used in policies and APIs. → [IAM](services/security-identity-compliance/iam.md)

## K

- **Key pair** – Keys used to log in to a server securely over SSH. → [EC2](services/compute/ec2.md)
- **Kubernetes** – An open-source system for running containers. → [EKS](services/containers/eks.md)

## L

- **Latency** – Delay; the time data takes to travel. → [Local Zones](services/compute/local-zones.md)
- **Least privilege** – Giving only the permissions needed. → [IAM](services/security-identity-compliance/iam.md)
- **Lifecycle rule** – An automatic rule to move or delete old files. → [S3](services/storage/s3.md)
- **Load balancer** – Shares traffic across several servers. → [Elastic Load Balancing](services/networking/elastic-load-balancing.md)

## M

- **Metric** – A number measured over time. → [CloudWatch](services/management-governance/cloudwatch.md)
- **MFA (multi-factor authentication)** – Needing a password plus a code to log in. → [START-HERE](START-HERE.md#step-3--turn-on-mfa-for-the-root-user)
- **MQTT** – A lightweight messaging protocol for devices. → [IoT Core](services/iot/iot-core.md)
- **Multi-AZ** – A standby copy in another Availability Zone. → [RDS](services/databases/rds.md)

## N

- **NAT gateway** – Lets private servers reach the internet without being reachable from it. → [VPC](services/networking/vpc.md)
- **Network ACL** – A stateless firewall around a subnet. → [VPC](services/networking/vpc.md)
- **NoSQL** – Databases that don't use fixed tables, e.g. key-value. → [DynamoDB](services/databases/dynamodb.md)

## O

- **OAC (Origin Access Control)** – Lets CloudFront read a private S3 bucket. → [CloudFront](services/networking/cloudfront.md)
- **Object** – One file stored in S3. → [S3](services/storage/s3.md)
- **On-demand** – Pay as you go, with no commitment. → [Savings Plans](services/cost-management/savings-plans.md)
- **Origin** – Where CloudFront gets the original files. → [CloudFront](services/networking/cloudfront.md)

## P

- **Partition key** – The main key used to store and find a DynamoDB item. → [DynamoDB](services/databases/dynamodb.md)
- **Policy** – A JSON document listing what's allowed or denied. → [IAM](services/security-identity-compliance/iam.md)
- **Private subnet** – A subnet with no direct route from the internet. → [VPC](services/networking/vpc.md)
- **Prompt** – The instruction you give an AI model. → [Bedrock](services/machine-learning-ai/bedrock.md)
- **Public subnet** – A subnet with a route to the internet gateway. → [VPC](services/networking/vpc.md)

## Q

- **Queue** – A waiting line for messages. → [SQS](services/application-integration/sqs.md)

## R

- **Read replica** – A read-only copy of a database. → [RDS](services/databases/rds.md)
- **Region** – A geographical area with several AZs, e.g. London `eu-west-2`. → [START-HERE](START-HERE.md#region)
- **Relational database** – A database of linked tables queried with SQL. → [RDS](services/databases/rds.md)
- **Root user** – The account owner login that can do anything. Lock it away. → [START-HERE](START-HERE.md#step-4--dont-use-the-root-user-day-to-day)
- **Route table** – Rules saying where network traffic goes. → [VPC](services/networking/vpc.md)

## S

- **SCP (service control policy)** – Sets the maximum permissions for accounts in an organisation. → [Organizations](services/security-identity-compliance/organizations.md)
- **SDK** – Code libraries for using AWS from your programs. → [SDKs](services/developer-tools/sdks.md)
- **Security group** – A stateful firewall around a resource. → [VPC](services/networking/vpc.md)
- **Serverless** – You don't manage any servers; AWS does. → [Lambda](services/compute/lambda.md)
- **Shared responsibility model** – Who looks after what: AWS or you. → [START-HERE](START-HERE.md#4-who-looks-after-what-the-shared-responsibility-model)
- **Snapshot** – A point-in-time backup copy. → [EBS](services/storage/ebs.md)
- **Spot Instance** – Spare EC2 capacity at a big discount that AWS can take back. → [EC2](services/compute/ec2.md)
- **SQL** – The standard language for asking databases questions. → [Athena](services/analytics/athena.md)
- **SSO (single sign-on)** – One login for many systems. → [IAM Identity Center](services/security-identity-compliance/iam-identity-center.md)
- **Stack** – Resources created together from a template. → [CloudFormation](services/management-governance/cloudformation.md)
- **Storage class** – A price-and-speed level for S3 objects. → [S3 Glacier](services/storage/s3-glacier.md)
- **Subnet** – A smaller section of a VPC in one AZ. → [VPC](services/networking/vpc.md)

## T

- **Tag** – A label (key and value) you attach to resources, e.g. `Project=learning`. → [Cost management](services/cost-management/README.md)
- **Target group** – The servers a load balancer sends traffic to. → [Elastic Load Balancing](services/networking/elastic-load-balancing.md)
- **Terraform** – A popular infrastructure-as-code tool that works with many clouds. → [CloudFormation](services/management-governance/cloudformation.md)
- **Token** – A digital pass after sign-in, or a chunk of text for AI models. → [Cognito](services/security-identity-compliance/cognito.md), [Bedrock](services/machine-learning-ai/bedrock.md)
- **Topic** – A named channel for messages. → [SNS](services/application-integration/sns.md)
- **TTL (time to live)** – How long something is kept before it expires. → [Route 53](services/networking/route-53.md)

## U

- **User data** – A script that runs when an EC2 server first starts. → [EC2](services/compute/ec2.md)

## V

- **Versioning** – Keeping old copies of files when they change. → [S3](services/storage/s3.md)
- **Visibility timeout** – How long a received SQS message stays hidden. → [SQS](services/application-integration/sqs.md)
- **Volume** – A virtual disk. → [EBS](services/storage/ebs.md)
- **VPC endpoint** – A private door from your VPC to a service. → [PrivateLink](services/networking/privatelink.md)
- **VPN** – An encrypted connection over a public network. → [Site-to-Site VPN](services/networking/site-to-site-vpn.md)

## W

- **Web ACL** – A set of WAF rules. → [WAF](services/security-identity-compliance/waf.md)

[← Back to the main index](README.md)
