# Project 2: Host a static website

**Services:** [S3](../services/storage/s3.md) + [CloudFront](../services/networking/cloudfront.md) + [Route 53](../services/networking/route-53.md) (optional) + [ACM](../services/security-identity-compliance/certificate-manager.md) (optional)  **Level:** 🟢 Beginner

## What you'll build

A fast, secure website made of HTML/CSS/images, stored in a **private** S3 bucket and served worldwide over HTTPS by CloudFront.

```
 Visitor ──► (Route 53: www.example.com) ──► CloudFront (HTTPS, cache) ──OAC──► private S3 bucket
```

## Why this design

- The bucket stays **private** – only CloudFront can read it (via Origin Access Control).
- CloudFront gives HTTPS, speed and protection.
- No servers to patch, and tiny costs for small sites.

## Steps

> ⚠️ **Cost warning:** S3 and CloudFront have free allowances; a small site costs little or nothing. A domain name costs a yearly fee (optional part).

### Step 1 – Make the website files

Create `index.html` on your computer:
```html
<!DOCTYPE html>
<html lang="en-GB">
  <head><meta charset="utf-8"><title>My first AWS site</title></head>
  <body><h1>Hello from S3 and CloudFront!</h1></body>
</html>
```

### Step 2 – Create a private bucket and upload

1. **S3** → **Create bucket** → name `my-example-site-12345` → Region **eu-west-2**.
2. Keep **Block all public access** ticked → **Create bucket**.
3. Upload `index.html`.

### Step 3 – Create the CloudFront distribution

1. **CloudFront** → **Create distribution**.
2. **Origin domain:** your bucket.
3. **Origin access:** **Origin access control settings** → **Create new OAC**.
4. **Viewer protocol policy:** **Redirect HTTP to HTTPS**.
5. **Default root object:** `index.html`.
6. **Create distribution**, then **Copy policy** from the banner.
7. In the bucket → **Permissions** → **Bucket policy** → paste → **Save**.

### Step 4 – Test

Open `https://<your-distribution>.cloudfront.net` – you should see your page. Try opening the S3 object URL directly – you should get **Access Denied**. That's correct!

### Step 5 (optional) – Add your own domain

1. Request a certificate in **ACM** in **us-east-1** for `www.yourdomain.com` and validate with DNS.
2. Edit the distribution: add the **alternate domain name** and choose the certificate.
3. In **Route 53**, create an **A record (alias)** for `www` pointing to the distribution.

### Terraform version

Written for the AWS provider `~> 6.0`.

```hcl
provider "aws" {
  region = "eu-west-2"
}

# Private bucket for the site files
resource "aws_s3_bucket" "site" {
  bucket = "my-example-site-12345"
}

resource "aws_s3_bucket_public_access_block" "site" {
  bucket                  = aws_s3_bucket.site.id
  block_public_acls       = true
  block_public_policy     = true
  ignore_public_acls      = true
  restrict_public_buckets = true
}

# Upload index.html from this folder
resource "aws_s3_object" "index" {
  bucket       = aws_s3_bucket.site.id
  key          = "index.html"
  source       = "index.html"
  content_type = "text/html"
  etag         = filemd5("index.html")
}

# Lets CloudFront sign its requests to the private bucket
resource "aws_cloudfront_origin_access_control" "site" {
  name                              = "site-oac"
  origin_access_control_origin_type = "s3"
  signing_behavior                  = "always"
  signing_protocol                  = "sigv4"
}

resource "aws_cloudfront_distribution" "site" {
  enabled             = true
  default_root_object = "index.html"

  origin {
    domain_name              = aws_s3_bucket.site.bucket_regional_domain_name
    origin_id                = "s3-site"
    origin_access_control_id = aws_cloudfront_origin_access_control.site.id
  }

  default_cache_behavior {
    target_origin_id       = "s3-site"
    viewer_protocol_policy = "redirect-to-https"
    allowed_methods        = ["GET", "HEAD"]
    cached_methods         = ["GET", "HEAD"]
    # AWS managed "CachingOptimized" cache policy
    cache_policy_id = "658327ea-f89d-4fab-a63d-7e88639e58f6"
  }

  restrictions {
    geo_restriction {
      restriction_type = "none"
    }
  }

  viewer_certificate {
    cloudfront_default_certificate = true
  }
}

# Allow only this distribution to read the bucket
resource "aws_s3_bucket_policy" "site" {
  bucket = aws_s3_bucket.site.id
  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Effect    = "Allow"
      Principal = { Service = "cloudfront.amazonaws.com" }
      Action    = "s3:GetObject"
      Resource  = "${aws_s3_bucket.site.arn}/*"
      Condition = {
        StringEquals = { "AWS:SourceArn" = aws_cloudfront_distribution.site.arn }
      }
    }]
  })
}

output "site_url" {
  value = "https://${aws_cloudfront_distribution.site.domain_name}"
}
```

## Clean up

1. CloudFront: **Disable** the distribution, wait, then **Delete** it.
2. S3: empty and delete the bucket.
3. Delete any Route 53 records and ACM certificate you created (hosted zones cost money monthly).
4. Terraform: `terraform destroy`.

## What you learned

- Keep buckets private and use OAC for CloudFront.
- CloudFront certificates must be in `us-east-1`.
- Static sites need no servers at all.
