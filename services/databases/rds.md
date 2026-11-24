# Amazon Relational Database Service (RDS)

**Category:** Databases  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

RDS runs a relational database (like MySQL, PostgreSQL or SQL Server) for you, handling setup, backups, patching and failover.

## Real-life comparison

Running your own database is like owning a car: you do the servicing, change the tyres and fix breakdowns. RDS is like a car lease with full maintenance – you still drive (design tables, write queries), but someone else keeps it running.

## What problem does it solve?

Installing a database on a server means you must patch it, take backups, test restores, set up a standby copy and replace failed disks. RDS does all of that, so you focus on your data.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **DB instance** | One database server managed by RDS. |
| **Engine** | The database software: MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Db2 (or Aurora). |
| **Instance class** | The size of the server, e.g. `db.t4g.micro`. |
| **Multi-AZ** | A standby copy in another AZ that takes over automatically if the main one fails. |
| **Read replica** | A read-only copy that takes reading work away from the main database. |
| **Automated backups** | Daily backups plus logs, so you can restore to any second in the retention period. |
| **Endpoint** | The address your app uses to connect. |
| **Subnet group** | The private subnets RDS can place the database in. |

## How it works (step by step)

1. You choose an engine (e.g. PostgreSQL) and an instance class.
2. You choose storage size and whether to use Multi-AZ.
3. You place it in **private subnets** of your VPC, with a security group.
4. RDS creates the database and gives you an **endpoint**.
5. Your app connects to the endpoint with a username and password (ideally from [Secrets Manager](../security-identity-compliance/secrets-manager.md)).
6. RDS takes automated backups and applies patches in a maintenance window you choose.

## When to use it

- Apps that need a traditional SQL database: online shops, booking systems, CRMs, WordPress.
- Moving an existing MySQL/PostgreSQL/SQL Server database to AWS.

## When NOT to use it (and what to use instead)

- **Massive scale with simple key lookups.** → [DynamoDB](dynamodb.md).
- **Analysing huge data sets for reports.** → [Redshift](redshift.md) or [Athena](../analytics/athena.md).
- **You need full control of the operating system or unsupported settings.** → Install it yourself on [EC2](../compute/ec2.md).

## Real-world example

**Scenario:** Hana runs an online furniture shop. Her MySQL database sits on the same EC2 server as her website.

**The problem:** Last month a disk failed and she lost two days of orders because the last backup was old.

**How RDS helps:** Hana moves the database to RDS for MySQL with Multi-AZ and 14 days of automated backups. If the main database fails, the standby takes over in about a minute or two, and she can restore to any point in the last 14 days.

**What it looks like:**

```
 Website (EC2, private subnet)
         │ port 3306
         ▼
 ┌──── RDS MySQL ────────────────────────┐
 │ Primary (AZ a) ══sync══► Standby (AZ b)│
 └───────────────────────────────────────┘
         │ automated backups
         ▼
     Snapshots (S3, managed by AWS)
```

## Try it yourself

> ⚠️ **Cost warning:** Small instance classes (such as `db.t4g.micro` or `db.t3.micro`) and some storage are in the Free Tier for new accounts, **single-AZ only**. Multi-AZ, bigger sizes and extra storage cost money. **Delete the database at the end.**

### Option A – Using the AWS Console (clicking in the website)

1. Open **RDS** → **Create database**.
2. Choose **Standard create**, engine **PostgreSQL** (or MySQL).
3. **Templates:** choose **Free tier** (or **Sandbox**).
4. **DB instance identifier:** `demo-db`.
5. **Credentials management:** choose **Managed in AWS Secrets Manager**.
6. **Instance configuration:** smallest burstable class offered.
7. **Connectivity:** your default VPC, **Public access: No**.
8. Open **Additional configuration** and set backup retention to **1 day**.
9. Click **Create database**. It takes 5–10 minutes.
10. Open `demo-db` and find its **Endpoint** on the **Connectivity & security** tab.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create a small PostgreSQL database with the password stored in Secrets Manager
aws rds create-db-instance --db-instance-identifier demo-db \
  --engine postgres --db-instance-class db.t4g.micro --allocated-storage 20 \
  --master-username dbadmin --manage-master-user-password \
  --no-publicly-accessible --backup-retention-period 1

# Check its status and endpoint
aws rds describe-db-instances --db-instance-identifier demo-db \
  --query 'DBInstances[0].[DBInstanceStatus,Endpoint.Address]'
```

### Option C – Using Terraform (infrastructure as code)

Written for the AWS provider `~> 6.0`.

```hcl
# A small private PostgreSQL database; the password is created and stored in Secrets Manager
resource "aws_db_instance" "demo" {
  identifier                  = "demo-db"
  engine                      = "postgres"
  instance_class              = "db.t4g.micro"
  allocated_storage           = 20
  username                    = "dbadmin"
  manage_master_user_password = true
  publicly_accessible         = false
  storage_encrypted           = true
  backup_retention_period     = 1
  skip_final_snapshot         = true # fine for a test, NOT for real data
}
```

### Clean up (delete what you made)

1. **RDS** → **Databases** → tick `demo-db` → **Actions** → **Delete**.
2. Untick **Create final snapshot** and tick the acknowledgement (only for test data!).
3. Type `delete me` and confirm.
4. Check **Snapshots** for any leftover manual snapshots and delete them.
5. Delete the secret RDS created in **Secrets Manager** if it isn't removed automatically.

## How much does it cost?

- **Instance hours** – by class, doubled for Multi-AZ.
- **Storage** – per GB per month, plus any provisioned IOPS.
- **Backups** – free up to the size of your database; extra is charged.
- **Data transfer** out of AWS.

Official pricing: <https://aws.amazon.com/rds/pricing/>

## Security tips

- **Never make the database publicly accessible.** Put it in private subnets.
- Only allow the app servers' **security group** on the database port.
- Turn on **encryption at rest** (can only be chosen at creation).
- Store the password in **Secrets Manager**, or use IAM database authentication.

## Common mistakes

- **Public access: Yes** "just to test" – bots will find it.
- **Forgetting Multi-AZ** for live systems.
- **Deleting without a final snapshot** on real data.
- **Stopped databases restart automatically after 7 days** – delete test ones instead.

## Works well with

- [EC2](../compute/ec2.md) and [Lambda](../compute/lambda.md) – connect to RDS.
- [Secrets Manager](../security-identity-compliance/secrets-manager.md) – stores and rotates the password.
- [Aurora](aurora.md) – AWS's higher-performance option within RDS.
- [Database Migration Service](../migration-transfer/database-migration-service.md) – moves existing databases into RDS.

## Quick check (test yourself)

1. What does Multi-AZ give you?
   <details><summary>Answer</summary>A standby copy in another AZ that takes over automatically if the primary fails.</details>
2. What is a read replica for?
   <details><summary>Answer</summary>Spreading out read traffic (and sometimes disaster recovery), not automatic failover for writes.</details>
3. Should an RDS database be publicly accessible?
   <details><summary>Answer</summary>Almost never. Keep it in private subnets.</details>

## Learn more

- [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- [Amazon RDS pricing](https://aws.amazon.com/rds/pricing/)
