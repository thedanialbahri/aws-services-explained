# Amazon Connect

**Category:** Business applications  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Amazon Connect is a cloud contact centre: phone numbers, call routing, chat and agent tools, set up in a web browser.

## Real-life comparison

It's like renting a fully equipped call centre floor – phones, queues, hold music and supervisor screens – that you can make bigger or smaller any day.

## What problem does it solve?

Traditional phone systems need hardware, long contracts and specialists. Connect is pay-as-you-go and configured with drag-and-drop flows.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Instance** | Your contact centre. |
| **Contact flow** | The path a call takes (menus, queues, messages). |
| **Queue** | Where customers wait for an agent. |
| **Agent** | A person answering contacts. |

## How it works (step by step)

1. Create an instance and claim a phone number.
2. Build a contact flow.
3. Add agents and queues.
4. Agents answer in a browser-based softphone.

## When to use it

- Customer service phone lines and chat.

## When NOT to use it (and what to use instead)

- **Internal team meetings.** Use a meetings tool like Teams or Zoom.

## Real-world example

**Scenario:** A small energy supplier needs a helpline in a week.

**How it helps:** Connect gives it a UK number, a menu ("press 1 for billing"), and agents working from home.

**What it looks like:**

```
 Customer calls ──► Connect flow (menu) ──► queue ──► agent softphone
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per minute of usage plus phone number and telephony charges. Release numbers and delete the instance after testing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Connect** → **Create instance** and follow the wizard.
2. Log in to the instance and explore the sample contact flows.

### Option B – Using the AWS CLI (typing commands)

```bash
aws connect list-instances
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Release phone numbers, then delete the instance.

## How much does it cost?

Per minute of voice/chat usage, plus telephony and phone number charges.

Official pricing: <https://aws.amazon.com/connect/pricing/>

## Security tips

- Use strong agent passwords or SSO; record calls only where lawful and disclosed.

## Common mistakes

- Forgetting to release claimed phone numbers.

## Works well with

- [Lex](../machine-learning-ai/lex.md), [Lambda](../compute/lambda.md).

## Quick check (test yourself)

1. What is a contact flow?
   <details><summary>Answer</summary>The path a call or chat follows.</details>
2. Do agents need special phones?
   <details><summary>Answer</summary>No, they use a browser softphone.</details>
3. How is it charged?
   <details><summary>Answer</summary>Per minute of use, plus telephony.</details>

## Learn more

- [Amazon Connect Administrator Guide](https://docs.aws.amazon.com/connect/latest/adminguide/what-is-amazon-connect.html)
