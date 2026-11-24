# AWS Step Functions

**Category:** Application integration  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Step Functions joins several steps (like Lambda functions and AWS service calls) into a visual workflow, handling the order, retries and errors for you.

## Real-life comparison

It's like a recipe card with a flowchart: "Step 1 boil water. Step 2 if pasta, add salt. If something burns, start again from step 1." Step Functions is the chef following the card exactly.

## What problem does it solve?

Multi-step processes (process payment → reserve stock → send email) get messy when each step calls the next. Step Functions keeps the flow in one place, shows each run visually, and retries failed steps.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **State machine** | The workflow. |
| **State** | One step: Task, Choice, Wait, Parallel, Map and so on. |
| **Execution** | One run of the workflow. |
| **Standard vs Express** | Long-running and auditable vs fast and high-volume. |

## How it works (step by step)

1. Design the workflow in Workflow Studio (drag and drop) or in JSON.
2. Start an execution with some input.
3. Each state runs in order; Step Functions passes data between them.
4. Watch the execution live in the Console.

## When to use it

- Order processing, data pipelines, approval workflows.

## When NOT to use it (and what to use instead)

- **One simple action.** → Just use [Lambda](../compute/lambda.md).

## Real-world example

**Scenario:** A photo-printing site processes orders in steps.

**How it helps:** A state machine charges the card, checks the image, sends to the printer, and emails the customer – retrying the printer step if it fails.

**What it looks like:**

```
 Start → Charge card → Check image → (OK?) → Send to printer → Email customer → End
                                    └─ no ─► Refund → End
```

## Try it yourself

> ⚠️ **Cost warning:** Free allowance of state transitions each month; a few test runs cost nothing.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Step Functions** → **Create state machine** → choose a **template** such as "Hello world" (or a blank one with a **Pass** state).
2. Create it and click **Start execution**.
3. Watch the graph turn green step by step.

### Option B – Using the AWS CLI (typing commands)

```bash
# Start an execution (replace the ARN)
aws stepfunctions start-execution \
  --state-machine-arn arn:aws:states:eu-west-2:123456789012:stateMachine:demo \
  --input '{"name":"test"}'
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_sfn_state_machine`; start with Workflow Studio.

### Clean up (delete what you made)

1. Delete the state machine and any IAM role created for it.

## How much does it cost?

Standard: per state transition. Express: per request and duration.

Official pricing: <https://aws.amazon.com/step-functions/pricing/>

## Security tips

- Give the state machine's role only the permissions its steps need.

## Common mistakes

- Passing very large data between states (there's a size limit) – store it in S3 and pass the key.

## Works well with

- [Lambda](../compute/lambda.md), [DynamoDB](../databases/dynamodb.md), [EventBridge](eventbridge.md).

## Quick check (test yourself)

1. What is a state machine?
   <details><summary>Answer</summary>The workflow made of states (steps).</details>
2. What is an execution?
   <details><summary>Answer</summary>One run of the workflow.</details>
3. Why not pass huge data between states?
   <details><summary>Answer</summary>There's a size limit; store data in S3 instead.</details>

## Learn more

- [AWS Step Functions Developer Guide](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)
- [Step Functions pricing](https://aws.amazon.com/step-functions/pricing/)
