# Amazon Managed Blockchain (AMB)

**Category:** Specialist  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Managed Blockchain lets you run or connect to blockchain networks (like Ethereum or Hyperledger Fabric) without managing the servers.

## Real-life comparison

A blockchain is like a shared ledger book that many people hold copies of; nobody can secretly change a page. AMB runs your copy of the book for you.

## What problem does it solve?

Running blockchain nodes is technical and needs constant upkeep. AMB provides managed nodes and APIs.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Blockchain** | A shared, tamper-evident record of transactions. |
| **Node** | A computer that keeps a copy of the ledger. |
| **Hyperledger Fabric** | A private, permissioned blockchain framework. |

## How it works (step by step)

1. Choose a network type (public Ethereum access or private Fabric).
2. Create nodes or use AMB Access APIs.
3. Your apps read and write through those nodes.

## When to use it

- Shared records between organisations that don't fully trust each other.

## When NOT to use it (and what to use instead)

- **A normal database would do the job** (most cases). → [RDS](../databases/rds.md) or [DynamoDB](../databases/dynamodb.md).

## Real-world example

**Scenario:** Several shipping companies want a shared record of container handovers.

**How it helps:** A private Fabric network on AMB records each handover; every company has a copy.

**What it looks like:**

```
 Company A node ─┐
 Company B node ─┼── shared ledger (AMB)
 Company C node ─┘
```

## Try it yourself

> ⚠️ **Cost warning:** Nodes are charged per hour. Only browse unless you have a real need.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Managed Blockchain** and read the options.

### Option B – Using the AWS CLI (typing commands)

```bash
aws managedblockchain list-networks
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Delete any nodes or networks you created.

## How much does it cost?

Per node-hour, storage and requests, depending on the network.

Official pricing: <https://aws.amazon.com/managed-blockchain/pricing/>

## Security tips

- Protect keys and wallets carefully – lost keys can't be recovered.

## Common mistakes

- Using a blockchain where a database is simpler.

## Works well with

- [Lambda](../compute/lambda.md), [KMS](../security-identity-compliance/kms.md).

## Quick check (test yourself)

1. What is a node?
   <details><summary>Answer</summary>A computer keeping a copy of the ledger.</details>
2. Is a blockchain usually better than a database?
   <details><summary>Answer</summary>No – only for specific shared-trust cases.</details>
3. Name a private blockchain framework.
   <details><summary>Answer</summary>Hyperledger Fabric.</details>

## Learn more

- [Amazon Managed Blockchain documentation](https://docs.aws.amazon.com/managed-blockchain/)
