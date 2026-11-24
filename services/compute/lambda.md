# AWS Lambda

**Category:** Compute  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Lambda runs your code only when something triggers it, and you pay only for the time it runs – there are no servers for you to manage.

## Real-life comparison

Lambda is like a taxi instead of owning a car. You don't pay for parking, insurance or servicing. You call it when you need a trip, pay for that trip, and it disappears afterwards. If 100 people need taxis at once, 100 taxis turn up.

## What problem does it solve?

A server that runs 24/7 costs money even when nobody's using it, and you must patch and scale it. Many tasks are small and occasional – resize a photo, process a form, run a nightly clean-up. Lambda runs that code only when needed and scales automatically.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Function** | Your piece of code, uploaded to Lambda. |
| **Runtime** | The language environment, e.g. Python 3.13 or Node.js 22. |
| **Handler** | The part of your code Lambda calls first. |
| **Trigger** (event source) | What starts the function, e.g. a file upload to S3 or an API call. |
| **Event** | The information sent to your function about what happened. |
| **Execution role** | An IAM role that says what your function is allowed to do. |
| **Timeout** | The longest a function can run (up to 15 minutes). |
| **Cold start** | A short delay the first time a function runs after a quiet period. |

## How it works (step by step)

1. You write a function (e.g. in Python) and upload it to Lambda.
2. You give it an **execution role** with only the permissions it needs.
3. You connect a **trigger**, such as "when a file is uploaded to this S3 bucket".
4. When the trigger happens, Lambda starts your code and passes it the **event**.
5. Your code runs, does its job, and finishes.
6. If many events arrive at once, Lambda runs many copies at the same time.
7. You pay per request and for the time your code ran (in milliseconds).

## When to use it

- Reacting to events: file uploads, database changes, messages in a queue.
- The back end of a website or app through [API Gateway](../networking/api-gateway.md).
- Scheduled jobs ("run every night at 2am") with [EventBridge](../application-integration/eventbridge.md).
- Gluing AWS services together.

## When NOT to use it (and what to use instead)

- **Jobs longer than 15 minutes.** → Use [Fargate](../containers/fargate.md), [Batch](batch.md) or [EC2](ec2.md).
- **Apps that need a constant, steady load all day.** A server or container may be cheaper. → [EC2](ec2.md) or [ECS](../containers/ecs.md).
- **Software that needs a specific operating system setup.** → [EC2](ec2.md).

## Real-world example

**Scenario:** Maya runs an online second-hand clothes shop. Sellers upload large photos from their phones.

**The problem:** The big photos make pages slow to load. Resizing them on her server slows the whole site.

**How Lambda helps:** When a photo lands in the `uploads/` folder of an S3 bucket, a Lambda function automatically creates a smaller version and saves it to `thumbnails/`. Maya pays only for the seconds the resizing takes.

**What it looks like:**

```
 Seller uploads photo
        │
        ▼
 S3 bucket: uploads/ ──(event)──► Lambda function ──► S3 bucket: thumbnails/
```

## Try it yourself

> ⚠️ **Cost warning:** Lambda has a generous always-free allowance of requests and compute time each month. A test function costs nothing or almost nothing. Delete it at the end anyway.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Lambda** in the Console (Region **eu-west-2**).
2. Click **Create function** → **Author from scratch**.
3. **Function name:** `hello-function`. **Runtime:** the latest **Python 3** version.
4. Leave **Create a new role with basic Lambda permissions** selected (it can only write logs).
5. Click **Create function**.
6. In the **Code** tab, replace the code with:
   ```python
   def lambda_handler(event, context):
       name = event.get("name", "world")
       return {"message": f"Hello, {name}!"}
   ```
7. Click **Deploy**.
8. Click **Test**, create a test event named `test1` with `{"name": "Danny"}`, and save.
9. Click **Test** again. You'll see `"Hello, Danny!"` in the result.
10. Click the **Monitor** tab → **View CloudWatch logs** to see the log of that run.

### Option B – Using the AWS CLI (typing commands)

```bash
# Run (invoke) the function you made above and save the reply to out.json
aws lambda invoke --function-name hello-function \
  --cli-binary-format raw-in-base64-out \
  --payload '{"name":"CLI"}' out.json

# Show the reply
cat out.json
```

### Option C – Using Terraform (infrastructure as code)

Written for the AWS provider `~> 6.0` and the `hashicorp/archive` provider.

```hcl
# Zip up hello.py (which contains lambda_handler) from the current folder
data "archive_file" "hello" {
  type        = "zip"
  source_file = "hello.py"
  output_path = "hello.zip"
}

# A role Lambda can use, with permission to write logs only
resource "aws_iam_role" "lambda" {
  name = "hello-function-role"
  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Effect    = "Allow"
      Principal = { Service = "lambda.amazonaws.com" }
      Action    = "sts:AssumeRole"
    }]
  })
}

resource "aws_iam_role_policy_attachment" "logs" {
  role       = aws_iam_role.lambda.name
  policy_arn = "arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole"
}

# The function itself
resource "aws_lambda_function" "hello" {
  function_name    = "hello-function"
  role             = aws_iam_role.lambda.arn
  runtime          = "python3.13"
  handler          = "hello.lambda_handler"
  filename         = data.archive_file.hello.output_path
  source_code_hash = data.archive_file.hello.output_base64sha256
}
```

### Clean up (delete what you made)

1. In **Lambda**, tick `hello-function` → **Actions** → **Delete**.
2. In **IAM** → **Roles**, delete the role Lambda created for it (its name starts with `hello-function-role`).
3. In **CloudWatch** → **Log groups**, delete `/aws/lambda/hello-function`.
4. Terraform: `terraform destroy`.

## How much does it cost?

- **Requests** – a small charge per million requests.
- **Duration** – per millisecond of run time, based on how much memory you give the function.
- A free allowance each month covers most learning and small apps.

Official pricing: <https://aws.amazon.com/lambda/pricing/>

## Security tips

- Give each function its **own role** with the least permissions it needs.
- Never put passwords in the code – use [Secrets Manager](../security-identity-compliance/secrets-manager.md).
- Be careful with **function URLs** set to no authentication – anyone can call them.

## Common mistakes

- **Setting the timeout too low** – the default is just 3 seconds.
- **Infinite loops** – a function that writes to the same S3 folder that triggers it will run forever (and cost money).
- **Giving the role full admin access** "to make it work".

## Works well with

- [S3](../storage/s3.md) – trigger functions on file uploads.
- [API Gateway](../networking/api-gateway.md) – turn functions into a web API.
- [DynamoDB](../databases/dynamodb.md) – store data from functions.
- [SQS](../application-integration/sqs.md) – process queued messages.
- [CloudWatch](../management-governance/cloudwatch.md) – logs and metrics for every run.

## Quick check (test yourself)

1. What is the longest a Lambda function can run?
   <details><summary>Answer</summary>15 minutes.</details>
2. What gives a function permission to use other AWS services?
   <details><summary>Answer</summary>Its execution role (an IAM role).</details>
3. Name two things that can trigger a Lambda function.
   <details><summary>Answer</summary>For example: an S3 upload, an API Gateway request, an SQS message, or an EventBridge schedule.</details>

## Learn more

- [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [AWS Lambda pricing](https://aws.amazon.com/lambda/pricing/)
