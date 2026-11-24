# Amazon Location Service

**Category:** Front-end web & mobile  **Level:** 🟡 Intermediate
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Location Service adds maps, address search, routes and device tracking to your apps.

## Real-life comparison

It's like building a sat-nav and a delivery-tracking screen into your app without making your own maps.

## What problem does it solve?

Apps often need "find my nearest shop", address autocomplete or "where's my driver?". Location Service provides these as APIs.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Maps** | Map images for your app. |
| **Places** | Address search and geocoding (turning addresses into coordinates). |
| **Routes** | Directions and travel times. |
| **Geofence** | A virtual boundary that triggers events when a device enters or leaves. |
| **Tracker** | Stores device positions. |

## How it works (step by step)

1. Get an API key or use IAM/Cognito for access.
2. Call the Maps, Places or Routes APIs from your app.
3. Optionally send device positions to a tracker and set geofences.

## When to use it

- Store finders, delivery tracking, address forms.

## When NOT to use it (and what to use instead)

- **You're already committed to another map provider's ecosystem.**

## Real-world example

**Scenario:** A florist wants customers to see where their delivery van is.

**How it helps:** The van's phone sends positions to a tracker; the website shows them on a map, and a geofence texts the customer when the van is near.

**What it looks like:**

```
 Van phone ──► Tracker ──► Geofence event ──► SNS text to customer
                  └────► map on website
```

## Try it yourself

> ⚠️ **Cost warning:** Free Tier for a number of requests for new accounts; then per request.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Location Service** and try the **Explore** map demo.

### Option B – Using the AWS CLI (typing commands)

```bash
# List trackers in this Region
aws location list-trackers
```

### Option C – Using Terraform (infrastructure as code)

Possible with `aws_location_tracker` and related resources.

### Clean up (delete what you made)

Delete any trackers, geofence collections and API keys.

## How much does it cost?

Per request for maps, places and routes; per position update for tracking.

Official pricing: <https://aws.amazon.com/location/pricing/>

## Security tips

- Restrict API keys to your website's domain.

## Common mistakes

- Storing more location history than needed (privacy).

## Works well with

- [Amplify](amplify.md), [EventBridge](../application-integration/eventbridge.md), [IoT Core](../iot/iot-core.md).

## Quick check (test yourself)

1. What is a geofence?
   <details><summary>Answer</summary>A virtual boundary that triggers events.</details>
2. What is geocoding?
   <details><summary>Answer</summary>Turning an address into map coordinates.</details>
3. How should you protect API keys?
   <details><summary>Answer</summary>Restrict them to your domain.</details>

## Learn more

- [Amazon Location Service Developer Guide](https://docs.aws.amazon.com/location/latest/developerguide/what-is.html)
