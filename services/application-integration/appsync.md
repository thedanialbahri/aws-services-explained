# AWS AppSync

**Category:** Application integration  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

AppSync creates managed GraphQL APIs (and real-time event APIs), letting apps fetch exactly the data they need from several sources in one request.

## Real-life comparison

A normal API is like a set menu – you get the whole meal. GraphQL is like ordering à la carte – you ask for exactly the dishes you want, in one order.

## What problem does it solve?

Mobile and web apps often need data from several places at once. AppSync combines them behind one GraphQL endpoint and can push live updates.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **GraphQL** | A query language where the app asks for exactly the fields it wants. |
| **Schema** | The description of available data. |
| **Resolver** | Code that fetches data for a field. |
| **Subscription** | A real-time update pushed to the app. |

## How it works (step by step)

1. Define a schema.
2. Connect data sources (DynamoDB, Lambda, HTTP, databases).
3. Write resolvers.
4. Apps send queries and get just the requested data.

## When to use it

- Mobile/web apps needing flexible queries or live updates.

## When NOT to use it (and what to use instead)

- **Simple REST APIs.** → [API Gateway](../networking/api-gateway.md).

## Real-world example

**Scenario:** A sports app shows live scores and player stats.

**How it helps:** One GraphQL query fetches scores and stats; subscriptions push score changes instantly.

**What it looks like:**

```
 App ──GraphQL──► AppSync ──► DynamoDB (scores) + Lambda (stats)
     ◄─subscription (live updates)─┘
```

## Try it yourself

> ⚠️ **Cost warning:** Free allowance for new accounts, then per million queries and real-time messages.

### Option A – Using the AWS Console (clicking in the website)

1. Open **AppSync** → **Create API** → **GraphQL APIs** → start from a sample.
2. Use the **Queries** tab to run a query.

### Option B – Using the AWS CLI (typing commands)

```bash
aws appsync list-graphql-apis
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for learning.

### Clean up (delete what you made)

Delete the API and any sample DynamoDB tables it created.

## How much does it cost?

Per million query/data operations, plus real-time messages and connection minutes.

Official pricing: <https://aws.amazon.com/appsync/pricing/>

## Security tips

- Use Cognito or IAM authorisation instead of API keys for real apps.

## Common mistakes

- Leaving API keys as the only protection.

## Works well with

- [DynamoDB](../databases/dynamodb.md), [Lambda](../compute/lambda.md), [Amplify](../front-end-web-mobile/amplify.md).

## Quick check (test yourself)

1. What is GraphQL?
   <details><summary>Answer</summary>A query language where apps ask for exactly the data they need.</details>
2. What is a subscription?
   <details><summary>Answer</summary>A real-time update pushed to the app.</details>
3. For a simple REST API, what's better?
   <details><summary>Answer</summary>API Gateway.</details>

## Learn more

- [AWS AppSync Developer Guide](https://docs.aws.amazon.com/appsync/latest/devguide/what-is-appsync.html)
