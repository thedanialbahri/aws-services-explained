# Project 4: Serverless contact form

**Services:** [API Gateway](../services/networking/api-gateway.md) + [Lambda](../services/compute/lambda.md) + [DynamoDB](../services/databases/dynamodb.md) + [SES](../services/business-applications/ses.md)  **Level:** 🟡 Intermediate

## What you'll build

A web form whose submissions are saved in DynamoDB and emailed to you – with no servers.

```
 Web form ──POST /contact──► API Gateway (HTTP API) ──► Lambda ──► DynamoDB (save)
                                                              └──► SES (email you)
```

## Steps

> ⚠️ **Cost warning:** All four services have free allowances; this costs nothing or almost nothing for testing. SES starts in the sandbox (you can only email verified addresses) – that's fine here.

### Step 1 – Verify your email in SES

1. **SES** (eu-west-2) → **Identities** → **Create identity** → **Email address** → yours.
2. Click the link in the verification email.

### Step 2 – Create the DynamoDB table

1. **DynamoDB** → **Create table** → name `ContactMessages`, partition key `id` (String) → create.

### Step 3 – Create the Lambda function

1. **Lambda** → **Create function** → `contact-form`, latest **Python 3**.
2. Environment variables: `TABLE` = `ContactMessages`, `SENDER` = your verified email.
3. Paste the code and **Deploy**:

```python
import json
import os
import time
import uuid

import boto3

table = boto3.resource("dynamodb").Table(os.environ["TABLE"])
ses = boto3.client("sesv2")
SENDER = os.environ["SENDER"]


def lambda_handler(event, context):
    # The form data arrives as a JSON string in the request body
    body = json.loads(event.get("body") or "{}")
    name = body.get("name")
    email = body.get("email")
    message = body.get("message")

    # Reject incomplete submissions
    if not (name and email and message):
        return {"statusCode": 400, "body": json.dumps({"error": "name, email and message are required"})}

    # Save the message
    table.put_item(Item={
        "id": str(uuid.uuid4()),
        "name": name,
        "email": email,
        "message": message,
        "createdAt": int(time.time()),
    })

    # Email it to you
    ses.send_email(
        FromEmailAddress=SENDER,
        Destination={"ToAddresses": [SENDER]},
        Content={"Simple": {
            "Subject": {"Data": f"New contact form message from {name}"},
            "Body": {"Text": {"Data": f"From: {name} <{email}>\n\n{message}"}},
        }},
    )

    return {"statusCode": 200, "body": json.dumps({"ok": True})}
```

### Step 4 – Permissions

Add an inline policy to the function's role (replace the account ID):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    { "Effect": "Allow", "Action": "dynamodb:PutItem",
      "Resource": "arn:aws:dynamodb:eu-west-2:123456789012:table/ContactMessages" },
    { "Effect": "Allow", "Action": "ses:SendEmail", "Resource": "*" }
  ]
}
```

### Step 5 – Create the API

1. **API Gateway** → **Create API** → **HTTP API** → **Build**.
2. Integration: **Lambda** → `contact-form`. Name `contact-api`.
3. Route: **POST** `/contact`. Keep the `$default` stage → **Create**.
4. Under **CORS**, allow your website's origin (or `*` just for testing) and method `POST`, header `content-type`.

### Step 6 – Test

```bash
# Send a test submission (replace the URL with your Invoke URL)
curl -X POST "https://abc123.execute-api.eu-west-2.amazonaws.com/contact" \
  -H "content-type: application/json" \
  -d '{"name":"Test","email":"test@example.com","message":"Hello!"}'
```
Check the DynamoDB table and your inbox.

### Step 7 – A simple form page

```html
<form id="f">
  <input name="name" placeholder="Name" required>
  <input name="email" type="email" placeholder="Email" required>
  <textarea name="message" placeholder="Message" required></textarea>
  <button>Send</button>
</form>
<script>
  // Send the form as JSON to the API
  document.getElementById("f").addEventListener("submit", async (e) => {
    e.preventDefault();
    const data = Object.fromEntries(new FormData(e.target));
    const res = await fetch("https://abc123.execute-api.eu-west-2.amazonaws.com/contact", {
      method: "POST", headers: { "content-type": "application/json" }, body: JSON.stringify(data)
    });
    alert(res.ok ? "Thanks!" : "Something went wrong");
  });
</script>
```
Host it with [Project 2](static-website.md).

## Security notes

- Add throttling on the API stage to stop abuse.
- Consider a CAPTCHA or AWS WAF to reduce spam.
- Lock CORS to your real domain.

## Clean up

1. Delete the API, function (and log group), and table.
2. Delete the SES identity and the function's IAM role.

## What you learned

- Building a serverless back end from four managed services.
- Passing configuration with environment variables.
- Least-privilege permissions.
