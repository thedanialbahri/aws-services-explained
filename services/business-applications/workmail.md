# Amazon WorkMail

**Category:** Business applications  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

> ⛔ **No longer available to new customers.** WorkMail stopped accepting new customers on 30 April 2026 and will end on **31 March 2027**. After that, mailboxes and the console can't be reached. Use Microsoft 365, Google Workspace or another email provider instead.

## In one sentence

WorkMail is a managed business email and calendar service that works with Outlook and mobile mail apps.

## Real-life comparison

It's like renting company mailboxes at a post office instead of running your own mail room.

## What problem does it solve?

It removed the need to run your own email server (like Exchange).

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Organisation** | Your WorkMail setup. |
| **Mailbox** | A user's email account. |

## How it works (step by step)

1. Create an organisation and add a domain.
2. Create users and mailboxes.
3. Users connect with Outlook, phones or the web client.

## When to use it

- Existing customers until 31 March 2027.

## When NOT to use it (and what to use instead)

- **New projects.** → Microsoft 365 or Google Workspace. For app emails → [SES](ses.md).

## Real-world example

**Scenario:** A small consultancy used WorkMail for staff email.

**Today:** It's planning a move to Microsoft 365 before 31 March 2027.

**What it looks like:**

```
 Outlook / phone ──► WorkMail mailboxes
```

## Try it yourself

> ⚠️ **Cost warning:** Not applicable for new customers.

### Option A – Using the AWS Console (clicking in the website)

Not applicable.

### Option B – Using the AWS CLI (typing commands)

Not applicable.

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Existing users: move or export mailboxes before 31 March 2027.

## How much does it cost?

Existing users pay per user per month.

## Security tips

- Existing users: plan migration early to avoid data loss.

## Common mistakes

- Waiting until the last month to migrate.

## Works well with

- [SES](ses.md).

## Quick check (test yourself)

1. Can new customers sign up?
   <details><summary>Answer</summary>No.</details>
2. What are common alternatives?
   <details><summary>Answer</summary>Microsoft 365 or Google Workspace.</details>
3. What should existing users do?
   <details><summary>Answer</summary>Plan and complete a migration before 31 March 2027.</details>

## Learn more

- [Amazon WorkMail end of support](https://docs.aws.amazon.com/workmail/latest/adminguide/workmail-end-of-support.html)
