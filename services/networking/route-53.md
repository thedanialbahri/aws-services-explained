# Amazon Route 53

**Category:** Networking & content delivery  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Route 53 lets you buy domain names and turns them (like `example.com`) into the IP addresses computers use to find your website.

## Real-life comparison

Route 53 is the internet's phone book (and sat-nav). People remember names like `sams-bakery.co.uk`, but computers need numbers like `203.0.113.10`. Route 53 looks up the name and gives back the number. It can even send people to the nearest or healthiest shop.

## What problem does it solve?

Without DNS (the Domain Name System), everyone would have to type IP addresses. Route 53 handles that lookup reliably at huge scale, and also checks your servers' health so it can stop sending users to one that's broken.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **DNS** | Domain Name System – the system that turns names into IP addresses. |
| **Domain** | A name you own, e.g. `example.com`. |
| **Hosted zone** | The container for all DNS records of one domain. |
| **Record** | One rule, e.g. "`www.example.com` → this IP". |
| **A record** | Points a name to an IPv4 address. |
| **CNAME record** | Points a name to another name. |
| **Alias record** | A Route 53 special record that points to AWS resources (like a load balancer or CloudFront), even at the top of the domain. |
| **TTL** | Time To Live – how long other computers remember the answer. |
| **Health check** | Route 53 regularly tests if your site is working. |

## How it works (step by step)

1. You register a domain (in Route 53 or elsewhere).
2. Route 53 creates a **hosted zone** for it.
3. You add **records**, e.g. `www` → your load balancer.
4. When someone types your domain, their computer asks DNS servers, which eventually ask Route 53.
5. Route 53 replies with the right address, and their browser connects.
6. Optional **routing policies** can send users to the nearest Region, split traffic, or fail over to a backup.

## When to use it

- Giving your website or app a proper domain name.
- Pointing domains at AWS resources with alias records.
- Automatic failover to a backup site.

## When NOT to use it (and what to use instead)

- **Your domain's DNS already works well with another provider** and you don't need AWS-specific features. You can keep it and just point records at AWS.
- **Private names inside your office network only.** You may already have DNS on your Active Directory servers; Route 53 private hosted zones are for names inside your VPCs.

## Real-world example

**Scenario:** Sam's online bakery has moved to AWS and bought `sams-bakery.co.uk`.

**The problem:** Customers need to reach the site by name, and Sam wants a backup page if the main site fails.

**How Route 53 helps:** Sam creates a hosted zone, an alias record pointing to CloudFront, and a health check with a failover record to a simple "we'll be back soon" page in S3.

**What it looks like:**

```
 Customer types sams-bakery.co.uk
           │
           ▼
      Route 53 ──(healthy?)── yes ──► CloudFront ──► website
                      └────── no  ──► S3 "back soon" page
```

## Try it yourself

> ⚠️ **Cost warning:** Each hosted zone has a monthly charge, and queries are charged per million. Registering a domain costs a yearly fee (and is not refundable). This exercise creates a hosted zone only – **delete it the same day**.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Route 53** → **Hosted zones** → **Create hosted zone**.
2. **Domain name:** `example-learning.com` (you don't need to own it to practise records).
3. **Type:** **Public hosted zone**. Click **Create hosted zone**.
4. Notice the **NS** and **SOA** records Route 53 created automatically.
5. Click **Create record**: name `www`, type **A**, value `192.0.2.10` (a documentation-only IP), then **Create records**.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create a hosted zone (caller reference must be unique each time)
aws route53 create-hosted-zone --name example-learning.com \
  --caller-reference "demo-$(date +%s)"

# List your hosted zones
aws route53 list-hosted-zones --query 'HostedZones[].[Name,Id]' --output table
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# A public hosted zone
resource "aws_route53_zone" "demo" {
  name = "example-learning.com"
}

# www.example-learning.com -> 192.0.2.10
resource "aws_route53_record" "www" {
  zone_id = aws_route53_zone.demo.zone_id
  name    = "www"
  type    = "A"
  ttl     = 300
  records = ["192.0.2.10"]
}
```

### Clean up (delete what you made)

1. Open the hosted zone and delete every record you created (not the NS and SOA records).
2. Go back to **Hosted zones**, tick it, and click **Delete**.
3. Terraform: `terraform destroy`.

## How much does it cost?

- **Hosted zones** – per zone per month.
- **Queries** – per million DNS queries (alias queries to many AWS resources are free).
- **Health checks** – per check per month.
- **Domains** – yearly fee depending on the ending (`.com`, `.co.uk` and so on).

Official pricing: <https://aws.amazon.com/route53/pricing/>

## Security tips

- Turn on **domain lock** and **auto-renew** so nobody can transfer or let your domain expire.
- Limit who can change DNS records with IAM – a bad record can send customers to the wrong place.
- Consider **DNSSEC** to stop forged DNS answers.

## Common mistakes

- **Waiting for changes** – old answers are cached until their TTL runs out.
- **Using a CNAME at the top of the domain** (`example.com`) – not allowed. Use an alias record.
- **Forgetting to update the name servers** at your registrar after creating the hosted zone.

## Works well with

- [CloudFront](cloudfront.md) and [Elastic Load Balancing](elastic-load-balancing.md) – common alias targets.
- [S3](../storage/s3.md) – static website hosting.
- [Certificate Manager](../security-identity-compliance/certificate-manager.md) – validates certificates with DNS records.

## Quick check (test yourself)

1. What does DNS do?
   <details><summary>Answer</summary>Turns names like example.com into IP addresses.</details>
2. Which record type lets you point `example.com` itself to a load balancer?
   <details><summary>Answer</summary>An alias record.</details>
3. Why might a DNS change take a while to show up?
   <details><summary>Answer</summary>Other computers cache the old answer until its TTL expires.</details>

## Learn more

- [Amazon Route 53 Developer Guide](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html)
- [Amazon Route 53 pricing](https://aws.amazon.com/route53/pricing/)
