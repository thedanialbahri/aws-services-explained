# AWS Amplify

**Category:** Front-end web & mobile  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Amplify hosts websites and web apps straight from a Git repository and helps you add back-end features like sign-in and data.

## Real-life comparison

Amplify is like a printing service connected to your laptop: every time you save a new version of your design, they automatically print and put it on display.

## What problem does it solve?

Getting a website online normally means setting up storage, a CDN, HTTPS and a deployment process. Amplify Hosting does all of this whenever you push code.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Amplify Hosting** | Builds and hosts your site from Git, with HTTPS and a CDN. |
| **Branch deployment** | Each Git branch can have its own preview site. |
| **Amplify Gen 2** | Defines back-end features (auth, data, storage) in TypeScript. |

## How it works (step by step)

1. Connect a GitHub, GitLab, Bitbucket or CodeCommit repo (or upload a zip).
2. Amplify detects the framework (React, Vue, Next.js, plain HTML).
3. It builds the site and deploys it to a global CDN.
4. Every push builds and deploys again.

## When to use it

- Static sites and modern web apps; quick prototypes.

## When NOT to use it (and what to use instead)

- **You want full control of each piece.** → [S3](../storage/s3.md) + [CloudFront](../networking/cloudfront.md) (see the [static website project](../../examples/static-website.md)).

## Real-world example

**Scenario:** A student builds a portfolio site in React.

**How it helps:** She connects the GitHub repo to Amplify; every push updates the live site at a custom domain with HTTPS.

**What it looks like:**

```
 git push ──► Amplify (build) ──► global CDN ──► https://portfolio.example.com
```

## Try it yourself

> ⚠️ **Cost warning:** Free Tier for build minutes, storage and data for new accounts; then per build minute and per GB served. Delete the app at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Create a folder with an `index.html` and zip it.
2. Open **AWS Amplify** → **Create new app** → **Deploy without Git**.
3. Upload the zip, then open the generated URL.

### Option B – Using the AWS CLI (typing commands)

```bash
aws amplify list-apps
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_amplify_app` and `aws_amplify_branch`.

### Clean up (delete what you made)

1. Open the app → **App settings** → **General** → **Delete app**.

## How much does it cost?

Per build minute, per GB stored and per GB served, above free amounts. Back-end services are charged separately.

Official pricing: <https://aws.amazon.com/amplify/pricing/>

## Security tips

- Use password protection for preview branches.

## Common mistakes

- Committing API keys into front-end code (everyone can see it).

## Works well with

- [Cognito](../security-identity-compliance/cognito.md), [AppSync](../application-integration/appsync.md), [Route 53](../networking/route-53.md).

## Quick check (test yourself)

1. What triggers a new deployment?
   <details><summary>Answer</summary>A push to the connected Git branch.</details>
2. Does Amplify include HTTPS?
   <details><summary>Answer</summary>Yes.</details>
3. Can you deploy without Git?
   <details><summary>Answer</summary>Yes, by uploading a zip.</details>

## Learn more

- [AWS Amplify Hosting User Guide](https://docs.aws.amazon.com/amplify/latest/userguide/welcome.html)
