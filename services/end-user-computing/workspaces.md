# Amazon WorkSpaces

**Category:** End-user computing  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

WorkSpaces gives each user a full Windows or Linux desktop that runs in AWS and can be reached from almost any device.

## Real-life comparison

It's like having your office PC in a secure locker that you can open from home, a café or a borrowed laptop – everything is exactly where you left it.

## What problem does it solve?

Buying, setting up and securing laptops for every worker (especially temporary or remote ones) is slow. With WorkSpaces, the desktop lives in AWS; data never needs to sit on the local device.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **WorkSpace** | One user's virtual desktop. |
| **Bundle** | The desktop's size and operating system. |
| **Directory** | Where users are managed (AWS Managed Microsoft AD or AD Connector; Simple AD closed to new customers in July 2026). |
| **Running mode** | AlwaysOn (monthly) or AutoStop (hourly). |
| **WorkSpaces Pools** | Shared, non-persistent desktops – AWS announced in 2026 that this option is being retired. |

## How it works (step by step)

1. Set up a directory for users.
2. Launch WorkSpaces for users, choosing a bundle.
3. Users get an email with a registration code.
4. They connect with the WorkSpaces client or a web browser.

## When to use it

- Remote and temporary staff, contractors, secure environments.

## When NOT to use it (and what to use instead)

- **Users need just one or two apps.** → [AppStream 2.0](appstream.md).

## Real-world example

**Scenario:** A call centre hires 50 seasonal staff for winter.

**How it helps:** Staff use their own laptops to connect to WorkSpaces; no customer data is stored on their devices. In spring, the WorkSpaces are removed.

**What it looks like:**

```
 Any laptop / tablet ──► WorkSpaces client ══secure stream══► Windows desktop in AWS
```

## Try it yourself

> ⚠️ **Cost warning:** A Free Tier offer may exist for new users (check the pricing page). Otherwise WorkSpaces cost per month or per hour, and directories may cost extra. **Delete the WorkSpace and directory at the end.**

### Option A – Using the AWS Console (clicking in the website)

1. Open **WorkSpaces** → **Create WorkSpaces** and follow the quick setup with a small Free Tier-eligible bundle.
2. Connect with the client using the emailed registration code.

### Option B – Using the AWS CLI (typing commands)

```bash
aws workspaces describe-workspaces
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_workspaces_workspace`, but needs a directory first.

### Clean up (delete what you made)

1. Remove (terminate) the WorkSpace.
2. Deregister and delete the directory.

## How much does it cost?

Monthly (AlwaysOn) or hourly plus small monthly fee (AutoStop), by bundle; plus licences where applicable.

Official pricing: <https://aws.amazon.com/workspaces/pricing/>

## Security tips

- Turn on MFA through your directory; block clipboard/drive redirection if data must not leave.

## Common mistakes

- Using AlwaysOn for part-time users (AutoStop is cheaper).

## Works well with

- [IAM Identity Center](../security-identity-compliance/iam-identity-center.md), [Directory Service](https://aws.amazon.com/directoryservice/).

## Quick check (test yourself)

1. Where does the desktop actually run?
   <details><summary>Answer</summary>In AWS.</details>
2. Which running mode suits part-time users?
   <details><summary>Answer</summary>AutoStop.</details>
3. What if users need only one app?
   <details><summary>Answer</summary>AppStream 2.0.</details>

## Learn more

- [Amazon WorkSpaces Administration Guide](https://docs.aws.amazon.com/workspaces/latest/adminguide/amazon-workspaces.html)
