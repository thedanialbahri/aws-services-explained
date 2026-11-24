# Storage

**Storage** means keeping data (files, backups, disk drives) safe so you can get it back later.

**Real-life comparison:** Think of the different places you keep things at home. A wardrobe for clothes you use daily, a loft for things you rarely need, and a storage unit across town for overflow. AWS has a different type of storage for each job too.

## The three main types of storage

| Type | Plain English | Everyday comparison | AWS service |
|------|---------------|---------------------|-------------|
| **Object storage** | Whole files, each with a name and a label, reached over the internet | A storage unit full of labelled boxes | [S3](s3.md) |
| **Block storage** | A virtual hard drive plugged into one server | The hard drive inside your laptop | [EBS](ebs.md) |
| **File storage** | A shared drive many servers can use at once | A shared network drive (like `S:\` at work) | [EFS](efs.md), [FSx](fsx.md) |

## Services in this category

| Service | Level | What it does |
|---------|-------|--------------|
| [Amazon S3](s3.md) | 🟢 | Stores any number of files, reachable from anywhere |
| [Amazon EBS](ebs.md) | 🟢 | A virtual hard drive for an EC2 server |
| [Amazon S3 Glacier](s3-glacier.md) | 🟢 | Very cheap storage for files you rarely need |
| [Amazon EFS](efs.md) | 🟡 | A shared network drive many Linux servers can use at once |
| [AWS Storage Gateway](storage-gateway.md) | 🟡 | Connects your office storage to AWS storage |
| [AWS Backup](backup.md) | 🟡 | Backs up many AWS services from one place |
| [Amazon FSx](fsx.md) | 🔴 | Managed file systems for Windows, Lustre, NetApp and OpenZFS |
| [AWS Snow Family](snow-family.md) | 🔴 | Physical devices posted to you to move huge amounts of data |

## Which one should I use?

- **Website images, backups, documents, logs?** → [S3](s3.md)
- **The main disk for an EC2 server?** → [EBS](ebs.md)
- **Several Linux servers need the same files?** → [EFS](efs.md)
- **Windows servers need a shared drive?** → [FSx for Windows File Server](fsx.md)
- **Keeping old files for years, very cheaply?** → [S3 Glacier](s3-glacier.md)
- **Backing up lots of different services on a schedule?** → [AWS Backup](backup.md)

[← Back to the main index](../../README.md)
