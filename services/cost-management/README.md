# Cost management

AWS charges you for what you use, so it's important to **see**, **predict** and **control** your bill.

**Real-life comparison:** Think of a pay-as-you-go phone contract. Billing is your monthly statement, Cost Explorer is the breakdown of what you spent on calls vs data, Budgets is the text that warns you when you're near your limit, the Pricing Calculator is the tariff checker before you sign up, and Savings Plans are like switching to a cheaper fixed contract.

## Services in this category

| Service | Level | What it does |
|---------|-------|--------------|
| [AWS Billing and Cost Management](billing.md) | 🟢 | Shows your bills and payments |
| [AWS Budgets](budgets.md) | 🟢 | Sends alerts when spending goes over a limit |
| [AWS Cost Explorer](cost-explorer.md) | 🟢 | Charts of what you've spent and on what |
| [AWS Pricing Calculator](pricing-calculator.md) | 🟢 | Estimates costs before you build |
| [Savings Plans](savings-plans.md) | 🟡 | Lower prices for committing to spend over 1 or 3 years |
| [Reserved Instances](reserved-instances.md) | 🟡 | Lower prices for committing to specific resources |

## Five habits that stop surprise bills

1. Set a **budget alert** on day one ([Budgets](budgets.md)).
2. **Delete** test resources as soon as you're done.
3. **Tag** resources (e.g. `Project=learning`) so you can see what costs what.
4. Check **Cost Explorer** weekly.
5. Watch for things that cost money even when idle: NAT gateways, load balancers, stopped instances' disks, public IPv4 addresses.

[← Back to the main index](../../README.md)
