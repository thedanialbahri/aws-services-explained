# AWS Secrets Manager

**Category:** Security, identity & compliance  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Secrets Manager stores passwords, API keys and other secrets safely, lets apps fetch them when needed, and can change them automatically.

## Real-life comparison

It's like a locked key cabinet with a guard. Staff ask the guard for a key when they need it, the guard checks their badge, and the locks are changed regularly.

## What problem does it solve?

Passwords often end up written in code or config files, where they leak (for example, pushed to GitHub). Secrets Manager keeps them encrypted, controls access with IAM, and can **rotate** (change) them on a schedule.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Secret** | A stored value, e.g. a database username and password. |
| **Rotation** | Changing the secret automatically on a schedule. |
| **Version** | Each change to a secret is kept as a version. |

## How it works (step by step)

1. You create a secret (encrypted with [KMS](kms.md)).
2. You give your app's IAM role permission to read it.
3. Your app asks Secrets Manager for the value when it starts.
4. Optionally, rotation updates the password in the database and the secret together.

## When to use it

- Database passwords, third-party API keys, tokens.

## When NOT to use it (and what to use instead)

- **Plain settings that aren't secret** (e.g. a feature flag). → Systems Manager Parameter Store ([Systems Manager](../management-governance/systems-manager.md)) – cheaper.

## Real-world example

**Scenario:** A developer's Lambda function connects to a database.

**The problem:** The password was in the code and was accidentally committed to a public repo.

**How it helps:** The password is changed and stored in Secrets Manager. The function reads it at runtime using its role. Rotation runs every 30 days.

**What it looks like:**

```
 Lambda (role) ──get secret──► Secrets Manager ──► password ──► Lambda ──► RDS
```

## Try it yourself

> ⚠️ **Cost warning:** Each secret has a monthly charge plus a charge per 10,000 API calls. New accounts may get a free trial period. Delete the test secret at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Secrets Manager** → **Store a new secret** → **Other type of secret**.
2. Add key `api_key`, value `test-123`. Click **Next**.
3. Name it `demo/api-key`, click **Next**, **Next**, **Store**.
4. Open it and click **Retrieve secret value**.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create a secret
aws secretsmanager create-secret --name demo/api-key --secret-string '{"api_key":"test-123"}'

# Read it back
aws secretsmanager get-secret-value --secret-id demo/api-key --query SecretString --output text
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# The secret "container" (keep the actual value out of Terraform code)
resource "aws_secretsmanager_secret" "api_key" {
  name                    = "demo/api-key"
  recovery_window_in_days = 0
}
```

### Clean up (delete what you made)

```bash
# Delete straight away (no recovery window)
aws secretsmanager delete-secret --secret-id demo/api-key --force-delete-without-recovery
```

## How much does it cost?

Per secret per month, plus per 10,000 API calls.

Official pricing: <https://aws.amazon.com/secrets-manager/pricing/>

## Security tips

- Give each app access only to its own secrets.
- Turn on rotation for database credentials.
- Cache secrets in your app to cut API calls.

## Common mistakes

- Printing secrets in logs.

## Works well with

- [RDS](../databases/rds.md), [Lambda](../compute/lambda.md), [KMS](kms.md).

## Quick check (test yourself)

1. What does rotation do?
   <details><summary>Answer</summary>Changes the secret automatically on a schedule.</details>
2. What controls who can read a secret?
   <details><summary>Answer</summary>IAM policies (and the secret's resource policy).</details>
3. What's a cheaper option for non-secret settings?
   <details><summary>Answer</summary>Systems Manager Parameter Store.</details>

## Learn more

- [Secrets Manager User Guide](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)
- [Secrets Manager pricing](https://aws.amazon.com/secrets-manager/pricing/)
