# Start here

New to the cloud? Read this page first. It takes about 10 minutes.

By the end you'll know:

1. [What "the cloud" is](#1-what-is-the-cloud)
2. [What AWS is](#2-what-is-aws)
3. [How AWS is organised around the world](#3-how-aws-is-organised-regions-availability-zones-and-edge-locations)
4. [Who looks after what: AWS or you](#4-who-looks-after-what-the-shared-responsibility-model)
5. [How to create a free AWS account safely](#5-create-your-aws-account-safely)

---

## 1. What is the cloud?

### The real-life comparison: renting a flat vs building a house

Imagine you need somewhere to live.

- **Building a house** – you buy land, pay builders, wait months, and fix the roof yourself when it leaks. If your family grows, you must build an extension.
- **Renting a flat** – you move in next week. The landlord fixes the boiler. If you need more space, you move to a bigger flat. You pay monthly, only for what you use.

Running your own servers is like building a house. **Using the cloud is like renting a flat.**

### In plain English

"The cloud" means **using someone else's computers over the internet**, instead of buying and running your own.

Those computers sit in huge buildings called **data centres** (warehouses full of computers, with backup power, cooling and security guards).

### Why people use it

| Old way (your own servers) | Cloud way |
|----------------------------|-----------|
| Buy servers up front (big cost) | Pay as you go (small, regular cost) |
| Wait weeks for new hardware to arrive | Get a new server in minutes |
| Guess how much you'll need | Add or remove capacity when you need to |
| You fix broken hardware | The cloud provider fixes it |
| Your servers sit in one building | Run your app in many countries |

### When the cloud is *not* cheaper

Be honest with yourself: the cloud isn't always the cheapest option. If you run the same large workload 24 hours a day for years, owning your own hardware can cost less. The cloud is best when you need speed, flexibility, or don't want to manage hardware.

---

## 2. What is AWS?

**AWS (Amazon Web Services)** is Amazon's cloud. It's one of the biggest cloud providers in the world. Others include Microsoft Azure and Google Cloud.

AWS offers hundreds of **services** (individual tools, each with one job). For example:

- **EC2** gives you a virtual server (a computer that runs inside AWS's data centre instead of on your desk).
- **S3** stores files – like a huge online storage unit.
- **IAM** controls who is allowed to do what in your account – like handing out keys to different rooms.

You don't need to learn all of them. Most real jobs use 10–20 core services. The [learning paths](LEARNING-PATHS.md) show you where to start.

### Three ways to use AWS

| Way | What it is | Good for |
|-----|-----------|----------|
| **AWS Console** | The website. You click buttons. | Learning, one-off tasks |
| **AWS CLI** (Command Line Interface) | You type commands in a terminal. | Repeating tasks, scripts |
| **Infrastructure as code** (e.g. Terraform, CloudFormation) | You write files that describe what you want. A tool builds it for you. | Real projects, teams, repeatable setups |

Most pages in this repo show all three.

---

## 3. How AWS is organised: Regions, Availability Zones and edge locations

AWS has data centres all over the world. They are grouped in three layers.

### Region

A **Region** is a geographical area, such as London, Ireland or Tokyo. Each Region is completely separate from the others.

- Example: `eu-west-2` is the London Region.
- You choose the Region when you create something. Pick one close to your users, so things load faster.
- Some laws say data must stay in a certain country. Regions help you follow those rules.

### Availability Zone (AZ)

Each Region contains several **Availability Zones** (AZs). An AZ is one or more data centres with its own power, cooling and network.

AZs in the same Region are miles apart, but linked by very fast connections. If one AZ has a power cut or flood, the others keep running.

- Example: `eu-west-2a`, `eu-west-2b` and `eu-west-2c` are AZs in London.

**Real-life comparison:** A Region is a city. AZs are separate hospitals in that city. If one hospital loses power, patients can go to another.

### Edge location

An **edge location** is a smaller site in a busy city, used to deliver content (like videos and images) quickly to people nearby. There are many more edge locations than Regions.

**Real-life comparison:** A Region is a big central warehouse. Edge locations are local corner shops that keep popular items in stock, so you don't have to travel to the warehouse.

### The diagram

```
                          🌍 AWS GLOBAL NETWORK
 ┌──────────────────────────────────────────────────────────────┐
 │                                                              │
 │  REGION: London (eu-west-2)       REGION: Ireland (eu-west-1)│
 │  ┌──────────────────────────┐     ┌────────────────────────┐ │
 │  │ ┌──────┐┌──────┐┌──────┐ │     │ ┌──────┐┌──────┐┌─────┐│ │
 │  │ │ AZ a ││ AZ b ││ AZ c │ │     │ │ AZ a ││ AZ b ││AZ c ││ │
 │  │ │ 🏢🏢 ││ 🏢🏢 ││ 🏢   │ │     │ │ 🏢🏢 ││ 🏢   ││ 🏢🏢││ │
 │  │ └──────┘└──────┘└──────┘ │     │ └──────┘└──────┘└─────┘│ │
 │  └──────────────────────────┘     └────────────────────────┘ │
 │                                                              │
 │   📍 Edge locations: Manchester, London, Dublin, Paris ...   │
 │      (small sites close to users, for fast delivery)         │
 └──────────────────────────────────────────────────────────────┘

 🏢 = a data centre
```

The exact number of Regions, AZs and edge locations keeps growing. See the official [AWS Global Infrastructure page](https://aws.amazon.com/about-aws/global-infrastructure/) for today's numbers.

### Global vs regional services

- Most services are **regional** – what you create in London stays in London.
- A few are **global** – for example, IAM (users and permissions) and Route 53 (domain names) work across all Regions.

> 💡 **Common beginner mistake:** You create something, then can't find it. Check the Region selector at the top right of the Console. You're probably looking in the wrong Region.

---

## 4. Who looks after what: the shared responsibility model

Security in AWS is a shared job. AWS looks after some things. You look after others.

**Real-life comparison:** You rent a flat in a block.
- The **landlord** looks after the building: the front door lock, the walls, the fire alarms in the hallway.
- **You** look after your flat: locking your own door, who you give spare keys to, and what you keep inside.

| AWS is responsible for... ("security **of** the cloud") | You are responsible for... ("security **in** the cloud") |
|--------------------------------------------------------|---------------------------------------------------------|
| The physical data centres (guards, fences, cameras) | Who can log in to your account (IAM, MFA) |
| The hardware (servers, disks, network cables) | Your data, and whether it's encrypted |
| The software that runs the cloud itself | Settings, like whether a storage bucket is public |
| The global network | Updating the operating system on your own servers (EC2) |
| | Firewall rules for your servers |

**The more AWS manages, the less you manage.**

- With **EC2** (your own virtual server), you must patch (update) the operating system yourself.
- With **Lambda** (AWS runs your code for you), AWS handles the operating system. You just look after your code and permissions.

Read the official version: [AWS Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/).

---

## 5. Create your AWS account safely

Follow every step. Steps 3–6 protect you from hackers and surprise bills.

> ⚠️ **Cost warning:** AWS has a Free Tier (a set amount of free use for new accounts). The rules for it have changed over time, so read the current [AWS Free Tier page](https://aws.amazon.com/free/) before you start. Outside the Free Tier, **you pay for what you use**. A billing alert (step 6) warns you early.

### Step 1 – Get ready

You'll need:
- An email address (use one you check often – AWS sends billing warnings here)
- A mobile phone (for a verification code)
- A debit or credit card (AWS needs it to confirm who you are, even for the Free Tier)
- An authenticator app on your phone, such as Google Authenticator or Microsoft Authenticator (for MFA – see step 3)

### Step 2 – Sign up

1. Go to <https://aws.amazon.com/> and click **Create an AWS Account**.
2. Enter your email address and an account name (e.g. `my-learning-account`).
3. Confirm your email with the code AWS sends you.
4. Create a **strong password** (long, unique, not used anywhere else). Save it in a password manager.
5. Enter your contact details and card details.
6. Confirm your phone number with the code AWS sends.
7. Choose the **Basic support** plan (it's free).
8. Sign in to the Console.

You are now signed in as the **root user**.

### Step 3 – Turn on MFA for the root user

The **root user** is the owner of the account. It can do *anything*, including deleting everything and closing the account. If someone steals the root password, they own your account.

**MFA (multi-factor authentication)** means you need two things to log in: your password *and* a code from your phone. A stolen password alone isn't enough.

**Real-life comparison:** A password is a key. MFA is a key *plus* a PIN. A thief with just the key can't get in.

1. In the Console, click your account name (top right) → **Security credentials**.
2. Under **Multi-factor authentication (MFA)**, click **Assign MFA device**.
3. Give it a name, choose **Authenticator app**, and click **Next**.
4. Open your authenticator app and scan the QR code on screen.
5. Type in two codes in a row from the app.
6. Click **Add MFA**.

### Step 4 – Don't use the root user day to day

Using the root user for everyday work is like carrying the master key to the whole building everywhere you go. If you lose it, everything is at risk.

Instead, create a separate login for daily work:

1. Search for **IAM Identity Center** in the Console search bar and open it. (This is AWS's recommended way to give people logins.)
2. Click **Enable**.
3. Create a **user** for yourself.
4. Give that user a **permission set** (a list of what they're allowed to do). For learning, `AdministratorAccess` is common, but see the note below.
5. Sign in with the new user using the **AWS access portal URL** that Identity Center shows you.
6. Bookmark that URL. Use it every day from now on.
7. Turn on MFA for this user too.

> 🔒 **About permissions:** In a real job, you'd give people the **least privilege** (only the permissions they actually need). For a personal learning account, admin access is normal – but never share those logins.

Full guide: [IAM Identity Center – Getting started](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html).

### Step 5 – Never create root access keys

**Access keys** are a username-and-password pair for programs (like the AWS CLI). If root access keys leak – for example, you accidentally upload them to GitHub – anyone can control your whole account.

- Don't create access keys for the root user.
- For the CLI, sign in with IAM Identity Center using `aws configure sso` instead of long-term keys.

### Step 6 – Set a billing alert

A billing alert emails you if your spending goes over an amount you choose. This is your safety net.

1. Sign in (root user or a user with billing access).
2. Search for **Budgets** in the Console search bar and open it.
3. Click **Create budget**.
4. Choose **Use a template (simplified)**.
5. Choose **Zero spend budget** (warns you as soon as you spend anything) or **Monthly cost budget** (warns you when you pass an amount you choose, e.g. £5).
6. Enter the email address where you want the warning sent.
7. Click **Create budget**.

> 💡 Prices in AWS are shown in US dollars (USD) by default.

### Step 7 – Choose your Region

At the top right of the Console, pick a Region. If you're in the UK, **Europe (London) `eu-west-2`** is a good default. Use the same Region every time while you learn, so you can always find what you made.

### ✅ You're ready

Your account now has:

- [x] A strong root password, saved in a password manager
- [x] MFA on the root user
- [x] A separate everyday user (not root)
- [x] No root access keys
- [x] A billing alert

**Next step:** Pick a [learning path](LEARNING-PATHS.md), or jump straight to the [main index](README.md).

---

## Quick check (test yourself)

1. What's the difference between a Region and an Availability Zone?
   <details><summary>Answer</summary>A Region is a geographical area (like London). An Availability Zone is one or more separate data centres inside a Region. A Region has several AZs, so if one fails the others keep running.</details>
2. Under the shared responsibility model, who is responsible for updating the operating system on an EC2 server?
   <details><summary>Answer</summary>You are. AWS looks after the physical hardware, but the operating system on your EC2 server is your job.</details>
3. Why shouldn't you use the root user for everyday work?
   <details><summary>Answer</summary>The root user can do anything, including deleting the whole account. If its login is stolen, everything is at risk. Use a separate user with only the permissions you need.</details>
