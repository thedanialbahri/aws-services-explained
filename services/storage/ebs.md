# Amazon Elastic Block Store (EBS)

**Category:** Storage  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

EBS gives your EC2 server a virtual hard drive that keeps its data even when the server is turned off.

## Real-life comparison

EBS is like the hard drive inside a laptop. The laptop (your EC2 server) uses it to store its operating system and files. You can unplug the drive and plug it into another laptop, but only in the same building (the same Availability Zone).

## What problem does it solve?

An EC2 server needs somewhere to keep its operating system, programs and data. Without a lasting disk, everything would vanish when the server stopped. EBS gives each server a disk that survives restarts, can be resized, and can be backed up with **snapshots** (point-in-time copies).

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Volume** | One virtual disk. |
| **Root volume** | The disk the operating system starts from. |
| **Snapshot** | A backup copy of a volume at one moment, stored in S3 behind the scenes. |
| **Volume type** | The kind of disk, e.g. `gp3` (general SSD), `io2` (very fast SSD), `st1` (cheap hard disk for big files). |
| **IOPS** | Input/output operations per second – how many reads and writes the disk can handle. |
| **Availability Zone (AZ)** | One data centre area. A volume only works with servers in the same AZ. |

## How it works (step by step)

1. You create a volume, choosing its size, type and AZ.
2. You **attach** it to an EC2 server in the same AZ.
3. The server sees it as a normal disk (e.g. `/dev/xvdf` on Linux, `D:` on Windows).
4. AWS copies the volume's data within that AZ, so one broken physical disk doesn't lose it.
5. You take **snapshots** to back it up. You can create new volumes from a snapshot, even in another AZ or Region.

## When to use it

- The main disk for any EC2 server.
- Databases you run yourself on EC2.
- Any app that needs a fast disk attached to one server.

## When NOT to use it (and what to use instead)

- **Many servers need the same files at once.** → Use [EFS](efs.md) or [FSx](fsx.md).
- **Storing files for websites, backups or sharing over the internet.** → Use [S3](s3.md).
- **You don't want to manage a database server.** → Use [RDS](../databases/rds.md).

## Real-world example

**Scenario:** Priya runs a WordPress blog on one EC2 server.

**The problem:** The blog's images and database are growing, and the 8 GB disk is nearly full.

**How EBS helps:** Priya takes a snapshot first (just in case), then increases the volume to 30 GB in the Console without stopping the server. She expands the file system inside Linux, and the blog keeps running. She also sets up daily snapshots with [AWS Backup](backup.md).

**What it looks like:**

```
 ┌──────────── AZ eu-west-2a ────────────┐
 │  EC2 server ◄──attached── EBS volume  │
 └───────────────────────────────┬───────┘
                                 │ daily snapshot
                                 ▼
                        Snapshots (stored in S3)
```

## Try it yourself

> ⚠️ **Cost warning:** The Free Tier includes a limited amount of EBS storage and snapshots. You pay per GB per month for every volume and snapshot, **even when the server is stopped**. Delete them at the end.

**Before you start:** An EC2 server running in your account (see [EC2](../compute/ec2.md)).

### Option A – Using the AWS Console (clicking in the website)

1. Open **EC2** in the Console.
2. In the left menu, click **Volumes** (under Elastic Block Store).
3. Click **Create volume**.
4. Choose **gp3**, size **1** GiB, and the **same AZ** as your server.
5. Click **Create volume**.
6. Tick the new volume → **Actions** → **Attach volume**.
7. Choose your server and click **Attach volume**.
8. Tick the volume → **Actions** → **Create snapshot**, give it a description, and click **Create snapshot**.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create a 1 GiB gp3 volume in AZ eu-west-2a
aws ec2 create-volume --size 1 --volume-type gp3 --availability-zone eu-west-2a

# Attach it to a server (replace the IDs with your own)
aws ec2 attach-volume --volume-id vol-0123456789abcdef0 \
  --instance-id i-0123456789abcdef0 --device /dev/sdf

# Take a snapshot of the volume
aws ec2 create-snapshot --volume-id vol-0123456789abcdef0 --description "Test snapshot"
```

### Option C – Using Terraform (infrastructure as code)

Written for the AWS provider `~> 6.0`.

```hcl
# A 1 GiB general-purpose SSD volume, encrypted
resource "aws_ebs_volume" "data" {
  availability_zone = "eu-west-2a"
  size              = 1
  type              = "gp3"
  encrypted         = true
}

# Attach the volume to an existing server (replace the instance ID)
resource "aws_volume_attachment" "data" {
  device_name = "/dev/sdf"
  volume_id   = aws_ebs_volume.data.id
  instance_id = "i-0123456789abcdef0"
}
```

### Clean up (delete what you made)

1. **Volumes** → tick the volume → **Actions** → **Detach volume**. Wait until it shows **Available**.
2. **Actions** → **Delete volume**.
3. **Snapshots** → tick your snapshot → **Actions** → **Delete snapshot**.
4. CLI: `aws ec2 delete-volume --volume-id vol-...` and `aws ec2 delete-snapshot --snapshot-id snap-...`

## How much does it cost?

- **Per GB per month** for each volume, depending on the type.
- **Extra IOPS or throughput** on some types (e.g. gp3 above its included baseline, io2).
- **Snapshots** – per GB per month of changed data stored.

Official pricing: <https://aws.amazon.com/ebs/pricing/>

## Security tips

- Turn on **EBS encryption by default** for your account (EC2 → Settings → Data protection and security).
- Never share snapshots publicly – they can contain whole disks of data.
- Limit who can delete volumes and snapshots with [IAM](../security-identity-compliance/iam.md).

## Common mistakes

- **Leaving volumes behind** after deleting a server. Unattached volumes still cost money.
- **Trying to attach a volume in another AZ.** Copy it via a snapshot instead.
- **Resizing the volume but not the file system.** The OS won't see the new space until you expand it.

## Works well with

- [EC2](../compute/ec2.md) – EBS volumes are the disks of EC2 servers.
- [AWS Backup](backup.md) – schedules snapshots automatically.
- [KMS](../security-identity-compliance/kms.md) – encrypts volumes and snapshots.

## Quick check (test yourself)

1. Can you attach an EBS volume in `eu-west-2a` to a server in `eu-west-2b`?
   <details><summary>Answer</summary>No. A volume only attaches to servers in its own AZ. Take a snapshot and create a new volume in the other AZ.</details>
2. Do you still pay for an EBS volume when its server is stopped?
   <details><summary>Answer</summary>Yes. You pay for the storage until you delete the volume.</details>
3. What is a snapshot?
   <details><summary>Answer</summary>A point-in-time backup of a volume that you can use to create new volumes.</details>

## Learn more

- [Amazon EBS User Guide](https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html)
- [Amazon EBS pricing](https://aws.amazon.com/ebs/pricing/)
