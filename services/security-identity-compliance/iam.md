# AWS Identity and Access Management (IAM)

**Category:** Security, identity & compliance  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

IAM controls who (people and programs) can sign in to your AWS account and exactly what each of them is allowed to do.

## Real-life comparison

IAM is like the ID badge system in an office building. Each badge (identity) opens only certain doors (permissions). The cleaner's badge opens the cupboards, the finance team's opens the finance office, and only the building manager's opens everything. Visitors get a temporary badge that stops working at the end of the day (a role).

## What problem does it solve?

If everyone shared one login with full access, one mistake or one stolen password could destroy everything – and you'd never know who did what. IAM gives each person and program its own identity with only the access it needs, and every action is recorded.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Principal** | Anyone or anything making a request – a user, a role or a service. |
| **IAM user** | A long-term identity with its own password or access keys. Best avoided for people now – use [Identity Center](iam-identity-center.md). |
| **IAM group** | A collection of users that share permissions. |
| **IAM role** | An identity with permissions but no password. It's "worn" temporarily by a person or service. |
| **Policy** | A JSON document listing what's allowed or denied. |
| **Action** | Something you can do, e.g. `s3:GetObject` (read a file from S3). |
| **Resource** | The thing being acted on, identified by an **ARN** (Amazon Resource Name). |
| **Least privilege** | Giving only the permissions needed – nothing more. |
| **Access keys** | A key ID and secret used by programs. Treat them like passwords. |

## How it works (step by step)

1. Someone or something makes a request, e.g. "delete this S3 file".
2. AWS checks who they are (**authentication**).
3. AWS gathers every policy that applies to them and the resource.
4. AWS decides (**authorisation**):
   - If any policy says **Deny** → refused.
   - Otherwise, if a policy says **Allow** → allowed.
   - If nothing says Allow → refused (everything is denied by default).
5. The decision is recorded in [CloudTrail](../management-governance/cloudtrail.md).

### What a policy looks like

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject"],
      "Resource": "arn:aws:s3:::my-example-bucket/reports/*"
    }
  ]
}
```
This says: "Allow reading files, but only from the `reports/` folder of `my-example-bucket`."

## When to use it

- Always. Every AWS account uses IAM.
- Giving AWS services permission to use other services (roles for EC2, Lambda and so on).
- Setting guardrails, e.g. requiring MFA.

## When NOT to use it (and what to use instead)

- **Logins for people across many accounts.** → [IAM Identity Center](iam-identity-center.md) is easier and safer than individual IAM users.
- **Sign-in for your app's customers.** → [Cognito](cognito.md).

## Real-world example

**Scenario:** Ravi's small software company has three developers and a Lambda function that reads from S3.

**The problem:** Everyone used the root login, and the Lambda function had an access key pasted into its code.

**How IAM helps:**
- Root is locked away with MFA.
- Developers sign in through Identity Center with a developer permission set.
- The Lambda function uses an **IAM role** that can only read one bucket. The access key is deleted.

**What it looks like:**

```
 Developer ──signs in──► Identity Center ──► Developer permissions
 Lambda function ──assumes──► Role "read-reports-bucket" ──► s3:GetObject on one bucket only
 Root user ──► locked away, MFA on, never used day to day
```

## Try it yourself

> ⚠️ **Cost warning:** IAM is free.

### Option A – Using the AWS Console (clicking in the website)

1. Open **IAM** in the Console.
2. Look at the **Dashboard** – it shows security recommendations (e.g. MFA for root).
3. Click **Policies** → **Create policy** → **JSON** and paste the policy above (change the bucket name).
4. Click **Next**, name it `read-reports-only`, and click **Create policy**.
5. Click **Roles** → **Create role** → **AWS service** → **EC2** → **Next**.
6. Search for and tick `read-reports-only` → **Next**.
7. Name the role `ec2-read-reports` → **Create role**.
8. Open the role and look at its **Trust relationships** tab – it says EC2 is allowed to use this role.

### Option B – Using the AWS CLI (typing commands)

```bash
# Who am I signed in as?
aws sts get-caller-identity

# Create the policy from a file called policy.json
aws iam create-policy --policy-name read-reports-only --policy-document file://policy.json

# List the roles in the account
aws iam list-roles --query 'Roles[].RoleName'
```

### Option C – Using Terraform (infrastructure as code)

Written for the AWS provider `~> 6.0`.

```hcl
# A role that EC2 servers can use
resource "aws_iam_role" "ec2_read_reports" {
  name = "ec2-read-reports"
  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Effect    = "Allow"
      Principal = { Service = "ec2.amazonaws.com" }
      Action    = "sts:AssumeRole"
    }]
  })
}

# The permission: read files in reports/ of one bucket only
resource "aws_iam_role_policy" "read_reports" {
  name = "read-reports-only"
  role = aws_iam_role.ec2_read_reports.id
  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Effect   = "Allow"
      Action   = ["s3:GetObject"]
      Resource = "arn:aws:s3:::my-example-bucket/reports/*"
    }]
  })
}
```

### Clean up (delete what you made)

1. **IAM** → **Roles** → tick `ec2-read-reports` → **Delete**.
2. **Policies** → tick `read-reports-only` → **Actions** → **Delete**.
3. Terraform: `terraform destroy`.

## How much does it cost?

IAM is free. (Some related features, like IAM Access Analyzer's unused-access checks, have charges.)

Official pricing: IAM has no pricing page because it's free – see the [IAM FAQ](https://aws.amazon.com/iam/faqs/).

## Security tips

- **MFA** on the root user and every human.
- **Roles, not access keys**, for anything running in AWS.
- **Least privilege** – start small and add permissions when needed. Use **IAM Access Analyzer** to find unused or too-broad access.
- **Never** commit access keys to Git.

## Common mistakes

- Attaching `AdministratorAccess` to everything "to make it work".
- Using `"Resource": "*"` when one bucket or table would do.
- Long-lived access keys that are never rotated.
- Forgetting that an explicit **Deny** always wins over an Allow.

## Works well with

- [IAM Identity Center](iam-identity-center.md) – logins for people.
- [Organizations](organizations.md) – guardrails across accounts (SCPs).
- [CloudTrail](../management-governance/cloudtrail.md) – records every IAM decision.

## Quick check (test yourself)

1. If one policy allows an action and another denies it, what happens?
   <details><summary>Answer</summary>It's denied. An explicit Deny always wins.</details>
2. What should a Lambda function use to access S3 – an access key or a role?
   <details><summary>Answer</summary>A role.</details>
3. What does "least privilege" mean?
   <details><summary>Answer</summary>Giving only the permissions needed to do the job, and nothing more.</details>

## Learn more

- [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)
- [IAM security best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
