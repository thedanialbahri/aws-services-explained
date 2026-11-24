# Amazon Lightsail

**Category:** Compute  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Lightsail gives you a simple virtual server, with storage and data transfer bundled in, for a fixed monthly price.

## Real-life comparison

If EC2 is building a meal from individual ingredients, Lightsail is a meal deal: sandwich, drink and snack for one price. Less choice, but simpler and you know exactly what you'll pay.

## What problem does it solve?

EC2 has hundreds of options and its bill has many parts. For a small website or blog, that's overwhelming. Lightsail gives you a ready-to-go server (even with WordPress pre-installed) and a predictable bill.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Instance** | Your Lightsail server. |
| **Blueprint** | A ready-made setup, e.g. "WordPress" or "Ubuntu". |
| **Bundle / plan** | The size and monthly price (CPU, memory, disk, data transfer). |
| **Static IP** | A fixed public address that doesn't change when you restart. |
| **Snapshot** | A backup copy of your server. |

## How it works (step by step)

1. You choose a Region and a **blueprint** (e.g. WordPress).
2. You choose a **plan** (monthly price).
3. Lightsail creates the server in a few minutes.
4. You attach a **static IP** and point your domain at it.
5. You manage it from the simple Lightsail console, including a browser-based terminal.

## When to use it

- Personal websites, blogs (WordPress) and small business sites.
- Learning servers on a fixed budget.
- Simple test or development environments.

## When NOT to use it (and what to use instead)

- **You need auto scaling, many AWS integrations or fine control.** → Use [EC2](ec2.md).
- **Your site is just static HTML.** → Use [S3](../storage/s3.md) + [CloudFront](../networking/cloudfront.md) or [Amplify](../front-end-web-mobile/amplify.md) – cheaper and no server.

## Real-world example

**Scenario:** Grace is a wedding photographer who wants a WordPress portfolio site.

**The problem:** Shared hosting is slow, and EC2 looks complicated.

**How Lightsail helps:** Grace launches a WordPress blueprint on a small plan, attaches a static IP, points her domain at it, and has a site in an afternoon – for a fixed monthly cost.

**What it looks like:**

```
 Visitor ──► grace-photos.co.uk ──► Static IP ──► Lightsail instance (WordPress)
```

## Try it yourself

> ⚠️ **Cost warning:** Some Lightsail plans include a free trial period for new users (check the [Lightsail pricing page](https://aws.amazon.com/lightsail/pricing/)). After that, you pay the monthly price **while the instance exists, even if it's stopped**. Delete it at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Search for **Lightsail** in the Console and open it.
2. Click **Create instance**.
3. Choose **London** as the location, **Linux/Unix**, and the **WordPress** blueprint.
4. Choose the smallest plan.
5. Name it `my-wordpress` and click **Create instance**.
6. When it's **Running**, click it and copy the public IP into your browser – you'll see WordPress.
7. Use the **Connect using SSH** button to open a terminal in the browser.

### Option B – Using the AWS CLI (typing commands)

```bash
# See which blueprints and plans are available
aws lightsail get-blueprints --query 'blueprints[].blueprintId'
aws lightsail get-bundles --query 'bundles[].[bundleId,price]' --output table

# Create a WordPress instance (check the blueprint and bundle IDs from above)
aws lightsail create-instances --instance-names my-wordpress \
  --availability-zone eu-west-2a --blueprint-id wordpress --bundle-id nano_3_0
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# A small WordPress server in London (check current bundle IDs first)
resource "aws_lightsail_instance" "wp" {
  name              = "my-wordpress"
  availability_zone = "eu-west-2a"
  blueprint_id      = "wordpress"
  bundle_id         = "nano_3_0"
}
```

`nano_3_0` was the smallest plan with a public IPv4 address when this page was written. Run `aws lightsail get-bundles` to see today's plans.

### Clean up (delete what you made)

1. In Lightsail, open `my-wordpress` → **Delete** → confirm.
2. Under **Networking**, release any **static IP** you created (unattached static IPs can cost money).
3. Delete any snapshots.

## How much does it cost?

A **fixed monthly price** per plan, which includes CPU, memory, disk and a data transfer allowance. Extra data transfer, snapshots and some add-ons cost extra.

Official pricing: <https://aws.amazon.com/lightsail/pricing/>

## Security tips

- Limit SSH to your own IP address in the instance's **Networking** tab.
- Keep WordPress and its plugins updated.
- Take regular snapshots (you can automate them).

## Common mistakes

- Stopping instead of deleting – you're still billed.
- Leaving a static IP unattached.

## Works well with

- [Route 53](../networking/route-53.md) – point your domain at Lightsail.
- [EC2](ec2.md) – you can export Lightsail snapshots to EC2 if you outgrow it.

## Quick check (test yourself)

1. What's the main difference between Lightsail and EC2 billing?
   <details><summary>Answer</summary>Lightsail is a fixed monthly bundle; EC2 charges separately for compute, storage and data transfer.</details>
2. What is a blueprint?
   <details><summary>Answer</summary>A ready-made setup, such as WordPress on Linux.</details>
3. Does a stopped Lightsail instance cost money?
   <details><summary>Answer</summary>Yes, until you delete it.</details>

## Learn more

- [Amazon Lightsail documentation](https://docs.aws.amazon.com/lightsail/)
- [Amazon Lightsail pricing](https://aws.amazon.com/lightsail/pricing/)
