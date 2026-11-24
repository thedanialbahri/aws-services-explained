# Amazon CloudFront

**Category:** Networking & content delivery  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

CloudFront is a content delivery network (CDN) that keeps copies of your website's files in locations around the world, so they load fast for everyone.

## Real-life comparison

Imagine one bakery in London shipping cakes to customers in Tokyo – slow. CloudFront is like opening small shops in many cities that keep popular cakes in stock. Customers get them from the nearest shop. If a shop runs out, it fetches more from the main bakery.

## What problem does it solve?

If your website is stored in London, a visitor in Sydney waits longer for every image and page. CloudFront serves copies from **edge locations** near each visitor, which is faster, takes load off your servers, and adds protection against attacks.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **CDN** | Content Delivery Network – a network of servers that store copies of content near users. |
| **Distribution** | Your CloudFront setup for one website or app. |
| **Origin** | Where the original files live, e.g. an S3 bucket or a load balancer. |
| **Edge location** | A CloudFront site near users that keeps cached copies. |
| **Cache** | Saved copies of files, so they don't have to be fetched each time. |
| **TTL** | How long a copy is kept before checking for a newer version. |
| **Invalidation** | Telling CloudFront to throw away old copies now. |
| **OAC** (Origin Access Control) | Lets CloudFront read a private S3 bucket, so the bucket doesn't need to be public. |

## How it works (step by step)

1. You create a **distribution** and set its **origin** (e.g. your S3 bucket).
2. CloudFront gives you a web address like `d1234abcd.cloudfront.net`.
3. A visitor requests a file. CloudFront sends them to the nearest edge location.
4. If the edge has a copy (a "cache hit"), it sends it straight away.
5. If not (a "cache miss"), it fetches the file from the origin, sends it, and keeps a copy.
6. Later visitors nearby get the cached copy.

## When to use it

- Speeding up websites, images, videos and downloads worldwide.
- Serving a static website from a **private** S3 bucket with HTTPS.
- Adding protection with [AWS WAF](../security-identity-compliance/waf.md) and [Shield](../security-identity-compliance/shield.md).

## When NOT to use it (and what to use instead)

- **All your users are next to one Region and traffic is tiny.** CloudFront still helps with HTTPS and security, but the speed gain is small.
- **Non-web traffic like games over UDP.** → Use [Global Accelerator](global-accelerator.md).

## Real-world example

**Scenario:** Kofi sells digital art prints worldwide from an S3-hosted website.

**The problem:** Customers in Australia and the USA complain that the large images load slowly.

**How CloudFront helps:** Kofi puts CloudFront in front of his private S3 bucket using OAC, adds his own domain and an HTTPS certificate, and images now load from edge locations near each customer.

**What it looks like:**

```
 Customer in Sydney ──► Edge location (Sydney) ──cache miss──► S3 bucket (London)
 Next customer       ──► Edge location (Sydney) ──cache hit ──► served instantly
```

## Try it yourself

> ⚠️ **Cost warning:** CloudFront has a monthly free allowance of data transfer and requests. A tiny test site costs nothing or very little. Delete the distribution at the end.

**Before you start:** An S3 bucket with an `index.html` file (see [S3](../storage/s3.md)). Keep Block Public Access **on**.

### Option A – Using the AWS Console (clicking in the website)

1. Open **CloudFront** → **Create distribution**.
2. **Origin domain:** choose your S3 bucket from the list.
3. **Origin access:** choose **Origin access control settings (recommended)** → **Create new OAC** → **Create**.
4. **Viewer protocol policy:** **Redirect HTTP to HTTPS**.
5. **Default root object:** `index.html`.
6. Leave other settings as default and click **Create distribution**.
7. CloudFront shows a banner with a **bucket policy** – click **Copy policy**, then open your bucket's **Permissions** tab and paste it into **Bucket policy**.
8. Wait until the distribution's status is **Enabled** (a few minutes).
9. Open the **Distribution domain name** (`https://d....cloudfront.net`) in your browser.

### Option B – Using the AWS CLI (typing commands)

```bash
# List your distributions and their web addresses
aws cloudfront list-distributions \
  --query 'DistributionList.Items[].[Id,DomainName,Status]' --output table

# Clear the cache for every file after you update the site (replace the ID)
aws cloudfront create-invalidation --distribution-id E1234567890ABC --paths "/*"
```

### Option C – Using Terraform (infrastructure as code)

A full CloudFront + private S3 example is in the [static website project](../../examples/static-website.md).

### Clean up (delete what you made)

1. Tick the distribution → **Disable**. Wait until it shows **Disabled** (a few minutes).
2. Tick it again → **Delete**.
3. Delete the OAC under **Origin access** (optional – it's free).
4. Remove the bucket policy statement you added, or delete the bucket.

## How much does it cost?

- **Data transfer out** to viewers – per GB, varying by part of the world.
- **Requests** – per 10,000 HTTP/HTTPS requests.
- **Extras** – invalidations above a free amount, functions, real-time logs.
- AWS also offers flat-rate plans for some use cases – check the pricing page.

Official pricing: <https://aws.amazon.com/cloudfront/pricing/>

## Security tips

- Keep the S3 bucket private and use **OAC**.
- Always redirect HTTP to HTTPS.
- Attach [AWS WAF](../security-identity-compliance/waf.md) to block common attacks.

## Common mistakes

- **Forgetting the bucket policy**, so you get "Access Denied".
- **Updating the site and seeing old files** – wait for the TTL or create an invalidation.
- **Making the bucket public** as well as using CloudFront – unnecessary and risky.

## Works well with

- [S3](../storage/s3.md) – the most common origin.
- [Route 53](route-53.md) – point your domain at the distribution.
- [Certificate Manager](../security-identity-compliance/certificate-manager.md) – free HTTPS certificates (must be in `us-east-1` for CloudFront).
- [WAF](../security-identity-compliance/waf.md) – web firewall.

## Quick check (test yourself)

1. What is an origin?
   <details><summary>Answer</summary>Where the original files live, such as an S3 bucket or load balancer.</details>
2. How can CloudFront read a private S3 bucket?
   <details><summary>Answer</summary>Using Origin Access Control (OAC) and a bucket policy that allows it.</details>
3. You updated your site but visitors see the old version. What can you do?
   <details><summary>Answer</summary>Create an invalidation, or wait for the cache TTL to expire.</details>

## Learn more

- [Amazon CloudFront Developer Guide](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)
- [Amazon CloudFront pricing](https://aws.amazon.com/cloudfront/pricing/)
