# Amazon Textract

**Category:** Machine learning & AI  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Textract reads printed and handwritten text, forms and tables from scanned documents and photos.

## Real-life comparison

It's like a data-entry clerk who reads invoices and forms and types the important boxes into a spreadsheet – in seconds.

## What problem does it solve?

Basic OCR (optical character recognition) gives you a jumble of words. Textract also understands structure: which value belongs to which form field, and which cell is in which table row.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **OCR** | Turning images of text into real text. |
| **Forms (key-value pairs)** | E.g. "Name: Jo Smith". |
| **Tables** | Rows and columns kept in order. |
| **AnalyzeExpense / AnalyzeID** | Special APIs for receipts/invoices and identity documents. |

## How it works (step by step)

1. Upload a document image or PDF (often to S3).
2. Call `DetectDocumentText` or `AnalyzeDocument`.
3. Get structured JSON with text, forms and tables.

## When to use it

- Invoices, application forms, receipts, contracts.

## When NOT to use it (and what to use instead)

- **Photos of everyday scenes.** → [Rekognition](rekognition.md).

## Real-world example

**Scenario:** An accountancy firm receives hundreds of scanned invoices.

**How it helps:** Textract extracts supplier, date and total from each, ready for the accounts system.

**What it looks like:**

```
 Scanned invoice (S3) ──► Textract (AnalyzeExpense) ──► supplier, date, total
```

## Try it yourself

> ⚠️ **Cost warning:** Free Tier for some pages per month for new accounts; then per page.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Textract** → **Try Amazon Textract**.
2. Upload a sample form and view the Forms and Tables tabs.

### Option B – Using the AWS CLI (typing commands)

```bash
aws textract detect-document-text \
  --document '{"S3Object":{"Bucket":"my-example-bucket-12345","Name":"form.png"}}'
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Delete test documents.

## How much does it cost?

Per page, depending on the features used.

Official pricing: <https://aws.amazon.com/textract/pricing/>

## Security tips

- Documents often contain personal data – encrypt, restrict access and delete promptly.

## Common mistakes

- Using the most expensive API when plain text detection would do.

## Works well with

- [S3](../storage/s3.md), [Lambda](../compute/lambda.md), [Comprehend](comprehend.md).

## Quick check (test yourself)

1. What is OCR?
   <details><summary>Answer</summary>Turning images of text into real text.</details>
2. What does Textract add beyond OCR?
   <details><summary>Answer</summary>Understanding of forms and tables.</details>
3. Which API suits receipts?
   <details><summary>Answer</summary>AnalyzeExpense.</details>

## Learn more

- [Amazon Textract Developer Guide](https://docs.aws.amazon.com/textract/latest/dg/what-is.html)
