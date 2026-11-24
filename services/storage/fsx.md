# Amazon FSx

**Category:** Storage  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

FSx runs popular shared file systems for you – Windows File Server, Lustre, NetApp ONTAP and OpenZFS – without you managing the servers.

## Real-life comparison

FSx is like renting a fully fitted office instead of an empty one. You pick the style you're used to (Windows, NetApp and so on), and the landlord handles the plumbing and repairs.

## What problem does it solve?

Many businesses rely on a specific type of file server, such as a Windows file share with Active Directory permissions. Running it yourself means patching servers, replacing disks and handling backups. FSx gives you the same file system, managed by AWS.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **FSx for Windows File Server** | A Windows file share (SMB) that works with Active Directory. |
| **FSx for Lustre** | A very fast file system for heavy computing, like science or machine learning. |
| **FSx for NetApp ONTAP** | NetApp storage features (snapshots, cloning) managed by AWS. |
| **FSx for OpenZFS** | A Linux-friendly file system based on ZFS. |
| **SMB** | Server Message Block – how Windows shares folders. |
| **Active Directory (AD)** | Microsoft's system for user accounts and permissions at work. |

## How it works (step by step)

1. You pick the FSx type you need.
2. You choose size, speed and the VPC subnets.
3. For Windows, you join it to your Active Directory.
4. AWS builds and runs the file system, including backups and patching.
5. Your servers connect to it like any other file share.

## When to use it

- Moving Windows file shares to AWS.
- High-performance computing (Lustre).
- Companies already using NetApp or ZFS features.

## When NOT to use it (and what to use instead)

- **Simple shared storage for Linux.** → Use [EFS](efs.md) (simpler, no sizing).
- **Object storage for websites or backups.** → Use [S3](s3.md).

## Real-world example

**Scenario:** An architecture firm stores drawings on a Windows file server in its office.

**The problem:** The server is old, and staff now work from home.

**How FSx helps:** The firm moves the share to FSx for Windows File Server, joined to its Active Directory. Staff keep the same folder permissions and connect over a VPN.

**What it looks like:**

```
 Staff laptops ──VPN──► VPC ──► FSx for Windows File Server ◄── Active Directory
```

## Try it yourself

> ⚠️ **Cost warning:** FSx file systems are charged per hour for storage and throughput. They are not a cheap test. Only create one if you're happy to pay for a short while, and delete it straight after.

### Option A – Using the AWS Console (clicking in the website)

1. Open **FSx** in the Console and click **Create file system**.
2. Read the four options and what each is for. You can cancel here without creating anything.

### Option B – Using the AWS CLI (typing commands)

```bash
# List FSx file systems in your account and Region
aws fsx describe-file-systems
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for a beginner test – most FSx types need Active Directory or larger setups first.

### Clean up (delete what you made)

1. If you created a file system, open it → **Actions** → **Delete file system**.
2. Delete any backups it made.

## How much does it cost?

- **Storage capacity** – per GB per month.
- **Throughput capacity** – per MB/s per month.
- **Backups** – per GB per month.

Official pricing: <https://aws.amazon.com/fsx/pricing/>

## Security tips

- Use security groups to allow only the servers that need access.
- Use Active Directory groups for permissions on Windows shares.
- Encryption at rest is on by default.

## Common mistakes

- Choosing a single-AZ deployment for important data – choose Multi-AZ for resilience.
- Over-sizing throughput and paying for speed you don't use.

## Works well with

- [EC2](../compute/ec2.md) – servers connect to FSx shares.
- [Site-to-Site VPN](../networking/site-to-site-vpn.md) and [Direct Connect](../networking/direct-connect.md) – reach FSx from your office.
- [AWS Backup](backup.md) – manages FSx backups.

## Quick check (test yourself)

1. Which FSx type suits Windows users?
   <details><summary>Answer</summary>FSx for Windows File Server.</details>
2. Which FSx type is built for very fast scientific computing?
   <details><summary>Answer</summary>FSx for Lustre.</details>
3. What should you use instead for simple Linux shared storage?
   <details><summary>Answer</summary>Amazon EFS.</details>

## Learn more

- [Amazon FSx documentation](https://docs.aws.amazon.com/fsx/)
- [Amazon FSx pricing](https://aws.amazon.com/fsx/pricing/)
