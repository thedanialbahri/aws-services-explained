# Amazon S3 Glacier storage classes (Glacier)

**Category:** Storage  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ℹ️ This page covers the **S3 Glacier storage classes** you choose inside S3. The older standalone Glacier "vault" service is closed to new customers. <!-- TODO: verify date and current name -->

## In one sentence

The Glacier storage classes keep files you rarely need in S3 for a much lower price, in exchange for slower or costlier retrieval.

## Real-life comparison

Glacier is like putting old boxes in the loft. It's cheap space, but getting a box down takes effort and time. You wouldn't keep your everyday coat there – but old tax papers are perfect.

## What problem does it solve?

Companies must often keep records for years (for legal reasons), but almost never look at them. Paying full price to store them is wasteful, and old tape backups in a cupboard are slow and fragile. Glacier keeps those files safe in AWS for a fraction of normal S3 prices.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Storage class** | The price-and-speed level of an S3 object. |
| **Glacier Instant Retrieval** | Cheap storage for data used about once a quarter, still readable in milliseconds. |
| **Glacier Flexible Retrieval** | Cheaper again. Getting files back takes minutes to hours. |
| **Glacier Deep Archive** | The cheapest. Getting files back takes up to about 12–48 hours. |
| **Restore** | Asking AWS to bring an archived file back so you can read it. |
| **Minimum storage duration** | You pay for at least this many days, even if you delete earlier (e.g. 90 or 180 days). |

## How it works (step by step)

1. You upload a file to S3 and choose a Glacier storage class – or a **lifecycle rule** moves it there later.
2. S3 keeps the file safely at a lower price.
3. For Instant Retrieval, you read it like any other file.
4. For Flexible Retrieval or Deep Archive, you first **restore** it, choosing how fast (faster costs more).
5. When the restore finishes, you download a temporary copy.

## When to use it

- Backups and archives you must keep but rarely open.
- Old logs, medical images or legal records.
- Replacing tape backups.

## When NOT to use it (and what to use instead)

- **Files you read often.** Retrieval fees add up. → Use S3 Standard or S3 Intelligent-Tiering ([S3](s3.md)).
- **Files you'll delete within a few weeks.** Minimum storage duration charges apply. → Use S3 Standard.

## Real-world example

**Scenario:** Ama runs a small accountancy firm and must keep client records for 6 years.

**The problem:** The records fill a server and are almost never opened.

**How Glacier helps:** Ama stores the records in S3 with a lifecycle rule: after 30 days move to Glacier Flexible Retrieval, after 1 year move to Deep Archive, after 6 years delete.

**What it looks like:**

```
 S3 Standard ──30 days──► Glacier Flexible ──1 year──► Deep Archive ──6 years──► deleted
```

## Try it yourself

> ⚠️ **Cost warning:** Archive classes have minimum storage durations and retrieval fees. Use a tiny test file and delete it at the end.

**Before you start:** An S3 bucket (see [S3](s3.md)).

### Option A – Using the AWS Console (clicking in the website)

1. Open your bucket in **S3**.
2. Click **Upload** → **Add files** and choose a small file.
3. Expand **Properties** and under **Storage class** choose **Glacier Deep Archive**.
4. Click **Upload**.
5. Click the file. Notice the **Restore** button – you can't download it straight away.
6. Go to the bucket's **Management** tab → **Create lifecycle rule** to see how files can move automatically.

### Option B – Using the AWS CLI (typing commands)

```bash
# Upload a file straight into Deep Archive
aws s3 cp old-report.txt s3://my-example-bucket-12345/archive/old-report.txt \
  --storage-class DEEP_ARCHIVE

# Ask S3 to restore it for 1 day using the cheapest (Bulk) speed
aws s3api restore-object --bucket my-example-bucket-12345 \
  --key archive/old-report.txt \
  --restore-request '{"Days":1,"GlacierJobParameters":{"Tier":"Bulk"}}'
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# Lifecycle rule: move files to Glacier after 30 days, delete after ~6 years
resource "aws_s3_bucket_lifecycle_configuration" "archive" {
  bucket = "my-example-bucket-12345"

  rule {
    id     = "archive-old-files"
    status = "Enabled"
    filter {}

    transition {
      days          = 30
      storage_class = "GLACIER"
    }

    expiration {
      days = 2190
    }
  }
}
```

### Clean up (delete what you made)

1. Delete the test file from the bucket (you'll be charged for the minimum duration anyway).
2. Delete any lifecycle rules you created, or delete the bucket as shown on the [S3 page](s3.md).

## How much does it cost?

- **Storage** – per GB per month, much lower than S3 Standard.
- **Retrieval** – per GB restored and per request; faster restores cost more.
- **Minimum storage duration** – early deletion is charged as if kept for the minimum.

Official pricing: <https://aws.amazon.com/s3/pricing/>

## Security tips

- The same S3 security applies: Block Public Access, least privilege, encryption.
- Use **S3 Object Lock** for records that must not be changed or deleted (e.g. compliance).

## Common mistakes

- Archiving files that someone needs every week.
- Forgetting that Deep Archive restores can take hours – not good in an emergency.
- Archiving millions of tiny files – per-object overheads can cost more than you save.

## Works well with

- [S3](s3.md) – Glacier classes are part of S3.
- [AWS Backup](backup.md) – can move backups to cold storage.

## Quick check (test yourself)

1. Which class is cheapest to store in?
   <details><summary>Answer</summary>Glacier Deep Archive.</details>
2. Can you download a Deep Archive file straight away?
   <details><summary>Answer</summary>No. You must restore it first, which can take hours.</details>
3. What tool moves files to Glacier automatically?
   <details><summary>Answer</summary>An S3 lifecycle rule.</details>

## Learn more

- [S3 storage classes](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html)
- [Amazon S3 pricing](https://aws.amazon.com/s3/pricing/)
