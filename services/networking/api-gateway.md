# Amazon API Gateway

**Category:** Networking & content delivery  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

API Gateway creates a secure web address (an API) that apps can call, and passes each request on to your code, such as a Lambda function.

## Real-life comparison

API Gateway is like a restaurant's front counter. Customers (apps) place orders at the counter; staff check the order is valid and paid for, then pass it to the kitchen (your code). Customers never walk into the kitchen.

## What problem does it solve?

An **API** (Application Programming Interface – a way for programs to talk to each other) needs a web address, security, rate limits and logging. Building that yourself is a lot of work. API Gateway provides it as a managed service.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **HTTP API** | The simpler, cheaper API type – good for most apps. |
| **REST API** | The older, more feature-rich API type. |
| **WebSocket API** | Keeps a two-way connection open, e.g. for chat apps. |
| **Route** | A path and method, e.g. `POST /orders`. |
| **Integration** | What the route sends the request to, e.g. a Lambda function. |
| **Stage** | A version of the API, e.g. `dev` or `prod`. |
| **Throttling** | Limiting how many requests are allowed per second. |

## How it works (step by step)

1. You create an API and add **routes** (e.g. `GET /products`).
2. You connect each route to an **integration** (Lambda, a URL, or another AWS service).
3. You add security (API keys, IAM, Cognito or JWT authorisers).
4. You deploy it to a **stage** and get a URL.
5. Apps call the URL; API Gateway checks, limits and logs each request, then forwards it.

## When to use it

- Serverless back ends with [Lambda](../compute/lambda.md).
- Putting one secure front door on several back-end services.

## When NOT to use it (and what to use instead)

- **Simple websites on servers.** → [Elastic Load Balancing](elastic-load-balancing.md).
- **A single Lambda that just needs a URL.** → Lambda function URLs may be enough.
- **GraphQL APIs.** → [AppSync](../application-integration/appsync.md).

## Real-world example

**Scenario:** A gym builds a mobile app for booking classes.

**The problem:** The app needs a safe way to read the timetable and make bookings.

**How API Gateway helps:** An HTTP API offers `GET /classes` and `POST /bookings`, each linked to a Lambda function. Only signed-in members (checked by [Cognito](../security-identity-compliance/cognito.md)) can book.

**What it looks like:**

```
 Mobile app ──► API Gateway ──► Lambda ──► DynamoDB
                    │
               Cognito (checks the user)
```

## Try it yourself

> ⚠️ **Cost warning:** API Gateway has a Free Tier for new accounts and then charges per million requests. A test API costs almost nothing. Delete it at the end.

**Before you start:** The `hello-function` from the [Lambda page](../compute/lambda.md).

### Option A – Using the AWS Console (clicking in the website)

1. Open **API Gateway** → **Create API** → **HTTP API** → **Build**.
2. **Add integration:** Lambda → choose `hello-function`.
3. **API name:** `hello-api`. Click **Next**.
4. Route: method **GET**, path `/hello`. Click **Next**, keep the `$default` stage, **Next**, **Create**.
5. Copy the **Invoke URL** and open `<invoke-url>/hello` in your browser.

### Option B – Using the AWS CLI (typing commands)

```bash
# "Quick create" an HTTP API that sends every request to a Lambda function
aws apigatewayv2 create-api --name hello-api --protocol-type HTTP \
  --target arn:aws:lambda:eu-west-2:123456789012:function:hello-function
```
(You also need to allow API Gateway to call the function with `aws lambda add-permission`.)

### Option C – Using Terraform (infrastructure as code)

See the [serverless contact form project](../../examples/serverless-contact-form.md) for a full Terraform example.

### Clean up (delete what you made)

1. **API Gateway** → tick `hello-api` → **Delete**.
2. Delete the Lambda function if you no longer need it.

## How much does it cost?

Per million requests (HTTP APIs are cheaper than REST APIs), plus data transfer out. WebSocket APIs charge for messages and connection minutes.

Official pricing: <https://aws.amazon.com/api-gateway/pricing/>

## Security tips

- Always add an authoriser for anything that changes data.
- Set throttling limits to stop abuse and surprise bills.
- Attach [WAF](../security-identity-compliance/waf.md) to REST APIs for extra protection.

## Common mistakes

- Forgetting to give API Gateway permission to call the Lambda function.
- Leaving CORS (browser cross-site rules) unset, so web pages can't call the API.

## Works well with

- [Lambda](../compute/lambda.md), [DynamoDB](../databases/dynamodb.md), [Cognito](../security-identity-compliance/cognito.md).

## Quick check (test yourself)

1. What is an API?
   <details><summary>Answer</summary>A way for programs to talk to each other, usually over web addresses.</details>
2. Which API type is cheaper and simpler for most apps?
   <details><summary>Answer</summary>HTTP API.</details>
3. What is a route?
   <details><summary>Answer</summary>A method and path, like GET /classes.</details>

## Learn more

- [API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)
- [API Gateway pricing](https://aws.amazon.com/api-gateway/pricing/)
