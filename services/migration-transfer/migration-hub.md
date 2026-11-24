# AWS Migration Hub

**Category:** Migration & transfer  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ⛔ **No longer available to new customers.** AWS Migration Hub stopped accepting new customers on 7 November 2025 (so did AWS Application Discovery Service). AWS recommends **AWS Transform**, which includes Migration Hub's features. Existing customers can finish their migrations.

## In one sentence

Migration Hub gives you one place to discover your servers, plan a migration and track its progress across AWS migration tools.

## Real-life comparison

It's like the master checklist on a clipboard during a house move: every room, every box, and whether it's packed, in the van or unpacked.

## What problem does it solve?

Big migrations use several tools and hundreds of servers. Migration Hub shows the status of everything in one dashboard.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Home Region** | The Region where Migration Hub stores tracking data. |
| **Application** | A group of servers that make up one system. |
| **Discovery** | Collecting details about your existing servers. |

## How it works (step by step)

1. Choose a home Region.
2. Discover servers (existing customers used Application Discovery Service).
3. Group them into applications.
4. Track progress as tools like MGN and DMS report in.

## When to use it

- Existing customers finishing large migrations.

## When NOT to use it (and what to use instead)

- **Any new migration.** → AWS Transform for planning and tracking; [MGN](application-migration-service.md) to move servers.

## Real-world example

**Scenario:** A university moves 200 servers in waves.

**How it helps:** The team tracks each application's status in one dashboard.

**What it looks like:**

```
 MGN + DMS ──status──► Migration Hub dashboard
```

## Try it yourself

> ⚠️ **Cost warning:** Migration Hub itself has no charge; the tools it tracks do.

### Option A – Using the AWS Console (clicking in the website)

1. Search for **Migration Hub** and read the overview.

### Option B – Using the AWS CLI (typing commands)

```bash
aws migrationhub-config get-home-region
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Nothing to clean up.

## How much does it cost?

No extra charge for Migration Hub.

## Security tips

- Discovery data reveals your network layout – limit access.

## Common mistakes

- Choosing a home Region you don't intend to keep.

## Works well with

- [Application Migration Service](application-migration-service.md), [DMS](database-migration-service.md).

## Quick check (test yourself)

1. What does Migration Hub track?
   <details><summary>Answer</summary>Migration progress across tools.</details>
2. What is a home Region?
   <details><summary>Answer</summary>Where Migration Hub stores its data.</details>
3. Is it needed for one server?
   <details><summary>Answer</summary>No.</details>

## Learn more

- [AWS Migration Hub User Guide](https://docs.aws.amazon.com/migrationhub/latest/ug/whatishub.html)
