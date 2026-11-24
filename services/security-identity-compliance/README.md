# Security, identity & compliance

**Security** keeps the wrong people and programs out. **Identity** is about knowing who someone is and what they're allowed to do. **Compliance** is proving you follow the rules (laws and standards).

**Real-life comparison:** Think of a secure office building. IAM is the ID badge system, KMS is the safe, Secrets Manager is the key cabinet, WAF and Shield are the guards at the door, and GuardDuty is the CCTV team watching for anything odd.

## Services in this category

| Service | Level | What it does |
|---------|-------|--------------|
| [AWS IAM](iam.md) | 🟢 | Controls who can do what in your AWS account |
| [AWS IAM Identity Center](iam-identity-center.md) | 🟢 | One login for people across many AWS accounts |
| [AWS Artifact](artifact.md) | 🟢 | Download AWS's compliance reports and agreements |
| [AWS Organizations](organizations.md) | 🟡 | Manage many AWS accounts together |
| [Amazon Cognito](cognito.md) | 🟡 | Sign-up and sign-in for your app's users |
| [AWS KMS](kms.md) | 🟡 | Creates and controls encryption keys |
| [AWS Secrets Manager](secrets-manager.md) | 🟡 | Stores passwords and API keys safely |
| [AWS Certificate Manager](certificate-manager.md) | 🟡 | Free SSL/TLS certificates (the padlock in your browser) |
| [AWS WAF](waf.md) | 🟡 | A web firewall that blocks bad web requests |
| [AWS Shield](shield.md) | 🟡 | Protects against DDoS attacks |
| [Amazon GuardDuty](guardduty.md) | 🟡 | Watches your account for suspicious activity |
| [Amazon Inspector](inspector.md) | 🟡 | Scans servers, containers and Lambda for known weaknesses |
| [AWS Security Hub](security-hub.md) | 🟡 | One dashboard for security findings |
| [Amazon Macie](macie.md) | 🔴 | Finds sensitive data in S3 |
| [Amazon Detective](detective.md) | 🔴 | Helps investigate the cause of a security problem |
| [AWS Firewall Manager](firewall-manager.md) | 🔴 | Sets firewall rules across many accounts at once |

## The golden rules

1. Turn on **MFA** for every human login.
2. Don't use the **root user** day to day.
3. Give **least privilege** – only the permissions needed.
4. **Encrypt** data at rest and in transit.
5. **Log everything** with [CloudTrail](../management-governance/cloudtrail.md) and watch it with [GuardDuty](guardduty.md).

[← Back to the main index](../../README.md)
