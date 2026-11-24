# Contributing

Thank you for helping! This guide explains how to add a new page or fix an existing one.

You don't need to be an expert. Spotting a confusing sentence or a broken link is a real help.

## Ways to help

- **Fix a mistake** – a wrong fact, a typo or a broken link.
- **Make something clearer** – if a sentence confused you, it will confuse others.
- **Add a missing service** – check the [main index](README.md) for pages marked 📝 Planned.
- **Update an old page** – AWS changes often. Check the "Last checked" date at the top of each page.
- **Add an example project** – see the [`examples/`](examples/) folder.

## How to make a change (step by step)

If you have never used GitHub before, follow these steps exactly.

1. **Fork the repository.** Click the **Fork** button at the top right of the GitHub page. This makes your own copy.
2. **Clone your copy** (download it to your computer):
   ```bash
   git clone https://github.com/YOUR-USERNAME/aws-services-explained.git
   ```
3. **Make a new branch** (a separate line of work, so your changes stay apart from the main copy):
   ```bash
   git checkout -b fix-s3-typo
   ```
4. **Make your changes.** For a new service page, copy [`templates/service-template.md`](templates/service-template.md) into the right folder under `services/`.
5. **Save your work in Git** (a "commit" is a saved snapshot of your changes):
   ```bash
   git add .
   git commit -m "Fix typo in S3 page"
   ```
6. **Upload your branch** to your copy on GitHub:
   ```bash
   git push origin fix-s3-typo
   ```
7. **Open a pull request** (a request asking us to add your changes). Go to your fork on GitHub and click **Compare & pull request**. Explain what you changed and why.

## Writing rules

Every page must follow these rules. They keep the whole repository easy to read.

1. **Use simple English.** Short sentences. Common words. One idea per sentence.
2. **Use British English spelling** – "organise", "colour", "centre", "licence" (noun).
3. **Explain every technical word the first time you use it.** Put the simple meaning in brackets straight after it.
   - ✅ "EC2 gives you a virtual server (a computer that runs inside AWS's data centre instead of on your desk)."
   - ❌ "EC2 provides resizable compute capacity."
4. **Use a real-life comparison** for every service.
5. **Never skip a step.** Number every step, even the small ones.
6. **Show, don't just tell.** Every service needs a real-world example.
7. **No marketing language.** Don't write "powerful", "seamless" or "cutting-edge". Say what it actually does.
8. **Be honest about limits.** Say when a service is *not* a good choice and what to use instead.
9. **Keep pages short** – about 5 minutes to read. Link to the official docs for more detail.

> **The test:** if a 15-year-old with an interest in computers can't follow it, rewrite it.

## Accuracy rules

- **Check facts** against the official [AWS documentation](https://docs.aws.amazon.com/).
- **Not sure?** Say so on the page and add `<!-- TODO: verify -->` next to it. Don't guess.
- **No fixed prices.** Explain *how* a service is charged (per hour, per GB, per request) and link to the pricing page. Prices change; links don't go out of date as fast.
- **Update the "Last checked" date** whenever you check a page against the AWS docs.

## Security rules for examples

- **Never include real secrets.** No real access keys, passwords or account IDs. Use placeholders:
  - Account ID: `123456789012`
  - Bucket name: `my-example-bucket`
  - Region: `eu-west-2` (London)
- **Use the least permissions needed** (only give access to what the example actually uses).
- **Don't make things public** unless the example needs it. If it does, add a clear warning.
- **Always include clean-up steps**, so readers don't get a surprise bill.

## Code rules

- **Code must run.** Test CLI commands and Terraform before you submit them.
- **Comment every command** – a line above it saying what it does.
- **Say which Terraform AWS provider version** you tested with.

## File and folder names

- Lowercase, with hyphens instead of spaces: `elastic-beanstalk.md`, not `Elastic Beanstalk.md`.
- Put each service in its category folder under `services/`.
- Add the new page to the category's `README.md` **and** the [main index](README.md).

## Retired services

If AWS closes a service to new customers or shuts it down, keep the page but put this at the very top:

```markdown
> ⛔ **No longer available to new customers.** Use [alternative] instead.
```

Check the official [AWS product lifecycle page](https://aws.amazon.com/products/lifecycle/) for the latest status.

## Checklist before you open a pull request

- [ ] The page follows the template, with every heading in order
- [ ] Every technical word is explained the first time it's used
- [ ] British English spelling
- [ ] No fixed prices
- [ ] No real keys, passwords or account IDs
- [ ] Clean-up steps included
- [ ] "Last checked" date added
- [ ] All links work
- [ ] Page added to the category `README.md` and the main `README.md`

## Be kind

Everyone here is learning, including the people who wrote the pages. Be patient and polite in issues and pull requests.
