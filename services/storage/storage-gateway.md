# AWS Storage Gateway

**Category:** Storage  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Storage Gateway connects servers in your office to AWS storage, so local apps can save files, disks or tape backups into the cloud.

## Real-life comparison

Storage Gateway is like a post room in your office. Staff drop items at the post room as normal, and it quietly ships them to a big warehouse (AWS). Recently used items stay in the post room so you can grab them quickly.

## What problem does it solve?

Many companies have old apps and backup software that expect a local file share, disk or tape drive. Moving everything to the cloud at once is hard. Storage Gateway lets those apps keep working the same way while the data is stored in AWS.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Gateway** | A virtual machine (or hardware box) you run in your office that talks to AWS. |
| **S3 File Gateway** | Shows S3 as a normal file share (NFS or SMB). |
| **Volume Gateway** | Shows cloud-backed disks (iSCSI) to local servers. |
| **Tape Gateway** | Pretends to be a tape library for backup software; tapes are stored in S3/Glacier. |
| **Cache** | Local storage that keeps recently used data for speed. |

## How it works (step by step)

1. You download the gateway as a virtual machine and run it in your office (e.g. on VMware or Hyper-V).
2. You **activate** it in the AWS Console.
3. You choose a type (file, volume or tape) and create a share, volume or virtual tapes.
4. Local servers connect to the gateway as if it were normal storage.
5. The gateway keeps recent data in its cache and sends everything to AWS.

## When to use it

- Moving off physical tape backups.
- Giving office servers more storage without buying disks.
- A step towards moving fully to AWS (hybrid cloud – part office, part cloud).

## When NOT to use it (and what to use instead)

- **A one-off copy of lots of data into AWS.** → Use [DataSync](../migration-transfer/datasync.md).
- **Your apps already run in AWS.** → Use [S3](s3.md), [EFS](efs.md) or [FSx](fsx.md) directly.

## Real-world example

**Scenario:** A school stores weekly backups on tapes, which a staff member drives to another site.

**The problem:** Tapes get lost, and restoring takes days.

**How Storage Gateway helps:** The school installs a Tape Gateway. Its backup software writes to "virtual tapes" as before, but they're stored in S3 Glacier. No more driving tapes around.

**What it looks like:**

```
 School office                         AWS
 Backup software ─► Tape Gateway ──internet──► S3 / Glacier
```

## Try it yourself

> ⚠️ **Cost warning:** You pay for the storage the gateway uses and for data transfer. Setting up a real gateway needs a local virtual machine or an EC2 server. Delete everything at the end.

Not ideal for a quick test. If you'd like to explore:

### Option A – Using the AWS Console (clicking in the website)

1. Open **Storage Gateway** in the Console and click **Create gateway**.
2. Read through the gateway types and host platforms (you can stop here without creating anything).

### Option B – Using the AWS CLI (typing commands)

```bash
# List any gateways in your account and Region
aws storagegateway list-gateways
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for a beginner test – the gateway needs a virtual machine running first.

### Clean up (delete what you made)

1. If you created a gateway, delete its shares/volumes/tapes, then delete the gateway.
2. Delete the virtual machine or EC2 server you used to run it.

## How much does it cost?

- **Storage** used in AWS (S3, EBS snapshots or Glacier).
- **Requests and data transfer out** of AWS.
- Some gateway types have small extra charges.

Official pricing: <https://aws.amazon.com/storagegateway/pricing/>

## Security tips

- Data is encrypted in transit and at rest; use KMS keys for more control.
- Restrict who can reach the file share on your local network.

## Common mistakes

- Making the cache too small, so everything is slow.
- Forgetting about internet bandwidth – big backups need a good connection.

## Works well with

- [S3](s3.md) and [S3 Glacier](s3-glacier.md) – where the data ends up.
- [AWS Backup](backup.md) – can manage Volume Gateway backups.

## Quick check (test yourself)

1. Which gateway type replaces tape backups?
   <details><summary>Answer</summary>Tape Gateway.</details>
2. Where does the gateway run?
   <details><summary>Answer</summary>Usually as a virtual machine in your own office or data centre.</details>
3. What does the cache do?
   <details><summary>Answer</summary>Keeps recently used data locally so it's fast to access.</details>

## Learn more

- [AWS Storage Gateway documentation](https://docs.aws.amazon.com/storagegateway/)
- [AWS Storage Gateway pricing](https://aws.amazon.com/storagegateway/pricing/)
