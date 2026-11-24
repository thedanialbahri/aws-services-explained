# Project 5: Classic web app

**Services:** [VPC](../services/networking/vpc.md) + [EC2](../services/compute/ec2.md) + [Auto Scaling](../services/compute/auto-scaling.md) + [Application Load Balancer](../services/networking/elastic-load-balancing.md) + [RDS](../services/databases/rds.md)  **Level:** 🟡 Intermediate

## What you'll build

The classic "three-tier" setup used by countless companies: a load balancer, web servers in two AZs, and a private database.

```
                     Internet
                        │ HTTP :80
           Application Load Balancer (sg: alb)
              ┌─────────┴─────────┐
        EC2 web (AZ a)      EC2 web (AZ b)     ← Auto Scaling group (sg: web)
              └─────────┬─────────┘
                 RDS PostgreSQL (sg: db, not public)
```

Security groups chain together: **internet → alb → web → db**. Nothing else can reach the servers or database.

> 🧭 To keep the code short, this project uses your account's **default VPC**. In a real job you'd build your own VPC with **private subnets** for the servers and database, plus NAT gateways – see the [VPC page](../services/networking/vpc.md).

## Steps

> ⚠️ **Cost warning:** This project uses an ALB (hourly), two EC2 instances, public IPv4 addresses and an RDS database. Some may be covered by the Free Tier, but **expect a small charge** if you leave it running. Build, test and destroy in one sitting.

### Option 1 – Terraform (recommended)

Save as `main.tf`, then run `terraform init`, `terraform plan`, `terraform apply`.

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }
}

provider "aws" {
  region = "eu-west-2"
}

# Use the default VPC and its subnets (one per AZ)
data "aws_vpc" "default" {
  default = true
}

data "aws_subnets" "default" {
  filter {
    name   = "vpc-id"
    values = [data.aws_vpc.default.id]
  }
}

# Latest Amazon Linux 2023 image
data "aws_ssm_parameter" "al2023" {
  name = "/aws/service/ami-amazon-linux-latest/al2023-ami-kernel-default-x86_64"
}

# Firewall for the load balancer: HTTP from anywhere
resource "aws_security_group" "alb" {
  name   = "demo-alb"
  vpc_id = data.aws_vpc.default.id
  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# Firewall for web servers: HTTP only from the load balancer
resource "aws_security_group" "web" {
  name   = "demo-web"
  vpc_id = data.aws_vpc.default.id
  ingress {
    from_port       = 80
    to_port         = 80
    protocol        = "tcp"
    security_groups = [aws_security_group.alb.id]
  }
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# Firewall for the database: PostgreSQL only from web servers
resource "aws_security_group" "db" {
  name   = "demo-db"
  vpc_id = data.aws_vpc.default.id
  ingress {
    from_port       = 5432
    to_port         = 5432
    protocol        = "tcp"
    security_groups = [aws_security_group.web.id]
  }
}

# The load balancer, target group and listener
resource "aws_lb" "web" {
  name               = "demo-alb"
  load_balancer_type = "application"
  security_groups    = [aws_security_group.alb.id]
  subnets            = data.aws_subnets.default.ids
}

resource "aws_lb_target_group" "web" {
  name     = "demo-web"
  port     = 80
  protocol = "HTTP"
  vpc_id   = data.aws_vpc.default.id
  health_check {
    path = "/"
  }
}

resource "aws_lb_listener" "http" {
  load_balancer_arn = aws_lb.web.arn
  port              = 80
  protocol          = "HTTP"
  default_action {
    type             = "forward"
    target_group_arn = aws_lb_target_group.web.arn
  }
}

# Recipe for each web server: install nginx and show the server's name
resource "aws_launch_template" "web" {
  name_prefix            = "demo-web-"
  image_id               = data.aws_ssm_parameter.al2023.value
  instance_type          = "t3.micro"
  vpc_security_group_ids = [aws_security_group.web.id]
  metadata_options {
    http_tokens = "required"
  }
  user_data = base64encode(<<-EOF
    #!/bin/bash
    dnf install -y nginx
    echo "<h1>Hello from $(hostname)</h1>" > /usr/share/nginx/html/index.html
    systemctl enable --now nginx
  EOF
  )
}

# Two web servers spread across AZs, registered with the load balancer
resource "aws_autoscaling_group" "web" {
  name                = "demo-web"
  min_size            = 2
  max_size            = 2
  desired_capacity    = 2
  vpc_zone_identifier = data.aws_subnets.default.ids
  target_group_arns   = [aws_lb_target_group.web.arn]
  health_check_type   = "ELB"
  launch_template {
    id      = aws_launch_template.web.id
    version = "$Latest"
  }
}

# The private database (password stored in Secrets Manager)
resource "aws_db_subnet_group" "db" {
  name       = "demo-db"
  subnet_ids = data.aws_subnets.default.ids
}

resource "aws_db_instance" "db" {
  identifier                  = "demo-db"
  engine                      = "postgres"
  instance_class              = "db.t4g.micro"
  allocated_storage           = 20
  username                    = "appadmin"
  manage_master_user_password = true
  db_subnet_group_name        = aws_db_subnet_group.db.name
  vpc_security_group_ids      = [aws_security_group.db.id]
  publicly_accessible         = false
  storage_encrypted           = true
  skip_final_snapshot         = true # test only!
}

output "website_url" {
  value = "http://${aws_lb.web.dns_name}"
}
```

### Option 2 – Console

Follow these pages in order, using the same security group chain:
1. [Elastic Load Balancing](../services/networking/elastic-load-balancing.md) – target group and ALB.
2. [Auto Scaling](../services/compute/auto-scaling.md) – launch template and group attached to the target group.
3. [RDS](../services/databases/rds.md) – database with **Public access: No** and the `db` security group.

## Test it

1. Open the `website_url` output in your browser.
2. Refresh several times – the hostname changes as the ALB sends you to different servers.
3. Terminate one instance in EC2 – the site keeps working, and Auto Scaling launches a replacement.

## Next steps

- Add HTTPS with an ACM certificate and an HTTPS listener.
- Move servers and the database to private subnets.
- Connect the app to the database using the secret in Secrets Manager.

## Clean up

Run `terraform destroy` and confirm. Check EC2, Load Balancers and RDS are empty afterwards.

## What you learned

- Three-tier architecture with security group chaining.
- High availability across two AZs.
- Self-healing with Auto Scaling and health checks.
