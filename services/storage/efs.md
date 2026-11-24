# Amazon Elastic File System (EFS)

**Category:** Storage  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

EFS is a shared network drive that many Linux servers can read and write at the same time, and it grows and shrinks automatically.

## Real-life comparison

EFS is like a shared drive at the office (the `S:\` drive). Everyone on the team can open the same folders at once, and nobody has to buy a bigger disk when it fills up.

## What problem does it solve?

An EBS disk belongs to one server. If you run five web servers that all need the same uploaded files, copying files between them is messy. EFS gives all of them one shared folder, across several Availability Zones, with no disk size to manage.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **File system** | The shared drive itself. |
| **Mount** | Connect the drive to a server so it appears as a folder, e.g. `/mnt/efs`. |
| **Mount target** | The network connection point for EFS inside one AZ of your VPC. |
| **NFS** | Network File System – the standard way Linux shares folders over a network. |
| **Storage classes** | Standard, Infrequent Access and Archive – cheaper classes for files used less often. |

## How it works (step by step)

1. You create a file system in your VPC.
2. EFS creates a **mount target** in each AZ you choose.
3. On each Linux server, you install the EFS mount helper and **mount** the file system.
4. All servers now see the same files.
5. EFS grows as you add files and shrinks as you delete them. You pay for what's stored.

## When to use it

- Several Linux servers or containers sharing uploads or content.
- Shared home folders for users.
- Lambda functions or containers that need a shared file system.

## When NOT to use it (and what to use instead)

- **Windows servers.** EFS is NFS (Linux) only. → Use [FSx for Windows File Server](fsx.md).
- **One server needs a fast disk.** → Use [EBS](ebs.md) (cheaper and faster for one server).
- **Storing files for a website or backups.** → Use [S3](s3.md).

## Real-world example

**Scenario:** A news website runs on three EC2 servers behind a load balancer.

**The problem:** Editors upload photos to whichever server they hit, so the other two servers show broken images.

**How EFS helps:** All three servers mount the same EFS file system at `/var/www/uploads`. A photo uploaded on one is instantly available on all.

**What it looks like:**

```
            Load balancer
          ┌──────┼──────┐
        EC2-a  EC2-b  EC2-c
          └──────┼──────┘
                 ▼
          EFS (shared /uploads)
```

## Try it yourself

> ⚠️ **Cost warning:** EFS has limited Free Tier storage for new accounts. You pay per GB stored per month. Delete the file system at the end.

**Before you start:** A default VPC and a Linux EC2 server (see [EC2](../compute/ec2.md)).

### Option A – Using the AWS Console (clicking in the website)

1. Open **EFS** in the Console and click **Create file system**.
2. Give it a name, choose your VPC, and click **Create**.
3. Open the file system and click **Attach** to see the mount command.
4. Make sure the server's security group can reach the EFS security group on port **2049** (NFS).
5. On your Linux server, install the helper: `sudo dnf install -y amazon-efs-utils` (Amazon Linux 2023).
6. Make a folder and mount: `sudo mkdir /mnt/efs` then run the mount command from step 3.
7. Create a test file: `echo hi | sudo tee /mnt/efs/test.txt`.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create an encrypted file system
aws efs create-file-system --encrypted --tags Key=Name,Value=demo-efs

# Create a mount target in one subnet (replace the IDs)
aws efs create-mount-target --file-system-id fs-0123456789abcdef0 \
  --subnet-id subnet-0123456789abcdef0 --security-groups sg-0123456789abcdef0
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# An encrypted EFS file system
resource "aws_efs_file_system" "shared" {
  encrypted = true
  tags = { Name = "demo-efs" }
}

# A mount target in one subnet (replace the IDs)
resource "aws_efs_mount_target" "a" {
  file_system_id  = aws_efs_file_system.shared.id
  subnet_id       = "subnet-0123456789abcdef0"
  security_groups = ["sg-0123456789abcdef0"]
}
```

### Clean up (delete what you made)

1. On the server: `sudo umount /mnt/efs`.
2. In the EFS Console, tick the file system → **Delete**, type its ID, confirm.
3. Delete any security group you created just for this.

## How much does it cost?

- **Storage** – per GB per month; cheaper for Infrequent Access and Archive classes.
- **Data access** – reads and writes can be charged, depending on the throughput mode.

Official pricing: <https://aws.amazon.com/efs/pricing/>

## Security tips

- Turn on encryption at rest when creating the file system.
- Only allow port 2049 from the servers that need it (security groups).
- Use **EFS access points** to give each app its own folder and user.

## Common mistakes

- Forgetting to open port 2049 in the security group, so mounting hangs.
- Using EFS for a single-server database – EBS is better.
- Not setting lifecycle management, so old files stay in the most expensive class.

## Works well with

- [EC2](../compute/ec2.md) – servers mount EFS as a shared folder.
- [ECS](../containers/ecs.md) and [Lambda](../compute/lambda.md) – can mount EFS too.
- [AWS Backup](backup.md) – backs up EFS automatically.

## Quick check (test yourself)

1. Can a Windows server mount EFS?
   <details><summary>Answer</summary>No. EFS uses NFS for Linux. Use FSx for Windows File Server.</details>
2. What port must be open for EFS?
   <details><summary>Answer</summary>2049 (NFS).</details>
3. Do you need to pick a size for an EFS file system?
   <details><summary>Answer</summary>No. It grows and shrinks automatically.</details>

## Learn more

- [Amazon EFS User Guide](https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html)
- [Amazon EFS pricing](https://aws.amazon.com/efs/pricing/)
