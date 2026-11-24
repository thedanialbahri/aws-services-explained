# AWS Backup

**Category:** Storage  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

AWS Backup takes and manages backups of many AWS services from one place, on a schedule you choose.

## Real-life comparison

AWS Backup is like a cleaner with a weekly rota. Instead of remembering to tidy each room yourself, you write one rota ("kitchen Mondays, bathroom Thursdays") and it gets done automatically.

## What problem does it solve?

Without it, you'd set up backups separately for each service – EBS snapshots here, RDS backups there – and hope nobody forgot one. AWS Backup gives you one set of rules, one place to check, and reports showing what was backed up.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Backup plan** | Your rota: how often to back up and how long to keep backups. |
| **Backup rule** | One line in the plan, e.g. "daily at 1am, keep for 35 days". |
| **Backup vault** | A secure container where backups are stored. |
| **Recovery point** | One backup you can restore from. |
| **Resource assignment** | Which things to back up, e.g. "everything tagged `backup=daily`". |
| **Vault Lock** | Stops anyone – even admins – deleting backups early (protects against ransomware). |

## How it works (step by step)

1. You create a **backup vault**.
2. You create a **backup plan** with rules (how often, how long to keep).
3. You **assign resources** to the plan, often using tags.
4. AWS Backup runs the backups automatically and stores recovery points in the vault.
5. When needed, you **restore** a recovery point to create a new resource.

## When to use it

- Backing up EC2, EBS, RDS, DynamoDB, EFS, FSx and more with one policy.
- Meeting rules that say "keep backups for X days" and proving it.
- Copying backups to another Region or account for disaster recovery.

## When NOT to use it (and what to use instead)

- **Only one small service and the built-in backup is enough** (e.g. RDS automated backups). That may be simpler.
- **Moving data into AWS.** → Use [DataSync](../migration-transfer/datasync.md).

## Real-world example

**Scenario:** A small online shop runs EC2 servers and an RDS database.

**The problem:** Backups were set up by hand and one server was missed. When its disk failed, a week of data was lost.

**How AWS Backup helps:** The team tags everything important with `backup=daily` and creates one plan: daily backups kept for 35 days, monthly backups kept for a year, with copies sent to another Region.

**What it looks like:**

```
 Resources tagged backup=daily
   EC2 ─┐
   RDS ─┼──► Backup plan (daily, keep 35 days) ──► Backup vault ──copy──► Vault in another Region
   EFS ─┘
```

## Try it yourself

> ⚠️ **Cost warning:** You pay for backup storage (per GB per month) and restores. Back up something tiny and delete the recovery points at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Open **AWS Backup** in the Console.
2. Click **Create backup plan** → **Start with a template** → choose **Daily-35day-Retention**.
3. Give it a name and click **Create plan**.
4. Click **Assign resources**, give it a name, choose **Include specific resource types**, and select an EBS volume.
5. Click **Assign resources**.
6. To test now: go to **Protected resources** → **Create on-demand backup**, pick the volume, and start.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create a backup vault
aws backup create-backup-vault --backup-vault-name demo-vault

# Start a one-off backup of an EBS volume (replace ARNs and account ID)
aws backup start-backup-job --backup-vault-name demo-vault \
  --resource-arn arn:aws:ec2:eu-west-2:123456789012:volume/vol-0123456789abcdef0 \
  --iam-role-arn arn:aws:iam::123456789012:role/service-role/AWSBackupDefaultServiceRole
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# A vault to store backups
resource "aws_backup_vault" "demo" {
  name = "demo-vault"
}

# Daily backups at 01:00 UTC, kept for 35 days
resource "aws_backup_plan" "daily" {
  name = "daily-35-days"
  rule {
    rule_name         = "daily"
    target_vault_name = aws_backup_vault.demo.name
    schedule          = "cron(0 1 ? * * *)"
    lifecycle {
      delete_after = 35
    }
  }
}
```

### Clean up (delete what you made)

1. In the vault, delete each **recovery point**.
2. Delete the **resource assignment**, then the **backup plan**.
3. Delete the **backup vault** (it must be empty).

## How much does it cost?

- **Backup storage** – per GB per month (warm or cold storage).
- **Restores** – charged per GB for some services.
- **Cross-Region copies** – data transfer between Regions.

Official pricing: <https://aws.amazon.com/backup/pricing/>

## Security tips

- Use **Vault Lock** for important backups so they can't be deleted early.
- Copy backups to a separate account, so a hacked account can't delete them.
- Encrypt vaults with KMS keys.

## Common mistakes

- Never testing a restore. A backup you can't restore isn't a backup.
- Forgetting to tag new resources, so they're not included.

## Works well with

- [EBS](ebs.md), [EFS](efs.md), [RDS](../databases/rds.md), [DynamoDB](../databases/dynamodb.md) – common things to back up.
- [Organizations](../security-identity-compliance/organizations.md) – apply backup policies across many accounts.

## Quick check (test yourself)

1. What is a backup vault?
   <details><summary>Answer</summary>A secure container where recovery points (backups) are stored.</details>
2. How can you include new resources automatically?
   <details><summary>Answer</summary>Assign resources by tag, e.g. `backup=daily`.</details>
3. What protects backups from being deleted by an attacker?
   <details><summary>Answer</summary>Vault Lock, and copying backups to another account.</details>

## Learn more

- [AWS Backup Developer Guide](https://docs.aws.amazon.com/aws-backup/latest/devguide/whatisbackup.html)
- [AWS Backup pricing](https://aws.amazon.com/backup/pricing/)
