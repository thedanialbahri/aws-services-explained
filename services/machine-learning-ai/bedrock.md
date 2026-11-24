# Amazon Bedrock

**Category:** Machine learning & AI  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Bedrock gives you access to many generative AI models (from Amazon, Anthropic, Meta, Mistral and others) through one AWS API, with your data kept private.

## Real-life comparison

Bedrock is like a food court: many different kitchens (AI models) under one roof, one payment system, and the same seating – you pick the dish that suits you.

## What problem does it solve?

Building generative AI apps means choosing models, handling security and connecting them to your data. Bedrock provides models plus tools like knowledge bases, guardrails and agents, without managing servers.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Foundation model (FM)** | A large AI model trained on huge amounts of data. |
| **Prompt** | The instruction or question you give the model. |
| **Token** | A chunk of text; usage is often charged per token. |
| **Knowledge base** | Connects a model to your documents (RAG – retrieval-augmented generation). |
| **Guardrails** | Filters that block unwanted topics or content. |
| **Agent** | A model that can plan steps and call your APIs. The original Bedrock Agents (now "Bedrock Agents Classic") closed to new customers in July 2026; new agents are built with **Amazon Bedrock AgentCore**. |

## How it works (step by step)

1. Check which models are available in your Region and request access if needed.
2. Try prompts in the **playground**.
3. Call a model from code with the Bedrock Runtime API (e.g. `Converse`).
4. Add a knowledge base or guardrails as needed.

## When to use it

- Chatbots, summaries, drafting, classification, search over your own documents.

## When NOT to use it (and what to use instead)

- **A specific simple task like translation or speech.** → [Translate](translate.md), [Polly](polly.md) – cheaper and simpler.
- **Training your own model from scratch.** → [SageMaker](sagemaker.md).

## Real-world example

**Scenario:** A council wants residents to ask questions about bin collections and parking permits.

**How it helps:** A Bedrock knowledge base indexes the council's web pages; a chatbot answers using that content, with guardrails to stay on topic.

**What it looks like:**

```
 Resident question ──► App ──► Bedrock (model + knowledge base + guardrails) ──► answer with sources
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per input and output token (prices differ by model). A few playground prompts cost very little. There's nothing to delete unless you create knowledge bases or agents.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Bedrock** in a Region with model access.
2. Go to **Playgrounds** → **Chat**.
3. Pick a model and ask: "Explain Amazon S3 to a 15-year-old in three sentences."

### Option B – Using the AWS CLI (typing commands)

```bash
# Send one message to a model (replace the model ID with one you have access to)
aws bedrock-runtime converse --model-id MODEL_ID_HERE \
  --messages '[{"role":"user","content":[{"text":"Explain Amazon S3 in one sentence."}]}]'
```

### Option C – Using Terraform (infrastructure as code)

Not applicable for a first test.

### Clean up (delete what you made)

Delete any knowledge bases, vector stores, guardrails or agents you created – some have ongoing costs.

## How much does it cost?

On-demand per token, batch, or provisioned throughput; knowledge bases also incur vector store costs.

Official pricing: <https://aws.amazon.com/bedrock/pricing/>

## Security tips

- Don't send secrets or unnecessary personal data in prompts.
- Use guardrails and IAM to control which models people can use.

## Common mistakes

- Trusting AI answers without checking – models can be confidently wrong.

## Works well with

- [Lambda](../compute/lambda.md), [S3](../storage/s3.md), [OpenSearch](../analytics/opensearch.md).

## Quick check (test yourself)

1. What is a foundation model?
   <details><summary>Answer</summary>A large AI model trained on huge amounts of data.</details>
2. What does a knowledge base add?
   <details><summary>Answer</summary>Answers based on your own documents.</details>
3. How is Bedrock usually charged?
   <details><summary>Answer</summary>Per token.</details>

## Learn more

- [Amazon Bedrock User Guide](https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-bedrock.html)
- [Bedrock pricing](https://aws.amazon.com/bedrock/pricing/)
