# AWS Transfer Family

**Category:** Migration & transfer  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Transfer Family runs a managed SFTP, FTPS, FTP or AS2 server that saves files straight into S3 or EFS.

## Real-life comparison

It's like a secure post box at the front of your building. Partners drop parcels in, and they go straight into your storeroom.

## What problem does it solve?

Many businesses exchange files with partners over SFTP. Running an SFTP server means patching and scaling. Transfer Family manages it.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **SFTP** | Secure File Transfer Protocol. |
| **Server endpoint** | The address partners connect to. |
| **User** | A login with a home folder in S3 or EFS. |

## How it works (step by step)

1. Create a server and choose protocols.
2. Create users with SSH keys and home folders.
3. Partners connect with normal SFTP clients.
4. Files land in S3/EFS.

## When to use it

- Exchanging files with partners or legacy systems.

## When NOT to use it (and what to use instead)

- **One-off bulk migrations.** → [DataSync](datasync.md).

## Real-world example

**Scenario:** A payroll provider sends monthly files by SFTP.

**How it helps:** Files arrive in S3 and trigger a Lambda to process them.

**What it looks like:**

```
 Partner SFTP client ──► Transfer Family server ──► S3 ──► Lambda
```

## Try it yourself

> ⚠️ **Cost warning:** Each server endpoint is charged **per hour while it exists**, plus per GB. Delete it straight after testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Transfer Family** → **Create server** → SFTP, service-managed users, public endpoint.
2. Add a user with an SSH public key and an S3 home folder.

### Option B – Using the AWS CLI (typing commands)

```bash
aws transfer list-servers
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_transfer_server` and `aws_transfer_user`.

### Clean up (delete what you made)

Delete users, then the server.

## How much does it cost?

Per protocol per hour per endpoint, plus per GB uploaded/downloaded.

Official pricing: <https://aws.amazon.com/aws-transfer-family/pricing/>

## Security tips

- Use SSH keys, not passwords; scope each user to their own folder.

## Common mistakes

- Leaving test servers running.

## Works well with

- [S3](../storage/s3.md), [Lambda](../compute/lambda.md).

## Quick check (test yourself)

1. Where do uploaded files go?
   <details><summary>Answer</summary>S3 or EFS.</details>
2. How is it charged?
   <details><summary>Answer</summary>Per endpoint-hour plus per GB.</details>
3. What authentication is best?
   <details><summary>Answer</summary>SSH keys.</details>

## Learn more

- [AWS Transfer Family User Guide](https://docs.aws.amazon.com/transfer/latest/userguide/what-is-aws-transfer-family.html)
