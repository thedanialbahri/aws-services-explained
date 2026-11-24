# AWS Application Migration Service (MGN)

**Category:** Migration & transfer  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Application Migration Service copies your physical, virtual or other-cloud servers into AWS as EC2 instances, with minimal downtime.

## Real-life comparison

It's like a removal company that builds an exact replica of your house in the new town, keeps it updated while you still live in the old one, then lets you move in on the day.

## What problem does it solve?

Rebuilding servers by hand in AWS is slow and risky. MGN replicates them continuously, so the final switch takes minutes.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Source server** | The server you're moving. |
| **Replication agent** | Software installed on the source to copy its disks. |
| **Test / cutover** | A trial launch / the final switch-over. |
| **Lift and shift (rehost)** | Moving without changing the app. |

## How it works (step by step)

1. Install the replication agent on the source server.
2. Data is copied continuously to a staging area in AWS.
3. Launch **test** instances to check everything works.
4. At **cutover**, launch the final instances and switch users over.

## When to use it

- Moving many servers quickly (lift and shift).

## When NOT to use it (and what to use instead)

- **Moving only a database.** → [Database Migration Service](database-migration-service.md).

## Real-world example

**Scenario:** A law firm moves 30 Windows servers from its office.

**How it helps:** MGN replicates them over a week; cutover happens on a Saturday morning.

**What it looks like:**

```
 Office servers (agent) ══replication══► AWS staging ──cutover──► EC2 instances
```

## Try it yourself

> ⚠️ **Cost warning:** Each server gets a free period of replication; you still pay for the EC2 and EBS resources used during staging and testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Application Migration Service** → **Get started** and read the setup steps.

### Option B – Using the AWS CLI (typing commands)

```bash
aws mgn describe-source-servers --filters '{}'
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Disconnect and delete source servers; terminate test instances.

## How much does it cost?

Free for a set period per server; then per server-hour. Plus EC2, EBS and data transfer.

Official pricing: <https://aws.amazon.com/application-migration-service/pricing/>

## Security tips

- Replication is encrypted; keep staging subnets private.

## Common mistakes

- Skipping the test launch.

## Works well with

- [EC2](../compute/ec2.md), [Migration Hub](migration-hub.md).

## Quick check (test yourself)

1. What is cutover?
   <details><summary>Answer</summary>The final switch to the servers in AWS.</details>
2. What gets installed on source servers?
   <details><summary>Answer</summary>A replication agent.</details>
3. What's "lift and shift"?
   <details><summary>Answer</summary>Moving an app without changing it.</details>

## Learn more

- [AWS Application Migration Service User Guide](https://docs.aws.amazon.com/mgn/latest/ug/what-is-application-migration-service.html)
