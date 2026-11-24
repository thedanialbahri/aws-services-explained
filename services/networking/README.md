# Networking & content delivery

**Networking** is how computers find and talk to each other. **Content delivery** is getting files and web pages to users quickly.

**Real-life comparison:** Networking is the road system. A VPC is your private estate with its own roads and gates, Route 53 is the sat-nav that turns names into addresses, load balancers are traffic police sharing cars between lanes, and CloudFront is a chain of local depots so deliveries arrive faster.

## Services in this category

| Service | Level | What it does |
|---------|-------|--------------|
| [Amazon VPC](vpc.md) | 🟢 | Your own private network inside AWS |
| [Amazon Route 53](route-53.md) | 🟢 | Domain names and DNS (the internet's phone book) |
| [Amazon CloudFront](cloudfront.md) | 🟢 | Delivers your website and files fast from locations near users |
| [Elastic Load Balancing](elastic-load-balancing.md) | 🟢 | Shares incoming traffic across several servers |
| [Amazon API Gateway](api-gateway.md) | 🟡 | Creates and protects APIs for your apps |
| [AWS Site-to-Site VPN](site-to-site-vpn.md) | 🟡 | Encrypted connection between your office and AWS over the internet |
| [AWS Direct Connect](direct-connect.md) | 🔴 | Private physical connection from your building to AWS |
| [AWS Transit Gateway](transit-gateway.md) | 🔴 | A central hub that connects many networks together |
| [AWS PrivateLink](privatelink.md) | 🔴 | Reach services privately without using the public internet |
| [AWS Global Accelerator](global-accelerator.md) | 🔴 | Sends users over AWS's global network for faster, steadier connections |

## Learn them in this order

1. [VPC](vpc.md) – everything else sits inside or around it.
2. [Elastic Load Balancing](elastic-load-balancing.md)
3. [Route 53](route-53.md)
4. [CloudFront](cloudfront.md)
5. Then the 🟡 and 🔴 services as you need them.

[← Back to the main index](../../README.md)
