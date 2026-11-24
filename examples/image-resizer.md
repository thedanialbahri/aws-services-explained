# Project 3: Automatic image resizer

**Services:** [S3](../services/storage/s3.md) + [Lambda](../services/compute/lambda.md)  **Level:** 🟡 Intermediate

## What you'll build

Upload a photo to one bucket, and a Lambda function automatically saves a small thumbnail in a second bucket.

```
 You upload photo ──► S3 bucket "uploads" ──(event)──► Lambda (resize) ──► S3 bucket "thumbnails"
```

> ⚠️ **Use two buckets.** If the function wrote back into the bucket that triggers it, it would trigger itself forever (an infinite loop – and a big bill).

## Steps

> ⚠️ **Cost warning:** Lambda and S3 free allowances cover this easily. Delete everything at the end.

### Step 1 – Create two buckets

1. `my-uploads-12345` and `my-thumbnails-12345` in **eu-west-2**, both private.

### Step 2 – Create the function

1. **Lambda** → **Create function** → name `resize-image`, runtime latest **Python 3**.
2. **Configuration** → **General configuration** → set **Timeout** to 30 seconds and **Memory** to 512 MB.
3. **Configuration** → **Environment variables** → add `DEST_BUCKET` = `my-thumbnails-12345`.
4. Paste this code and **Deploy**:

```python
import io
import os
import urllib.parse

import boto3
from PIL import Image  # provided by a Pillow layer (see step 3)

s3 = boto3.client("s3")
DEST = os.environ["DEST_BUCKET"]


def lambda_handler(event, context):
    # One event can contain several uploaded files
    for record in event["Records"]:
        bucket = record["s3"]["bucket"]["name"]
        key = urllib.parse.unquote_plus(record["s3"]["object"]["key"])

        # Download the original image into memory
        original = s3.get_object(Bucket=bucket, Key=key)["Body"].read()
        image = Image.open(io.BytesIO(original))
        image_format = image.format or "JPEG"

        # Shrink it to fit inside 300 x 300 pixels, keeping its shape
        image.thumbnail((300, 300))

        # Save the thumbnail into the destination bucket
        buffer = io.BytesIO()
        image.save(buffer, format=image_format)
        buffer.seek(0)
        s3.put_object(Bucket=DEST, Key=f"thumbnails/{key}", Body=buffer)

    return {"resized": len(event["Records"])}
```

### Step 3 – Add the Pillow library

Pillow (the image library) isn't included in Lambda, so you package it as a **Lambda layer** (a zip of extra libraries that functions can share).

Pillow contains compiled code, so it must be built for **Linux** and for **your function's Python version and architecture** – even if you're on Windows or a Mac. The `--platform` and `--only-binary` options make pip download the right Linux version.

Run these in a terminal (or [CloudShell](../services/developer-tools/cloudshell.md)). Replace `3.13` with your function's Python version (shown under **Runtime settings**), and keep `x86_64` unless you chose arm64:

```bash
# Make a folder. Lambda layers for Python must have a top-level "python" folder
mkdir -p pillow-layer/python && cd pillow-layer

# Download the Linux build of Pillow for Python 3.13 into python/
pip install pillow --platform manylinux2014_x86_64 --only-binary=:all: \
  --python-version 3.13 -t python/

# Zip it up – python/ must be at the root of the zip
zip -r pillow-layer.zip python/

# Upload it as a layer (note the LayerVersionArn in the output)
aws lambda publish-layer-version --layer-name pillow \
  --zip-file fileb://pillow-layer.zip \
  --compatible-runtimes python3.13 --compatible-architectures x86_64

# Attach the layer to your function (paste the LayerVersionArn from above)
aws lambda update-function-configuration --function-name resize-image \
  --layers arn:aws:lambda:eu-west-2:123456789012:layer:pillow:1
```

Prefer clicking? In the function, scroll to **Layers** → **Add a layer** → **Custom layers** → choose `pillow`.

Based on AWS's guide: [Working with layers for Python Lambda functions](https://docs.aws.amazon.com/lambda/latest/dg/python-layers.html).

### Step 4 – Give the function permission

1. **Configuration** → **Permissions** → click the role name.
2. **Add permissions** → **Create inline policy** → JSON:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    { "Effect": "Allow", "Action": "s3:GetObject", "Resource": "arn:aws:s3:::my-uploads-12345/*" },
    { "Effect": "Allow", "Action": "s3:PutObject", "Resource": "arn:aws:s3:::my-thumbnails-12345/thumbnails/*" }
  ]
}
```

### Step 5 – Add the S3 trigger

1. In the function, **Add trigger** → **S3** → bucket `my-uploads-12345` → event **All object create events**.
2. Tick the acknowledgement → **Add**.

### Step 6 – Test

1. Upload a JPG to `my-uploads-12345`.
2. Check `my-thumbnails-12345/thumbnails/` – the small version appears within seconds.
3. If not, check **Monitor** → **View CloudWatch logs**.

## Clean up

1. Delete the function and its log group.
2. Empty and delete both buckets.
3. Delete the layer versions (`aws lambda delete-layer-version --layer-name pillow --version-number 1`) and the function's IAM role.

## What you learned

- Event-driven design: S3 events trigger Lambda.
- Least-privilege permissions for a function.
- Avoiding recursive triggers.
