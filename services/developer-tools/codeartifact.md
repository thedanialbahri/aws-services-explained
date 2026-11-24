# AWS CodeArtifact

**Category:** Developer tools  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

CodeArtifact stores the software packages your code depends on (npm, pip, Maven, NuGet and more), privately and securely.

## Real-life comparison

It's like a company stockroom of approved parts. Engineers take parts from the stockroom instead of buying from random shops.

## What problem does it solve?

Builds download packages from the internet, which can be slow, unavailable or tampered with. CodeArtifact keeps approved copies and your own private packages.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Domain** | A group of repositories. |
| **Repository** | Where packages are stored. |
| **Upstream** | A public source (like npmjs) CodeArtifact fetches from. |

## How it works (step by step)

1. Create a domain and repository with a public upstream.
2. Point `npm`/`pip` at it with `aws codeartifact login`.
3. Packages are fetched once and cached.

## When to use it

- Companies wanting control over dependencies.

## When NOT to use it (and what to use instead)

- **Small personal projects.** Public registries are fine.

## Real-world example

**Scenario:** A bank must review every open-source package.

**How it helps:** Builds only use CodeArtifact, which holds approved versions.

**What it looks like:**

```
 pip / npm ──► CodeArtifact ──(upstream)──► PyPI / npmjs
```

## Try it yourself

> ⚠️ **Cost warning:** Free allowance of storage and requests, then per GB and per request.

### Option A – Using the AWS Console (clicking in the website)

1. Open **CodeArtifact** → **Create domain**, then **Create repository** with a public upstream (e.g. pypi-store).

### Option B – Using the AWS CLI (typing commands)

```bash
# Point pip at your CodeArtifact repository
aws codeartifact login --tool pip --domain demo --repository demo-repo
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete the repository, then the domain. Run `pip config unset global.index-url` to point pip back to PyPI.

## How much does it cost?

Per GB-month stored and per request, above free amounts.

Official pricing: <https://aws.amazon.com/codeartifact/pricing/>

## Security tips

- Restrict publishing to CI roles only.

## Common mistakes

- Forgetting the login token expires (re-run login).

## Works well with

- [CodeBuild](codebuild.md).

## Quick check (test yourself)

1. What is an upstream?
   <details><summary>Answer</summary>A public source CodeArtifact fetches packages from.</details>
2. How does pip connect?
   <details><summary>Answer</summary>aws codeartifact login --tool pip.</details>
3. Why use it?
   <details><summary>Answer</summary>Control, speed and safety of dependencies.</details>

## Learn more

- [AWS CodeArtifact User Guide](https://docs.aws.amazon.com/codeartifact/latest/ug/welcome.html)
