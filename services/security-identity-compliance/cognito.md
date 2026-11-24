# Amazon Cognito

**Category:** Security, identity & compliance  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Cognito adds sign-up, sign-in and password reset to your web or mobile app, including "Sign in with Google" and similar options.

## Real-life comparison

Cognito is like hiring a reception desk for your building. The desk checks IDs, hands out visitor badges and deals with lost passes, so you don't have to.

## What problem does it solve?

Building secure logins yourself is hard: storing passwords safely, email verification, MFA, password reset, social logins. Get it wrong and user accounts get hacked. Cognito does it for you.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **User pool** | Your app's directory of users and its sign-in rules. |
| **Identity pool** | Swaps a signed-in user for temporary AWS credentials. |
| **App client** | The settings for one app that uses the user pool. |
| **Managed login** | A ready-made sign-in page hosted by Cognito. |
| **Token** | A digital pass (JWT) your app receives after sign-in. |

## How it works (step by step)

1. You create a **user pool** with password and MFA rules.
2. You add an **app client** and turn on the managed login page.
3. Users sign up and sign in on that page (or through your own screens).
4. Cognito gives your app **tokens**.
5. Your API (e.g. [API Gateway](../networking/api-gateway.md)) checks the token before allowing access.

## When to use it

- Customer logins for web and mobile apps.
- Protecting APIs so only signed-in users can call them.

## When NOT to use it (and what to use instead)

- **Staff logins to AWS itself.** → [IAM Identity Center](iam-identity-center.md).

## Real-world example

**Scenario:** A dog-walking start-up has an app where owners book walks.

**The problem:** They need secure accounts with email verification and "Sign in with Apple".

**How it helps:** A Cognito user pool handles sign-up and logins; the booking API only accepts requests with a valid Cognito token.

**What it looks like:**

```
 App ──sign in──► Cognito user pool ──token──► App ──request + token──► API Gateway ──► Lambda
```

## Try it yourself

> ⚠️ **Cost warning:** Cognito has a free allowance of monthly active users; check the pricing page for your tier. A test pool with one user is free.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Cognito** → **Create user pool**.
2. Choose **Traditional web application**, name it `demo-app`.
3. Sign-in option: **Email**. Click **Create user directory**.
4. Open **View login page** to see the hosted sign-in page and create a test account.

### Option B – Using the AWS CLI (typing commands)

```bash
# List user pools
aws cognito-idp list-user-pools --max-results 10
```

### Option C – Using Terraform (infrastructure as code)

```hcl
# A user pool where people sign in with their email address
resource "aws_cognito_user_pool" "app" {
  name                     = "demo-app"
  username_attributes      = ["email"]
  auto_verified_attributes = ["email"]
}
```

### Clean up (delete what you made)

1. Open the user pool → turn off **deletion protection** if on → **Delete**.

## How much does it cost?

Charged per monthly active user above a free amount; extra features (advanced security, SMS messages) cost more.

Official pricing: <https://aws.amazon.com/cognito/pricing/>

## Security tips

- Require MFA, or at least offer it.
- Use strong password rules.
- Never store tokens in places other sites can read.

## Common mistakes

- Using Cognito for staff AWS access instead of Identity Center.

## Works well with

- [API Gateway](../networking/api-gateway.md), [Amplify](../front-end-web-mobile/amplify.md), [Lambda](../compute/lambda.md).

## Quick check (test yourself)

1. What is a user pool?
   <details><summary>Answer</summary>Your app's user directory and sign-in settings.</details>
2. What does your app receive after sign-in?
   <details><summary>Answer</summary>Tokens (JWTs).</details>
3. Should staff use Cognito to sign in to AWS?
   <details><summary>Answer</summary>No – use IAM Identity Center.</details>

## Learn more

- [Amazon Cognito Developer Guide](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)
- [Amazon Cognito pricing](https://aws.amazon.com/cognito/pricing/)
