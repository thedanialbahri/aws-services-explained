# Amazon Rekognition

**Category:** Machine learning & AI  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Rekognition analyses images and videos to find objects, text, unsafe content and faces.

## Real-life comparison

It's like a very fast assistant who looks at every photo and writes a list: "dog, beach, sunset, text: 'SALE'".

## What problem does it solve?

Checking thousands of uploaded images by hand is impossible. Rekognition labels and moderates them automatically.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Labels** | Things detected, with a confidence score. |
| **Content moderation** | Spotting unsafe or inappropriate images. |
| **Confidence** | How sure the model is (0–100). |

## How it works (step by step)

1. Send an image (or an S3 location).
2. Call an API like `DetectLabels` or `DetectModerationLabels`.
3. Get back labels with confidence scores.

## When to use it

- Tagging photos, moderating uploads, reading text in images.

## When NOT to use it (and what to use instead)

- **Reading forms and tables from documents.** → [Textract](textract.md).

## Real-world example

**Scenario:** A second-hand marketplace must block inappropriate photos.

**How it helps:** Each upload triggers Lambda, which calls moderation and flags risky images for a human.

**What it looks like:**

```
 Upload to S3 ──► Lambda ──► Rekognition (moderation) ──► approve / send to human review
```

## Try it yourself

> ⚠️ **Cost warning:** Free Tier for some images per month for new accounts; then per image.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Rekognition** → **Label detection** demo.
2. Upload a photo and see the labels.

### Option B – Using the AWS CLI (typing commands)

```bash
aws rekognition detect-labels --max-labels 10 \
  --image '{"S3Object":{"Bucket":"my-example-bucket-12345","Name":"photo.jpg"}}'
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Delete any test images.

## How much does it cost?

Per image analysed, or per minute of video.

Official pricing: <https://aws.amazon.com/rekognition/pricing/>

## Security tips

- Face features raise privacy and legal concerns; follow UK GDPR and get consent.

## Common mistakes

- Treating low-confidence results as facts.

## Works well with

- [S3](../storage/s3.md), [Lambda](../compute/lambda.md).

## Quick check (test yourself)

1. What is a confidence score?
   <details><summary>Answer</summary>How sure the model is about a result.</details>
2. Which API checks for unsafe images?
   <details><summary>Answer</summary>DetectModerationLabels.</details>
3. For forms and tables, which service is better?
   <details><summary>Answer</summary>Textract.</details>

## Learn more

- [Amazon Rekognition Developer Guide](https://docs.aws.amazon.com/rekognition/latest/dg/what-is.html)
