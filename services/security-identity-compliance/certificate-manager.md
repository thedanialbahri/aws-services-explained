# AWS Certificate Manager (ACM)

**Category:** Security, identity & compliance  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

ACM gives you free SSL/TLS certificates for your websites and renews them automatically.

## Real-life comparison

A certificate is like a passport for your website. It proves the site really is `example.com`, which lets browsers show the padlock and encrypt the connection. ACM is the passport office – and it renews your passport for you before it expires.

## What problem does it solve?

Websites need HTTPS. Certificates used to cost money, and if someone forgot to renew one, the site showed scary warnings. ACM's public certificates are free when used with AWS services, and renew themselves.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **SSL/TLS certificate** | A digital file that proves a site's identity and enables encryption. |
| **HTTPS** | Encrypted web traffic (the padlock). |
| **DNS validation** | Proving you own a domain by adding a DNS record. |
| **Wildcard certificate** | Covers all sub-domains, e.g. `*.example.com`. |

## How it works (step by step)

1. You request a certificate for your domain.
2. ACM gives you a DNS record to add (one click if you use [Route 53](../networking/route-53.md)).
3. ACM checks the record and issues the certificate.
4. You attach it to a load balancer, CloudFront or API Gateway.
5. ACM renews it automatically while the DNS record stays in place.

## When to use it

- HTTPS on [CloudFront](../networking/cloudfront.md), [load balancers](../networking/elastic-load-balancing.md) and [API Gateway](../networking/api-gateway.md).

## When NOT to use it (and what to use instead)

- **A certificate installed directly on an EC2 server's web server software.** Standard ACM public certificates can't be downloaded for that; use a load balancer in front, or a free provider like Let's Encrypt on the server. <!-- TODO: verify ACM exportable public certificate feature -->

## Real-world example

**Scenario:** Sam's bakery site uses CloudFront.

**The problem:** Browsers say "Not secure".

**How it helps:** Sam requests a free certificate for `sams-bakery.co.uk` and `www.sams-bakery.co.uk` in `us-east-1` (required for CloudFront), validates it with Route 53 and attaches it.

**What it looks like:**

```
 Browser ══HTTPS (padlock)══► CloudFront [ACM certificate] ──► S3
```

## Try it yourself

> ⚠️ **Cost warning:** Public certificates used with AWS services are free. You need a domain you own to complete validation.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Certificate Manager** (switch to **us-east-1** if it's for CloudFront).
2. **Request** → **Request a public certificate** → enter your domain.
3. Choose **DNS validation** → **Request**.
4. Open the certificate → **Create records in Route 53** (if your domain is there).
5. Wait until the status is **Issued**.

### Option B – Using the AWS CLI (typing commands)

```bash
# Request a certificate using DNS validation
aws acm request-certificate --domain-name www.example.com --validation-method DNS --region us-east-1
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# Ask ACM for a certificate validated by DNS
resource "aws_acm_certificate" "site" {
  domain_name       = "www.example.com"
  validation_method = "DNS"
}
```

### Clean up (delete what you made)

1. Detach the certificate from any service.
2. **ACM** → tick it → **Delete**.

## How much does it cost?

Public certificates used with integrated AWS services are free. Private certificates (AWS Private CA) and exportable certificates have charges.

Official pricing: <https://aws.amazon.com/certificate-manager/pricing/>

## Security tips

- Redirect all HTTP to HTTPS.
- Keep the validation DNS record, or renewal will fail.

## Common mistakes

- Creating the certificate in the wrong Region – CloudFront needs `us-east-1`.

## Works well with

- [CloudFront](../networking/cloudfront.md), [Route 53](../networking/route-53.md), [Elastic Load Balancing](../networking/elastic-load-balancing.md).

## Quick check (test yourself)

1. Which Region must certificates for CloudFront be in?
   <details><summary>Answer</summary>us-east-1 (N. Virginia).</details>
2. How does ACM know you own the domain?
   <details><summary>Answer</summary>Through DNS (or email) validation.</details>
3. Do you need to renew ACM certificates yourself?
   <details><summary>Answer</summary>No, ACM renews them automatically.</details>

## Learn more

- [AWS Certificate Manager User Guide](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html)
- [ACM pricing](https://aws.amazon.com/certificate-manager/pricing/)
