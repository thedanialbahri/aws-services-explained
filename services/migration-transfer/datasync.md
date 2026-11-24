# AWS DataSync

**Category:** Migration & transfer  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

DataSync copies large amounts of files quickly and securely between your storage and AWS (S3, EFS, FSx), or between AWS services.

## Real-life comparison

It's like a professional moving company for files: it packs efficiently, checks nothing is damaged and only moves what's changed on later trips.

## What problem does it solve?

Copying millions of files with scripts is slow and unreliable. DataSync speeds it up, checks integrity and can run on a schedule.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Agent** | A virtual machine in your office that reads local storage. |
| **Location** | A source or destination. |
| **Task** | A copy job between two locations. |

## How it works (step by step)

1. Deploy an agent (for on-premises storage).
2. Create source and destination locations.
3. Create and run a task (once or on a schedule).

## When to use it

- Migrating file shares; regular copies to AWS for backup or analytics.

## When NOT to use it (and what to use instead)

- **Ongoing access to cloud storage from the office.** → [Storage Gateway](../storage/storage-gateway.md).
- **Partners sending files by SFTP.** → [Transfer Family](transfer-family.md).

## Real-world example

**Scenario:** A design studio has 40 TB of project files on a NAS.

**How it helps:** DataSync copies them to S3 over a weekend, then syncs changes nightly until cutover.

**What it looks like:**

```
 Office NAS ──► DataSync agent ══► DataSync ──► S3 / EFS / FSx
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per GB copied. Copy a small folder between two S3 buckets to test cheaply.

### Option A – Using the AWS Console (clicking in the website)

1. Open **DataSync** → **Create task**.
2. Source: an S3 location; destination: another S3 location.
3. Start the task and watch the progress.

### Option B – Using the AWS CLI (typing commands)

```bash
aws datasync list-tasks
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_datasync_location_s3` and `aws_datasync_task`.

### Clean up (delete what you made)

Delete the task, locations and test files.

## How much does it cost?

Per GB transferred, plus normal storage and requests.

Official pricing: <https://aws.amazon.com/datasync/pricing/>

## Security tips

- Data is encrypted in transit; use least-privilege roles for locations.

## Common mistakes

- Not limiting bandwidth during office hours.

## Works well with

- [S3](../storage/s3.md), [EFS](../storage/efs.md), [FSx](../storage/fsx.md).

## Quick check (test yourself)

1. What reads on-premises storage?
   <details><summary>Answer</summary>A DataSync agent.</details>
2. How is DataSync charged?
   <details><summary>Answer</summary>Per GB transferred.</details>
3. Can it run on a schedule?
   <details><summary>Answer</summary>Yes.</details>

## Learn more

- [AWS DataSync User Guide](https://docs.aws.amazon.com/datasync/latest/userguide/what-is-datasync.html)
