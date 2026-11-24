# Amazon Braket

**Category:** Specialist  **Level:** 🔴 Advanced
**Last checked against AWS docs:** 2026-11-24 (first draft – needs a human check)

## In one sentence

Braket lets you design and run programs on quantum computers and quantum simulators from different hardware makers.

## Real-life comparison

It's like a science museum that lets you book time on rare, experimental machines without buying one.

## What problem does it solve?

Quantum computers are rare and expensive. Braket gives researchers and learners access to them, plus simulators for practice.

## Key words to know

| Word | What it means in plain English |
|------|-------------------------------|
| **Qubit** | The basic unit of quantum information. |
| **Circuit** | A quantum program. |
| **Simulator** | A normal computer pretending to be a quantum one. |
| **Task / shot** | One run of a circuit / one measurement. |

## How it works (step by step)

1. Write a circuit with the Braket SDK (Python).
2. Run it on a simulator.
3. Optionally run it on real quantum hardware.

## When to use it

- Research, learning, experimenting with quantum algorithms.

## When NOT to use it (and what to use instead)

- **Normal business computing.** → Classical services like [EC2](../compute/ec2.md).

## Real-world example

**Scenario:** A university physics class learns about qubits.

**How it helps:** Students run circuits on simulators, then once on real hardware.

**What it looks like:**

```
 Python notebook ──► Braket ──► simulator / quantum hardware ──► results
```

## Try it yourself

> ⚠️ **Cost warning:** Charged per task and per shot on hardware, per minute on managed simulators, plus notebook instances. A free tier may apply to simulator time – check.

### Option A – Using the AWS Console (clicking in the website)

1. Open **Amazon Braket** → **Devices** to browse available hardware and simulators.

### Option B – Using the AWS CLI (typing commands)

```bash
aws braket search-devices --filters '[]'
```

### Option C – Using Terraform (infrastructure as code)

Not applicable.

### Clean up (delete what you made)

Stop any notebook instances.

## How much does it cost?

Per task and per shot (hardware), per minute (simulators), plus notebooks.

Official pricing: <https://aws.amazon.com/braket/pricing/>

## Security tips

- Standard IAM controls; results are saved to S3 – keep the bucket private.

## Common mistakes

- Leaving notebook instances running.

## Works well with

- [S3](../storage/s3.md).

## Quick check (test yourself)

1. What is a qubit?
   <details><summary>Answer</summary>The basic unit of quantum information.</details>
2. Can you practise without real hardware?
   <details><summary>Answer</summary>Yes, with simulators.</details>
3. Is Braket for everyday business apps?
   <details><summary>Answer</summary>No.</details>

## Learn more

- [Amazon Braket Developer Guide](https://docs.aws.amazon.com/braket/latest/developerguide/what-is-braket.html)
