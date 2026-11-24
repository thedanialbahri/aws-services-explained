# Amazon DynamoDB

**Category:** Databases  **Level:** 🟢 Beginner
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

DynamoDB is a fast, fully managed NoSQL database that stores items by key and scales automatically, with no servers to manage.

## Real-life comparison

DynamoDB is like a giant, perfectly organised coat check. You hand in an item and get a ticket number (the key). When you come back with the ticket, the attendant finds your coat instantly – whether there are 10 coats or 10 million.

## What problem does it solve?

Traditional databases can slow down or need bigger servers as traffic grows. DynamoDB gives consistent single-digit millisecond responses at almost any scale, and you never patch or size a server.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Table** | A collection of items. |
| **Item** | One record, like a row. Items in the same table can have different fields. |
| **Attribute** | One piece of data in an item, e.g. `name`. |
| **Partition key** | The main key used to find an item, e.g. `customerId`. |
| **Sort key** | An optional second key to order items, e.g. `orderDate`. |
| **On-demand** | Pay per request; DynamoDB scales automatically. |
| **Provisioned** | You set the capacity in advance (cheaper for steady traffic). |
| **GSI** (global secondary index) | An extra way to look items up by a different key. |

## How it works (step by step)

1. You create a **table** and choose a **partition key** (and optionally a sort key).
2. You choose **on-demand** or **provisioned** capacity.
3. Your app writes items with `PutItem` and reads them with `GetItem` or `Query`.
4. DynamoDB spreads data across many servers using the partition key.
5. It copies data across three AZs automatically.

## When to use it

- Very high or unpredictable traffic: shopping baskets, game scores, sessions, IoT data.
- Serverless apps with [Lambda](../compute/lambda.md).
- When you know your access patterns ("get all orders for customer X").

## When NOT to use it (and what to use instead)

- **Complex queries joining many tables, or reports you can't plan in advance.** → [RDS](rds.md) or [Aurora](aurora.md).
- **Big analytics.** → [Redshift](redshift.md) or [Athena](../analytics/athena.md).

## Real-world example

**Scenario:** A mobile quiz game has a leaderboard.

**The problem:** On the night a TV advert airs, players jump from 1,000 to 500,000, and the old database crashed.

**How DynamoDB helps:** Scores are stored in an on-demand table with `gameId` as the partition key and `score` in a sort key. DynamoDB scales automatically during the spike.

**What it looks like:**

```
 Players ──► API Gateway ──► Lambda ──► DynamoDB table "Scores"
                                          partition key: gameId
                                          sort key:      score#playerId
```

## Try it yourself

> ⚠️ **Cost warning:** DynamoDB has an always-free allowance of storage and capacity. A small test table costs nothing or almost nothing. Delete it at the end.

### Option A – Using the AWS Console (clicking in the website)

1. Open **DynamoDB** → **Create table**.
2. **Table name:** `Books`. **Partition key:** `isbn` (String).
3. Leave **Default settings** and click **Create table**.
4. When it's **Active**, open it → **Explore table items** → **Create item**.
5. Set `isbn` = `978-0000000001`, then **Add new attribute** → String `title` = `Cloud for Beginners`. Click **Create item**.
6. Add a second item with an extra attribute `pages` (Number) – notice items don't need the same fields.

### Option B – Using the AWS CLI (typing commands)

```bash
# Create an on-demand table with "isbn" as the partition key
aws dynamodb create-table --table-name Books \
  --attribute-definitions AttributeName=isbn,AttributeType=S \
  --key-schema AttributeName=isbn,KeyType=HASH \
  --billing-mode PAY_PER_REQUEST

# Add an item
aws dynamodb put-item --table-name Books \
  --item '{"isbn":{"S":"978-0000000001"},"title":{"S":"Cloud for Beginners"}}'

# Read it back by its key
aws dynamodb get-item --table-name Books --key '{"isbn":{"S":"978-0000000001"}}'
```

### Option C – Using Terraform (infrastructure as code)

Written for the AWS provider `~> 6.0`.

```hcl
# An on-demand table with "isbn" as the partition key
resource "aws_dynamodb_table" "books" {
  name         = "Books"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "isbn"

  attribute {
    name = "isbn"
    type = "S"
  }

  # Keep continuous backups for 35 days
  point_in_time_recovery {
    enabled = true
  }
}
```

### Clean up (delete what you made)

1. **DynamoDB** → **Tables** → tick `Books` → **Delete** → confirm.
2. CLI: `aws dynamodb delete-table --table-name Books`
3. Terraform: `terraform destroy`

## How much does it cost?

- **On-demand:** per million read and write requests.
- **Provisioned:** per hour for the capacity you set.
- **Storage:** per GB per month.
- **Extras:** backups, global tables (copies in other Regions), streams.

Official pricing: <https://aws.amazon.com/dynamodb/pricing/>

## Security tips

- Give each app access to **only its tables** (and even only certain items) with IAM.
- Encryption at rest is always on.
- Turn on **point-in-time recovery** for important tables.

## Common mistakes

- **Using `Scan`** (reading the whole table) instead of `Query` – slow and expensive.
- **Choosing a poor partition key**, e.g. one value used by most items, which creates a "hot" partition.
- **Designing it like a SQL database** – plan your access patterns first.

## Works well with

- [Lambda](../compute/lambda.md) and [API Gateway](../networking/api-gateway.md) – serverless apps.
- [AWS Backup](../storage/backup.md) – scheduled backups.
- DynamoDB Streams + Lambda – react to changes.

## Quick check (test yourself)

1. What is a partition key?
   <details><summary>Answer</summary>The main key DynamoDB uses to store and find an item.</details>
2. Why avoid `Scan`?
   <details><summary>Answer</summary>It reads the whole table, which is slow and costly. Use `Query` with keys instead.</details>
3. Do all items in a table need the same attributes?
   <details><summary>Answer</summary>No, only the key attributes are required.</details>

## Learn more

- [Amazon DynamoDB Developer Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)
- [Amazon DynamoDB pricing](https://aws.amazon.com/dynamodb/pricing/)
