# AWS Key Management Service (KMS)

**Category:** Security, identity & compliance  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

KMS creates and guards the encryption keys that lock and unlock your data across AWS services.

## Real-life comparison

KMS is like a bank's safe-deposit vault for keys. Your keys never leave the vault. When you need something locked or unlocked, you ask the vault staff, who check your ID first and write down every visit.

## What problem does it solve?

**Encryption** scrambles data so only someone with the key can read it. The hard part is protecting the keys. KMS stores keys in secure hardware, controls who can use them, and logs every use in CloudTrail.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **KMS key** | A key that never leaves KMS; used to encrypt data or other keys. |
| **AWS managed key** | A key AWS creates for a service (e.g. `aws/s3`). Free, but less control. |
| **Customer managed key** | A key you create and control. |
| **Key policy** | Rules saying who can use or manage the key. |
| **Envelope encryption** | Data is locked with a data key, and the data key is locked with a KMS key. |
| **Key rotation** | Automatically making new key material on a schedule. |

## How it works (step by step)

1. You create a customer managed key (or use an AWS managed one).
2. You set a **key policy**.
3. You tell a service (S3, EBS, RDS) to encrypt with that key.
4. When data is read, the service asks KMS to unlock it – but only if the caller is allowed.
5. Every request is logged in [CloudTrail](../management-governance/cloudtrail.md).

## When to use it

- Encrypting S3, EBS, RDS, DynamoDB and more with keys you control.
- Meeting rules that require you to manage and audit keys.

## When NOT to use it (and what to use instead)

- **Storing passwords or API keys.** → [Secrets Manager](secrets-manager.md).
- **Needing a dedicated hardware device only you control.** → AWS CloudHSM.

## Real-world example

**Scenario:** A clinic stores patient letters in S3.

**The problem:** Regulators want proof of who can read the data and when it was read.

**How KMS helps:** The bucket uses a customer managed key that only the clinic's app role can use. CloudTrail shows every decryption.

**What it looks like:**

```
 App role ──read file──► S3 ──"please decrypt"──► KMS (checks key policy, logs it) ──► S3 ──► App
```

## Try it yourself

> ⚠️ **Cost warning:** Each customer managed key has a monthly charge (charged per day it exists) plus a small cost per request. Deleting a key takes 7–30 days, and charges stop once it's scheduled for deletion.

### Option A – Using the AWS Console (clicking in the website)

1. Open **KMS** → **Create key** → **Symmetric** → **Encrypt and decrypt** → **Next**.
2. Alias: `demo-key`. Choose yourself as key administrator and user.
3. Click **Finish**.
4. Open the key and look at the **Key policy** tab.

### Option B – Using the AWS CLI (typing commands)

```bash
# Encrypt a short message with the key
aws kms encrypt --key-id alias/demo-key --plaintext "$(echo -n 'hello' | base64)" \
  --query CiphertextBlob --output text > secret.b64

# Decrypt it again
aws kms decrypt --ciphertext-blob fileb://<(base64 -d secret.b64) \
  --query Plaintext --output text | base64 -d
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# A customer managed key with automatic yearly rotation
resource "aws_kms_key" "demo" {
  description             = "Demo key"
  enable_key_rotation     = true
  deletion_window_in_days = 7
}

resource "aws_kms_alias" "demo" {
  name          = "alias/demo-key"
  target_key_id = aws_kms_key.demo.key_id
}
```

### Clean up (delete what you made)

1. Open the key → **Key actions** → **Schedule key deletion** → 7 days → confirm.
2. Anything encrypted with it can't be read after deletion – make sure you don't need it.

## How much does it cost?

Per customer managed key per month, plus per 10,000 API requests. AWS managed keys have no monthly fee.

Official pricing: <https://aws.amazon.com/kms/pricing/>

## Security tips

- Turn on automatic rotation.
- Separate who can **manage** a key from who can **use** it.

## Common mistakes

- Deleting a key that still protects data – the data is lost for good.

## Works well with

- [S3](../storage/s3.md), [EBS](../storage/ebs.md), [RDS](../databases/rds.md), [CloudTrail](../management-governance/cloudtrail.md).

## Quick check (test yourself)

1. Do KMS keys ever leave KMS?
   <details><summary>Answer</summary>No – services send data or data keys to KMS to be encrypted or decrypted.</details>
2. Where is every key use recorded?
   <details><summary>Answer</summary>In CloudTrail.</details>
3. Where should you store a database password?
   <details><summary>Answer</summary>In Secrets Manager.</details>

## Learn more

- [AWS KMS Developer Guide](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)
- [AWS KMS pricing](https://aws.amazon.com/kms/pricing/)
