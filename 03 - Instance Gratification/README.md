# Day 3: Instance Gratification ⚡️

Day 3 of the #30DayTerraformChallenge was pure **instance gratification** – no more just talking about cloud infrastructure, but actually deploying it and watching code bring resources to life!

---

## 🚀 Quick Wins of the Day:

I achieved two key deployments:
- ✅ A 🖥️ **Single Server** — a basic standalone EC2 instance with no configurations.
- ✅ A 🌐 **Web Server** — an EC2 instance that auto-installs Apache and serves a custom web page using `user_data`. (a fully functional web server)
Seeing `terraform apply` work its magic? Priceless! ✨

---

## 🧠 Key Differences: Single Server vs Web Server

| Feature | Single Server 🖥️ | Web Server 🌐 |
|------|---------|---------|
| **Purpose** | Basic EC2 VM | Hosts a website | 
| **User Data Script** | ❌ No | ✅ Installs Apache & HTML |
| **HTTP Access** | ❌ No | ✅ Yes |
| **Visible in Browser** | ❌ No | ✅ Yes |

---

## 1. The Simple Start: Deploying a Basic EC2 Instance 👶

- Every cloud journey begins somewhere, and for me, it was a fundamental EC2 instance. This represents the simplest form of compute in AWS – a virtual server spun up straight from code.

---

## 🖥️ Single Server: Basic EC2 Setup

- This is a minimal EC2 instance — no web server, no automation, just a VM in the cloud.
- **Why deploy this?** To confirm my Day 2 setup was solid and to witness the raw power of `terraform apply` in action for basic resource creation.

**📜 Code: single-server.tf**

```terraform
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "af-south-1"
}

resource "aws_instance" "single-server" {
  ami           = "ami-0914bddde8faa93a0" # Amazon Linux 2023 AMI
  instance_type = "t3.micro"
  key_name      = "cloudykey"

  tags = {
    Name = "single-server"
  }
}
```
### 💬 Code Comments:

- **provider "aws"**: Your entry point to AWS, specifying the region (af-south-1 for Nairobi vibes! 🌍).
- **resource "aws_instance"**: The core block for creating an EC2 VM.
- **ami**: The Amazon Machine Image – essentially the operating system pre-configured.
- **instance_type**: Defines the CPU, memory, and networking capacity (e.g., t3.micro is usually free-tier eligible).
- **key_name**: Links to your SSH key pair for secure remote access.
- **tags**: Simple key-value pairs for organizing and identifying your resources in AWS.


![Single Server](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/770v2s44au0v4a73d2rw.png)



---

## 2. Beyond Basic: Spinning Up A Web Server! 🌐

- This EC2 instance runs a startup script to install Apache and serve a static HTML page.

## 🌐 Web Server: With Apache and HTML Page

- Why deploy this? To demonstrate automating server configuration post-launch (user_data) and managing network traffic (Security Groups).

**📜 Code: web-server.tf**

```terraform
# Terraform 0.13 and later:

terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

# Configure the AWS provider
provider "aws" {
  region = "af-south-1" # Specify your desired AWS Region
}

# Create an EC2 Instance
resource "aws_instance" "web-server" {
  ami                    = "ami-0914bddde8faa93a0" # Amazon Linux 2023 AMI ID for af-south-1
  instance_type          = "t3.micro"             # Free tier eligible
  key_name               = "cloudykey"
  vpc_security_group_ids = [aws_security_group.web-server-sg.id]
  user_data = <<-EOF
              #!/bin/bash
              sudo yum update -y           # Update all installed packages
              sudo yum install -y httpd    # Install Apache Web Server
              sudo systemctl start httpd   # Start the Apache Web Server Service
              sudo systemctl enable httpd  # Configure Apache to start on every reboot

              echo "<!DOCTYPE html>
              <html>
              <head><title>We Are Live, Baby!🚀🎉🥳</title></head>
              <body style='background-color:#1e1e1e; color:#00ffcc; text-align:center; padding-top:15%; font-family:monospace;'>
              <p>Infrastructure as Code? More like <strong>Magic as Code!😂💫✨</strong></p>
              </body>
              </html>" > /var/www/html/index.html
              EOF

  tags = {
    Name = "web-server"
  }
}

# Data source to Default VPC
data "aws_vpc" "default_vpc" {
  default = true
}

resource "aws_security_group" "web-server-sg" {
  name        = "web-server-ssh-http-sg"
  description = "Allow SSH and HTTP inbound traffic for web server"
  vpc_id      = data.aws_vpc.default_vpc.id # Or hardcode your VPC ID

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"] # From ANYWHERE - Be cautious! Wide open for testing only
    description = "Allow SSH"
  }

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"] # From ANYWHERE - Be cautious! Wide open for testing only
    description = "Allow HTTP"
  }

  egress {
    from_port   = 0     # All Ports
    to_port     = 0     # All Ports
    protocol    = "-1"  # All Protocols
    cidr_blocks = ["0.0.0.0/0"] # To ANYWHERE
  }
}
```

### 💬 Code Comments & What's New:

- **user_data Power**: This is where the real "Magic as Code" shines! It's a bash script that runs when the instance first launches. I used it to:
 * ➡️ Update packages, install Apache.
 * ➡️ Start/enable the Apache service.
 * ➡️ Create my awesome custom HTML welcome page:"Infrastructure as Code? More like Magic as Code!😂💫✨"
- **aws_security_group**: This acts as a virtual firewall for your server.
 * 🔒 It allows Port 22 (SSH) for secure remote access.
 * 🔒 It allows Port 80 (HTTP) so web browsers can connect to our page.
 * 🔒 Caution: 0.0.0.0/0 means "from anywhere." Super easy for testing, but in production, you'd restrict this to known IPs for better security!
- **data "aws_vpc" "default_vpc"**: A neat way to reference your default VPC without hardcoding its ID.


![Web Server](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/r950lcmb1ab0qqt0piz5.png)



![Web Server Live](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pxsb9hsabrhp4v38nn0a.png)




---

## 🧪 The Terraform Lifecycle: From Code to Cloud (and Back!) 🔁

I truly experienced the core Terraform workflow:

- ➡️ **terraform init**: Initializes the working directory, downloading necessary provider plugins (like hashicorp/aws). It's the setup step.
- ➡️ **terraform plan**: Before applying any changes, terraform plan shows you exactly what Terraform will do. It's a crucial "dry run" to avoid surprises!
- ➡️ **terraform apply**: Brings your infrastructure to life! It executes the changes outlined in the plan, creating, updating, or deleting resources in your cloud provider.
- ➡️ **terraform destroy**: The responsible cleanup crew! This command tears down all the resources managed by your Terraform configuration. Crucial for avoiding unwanted cloud costs! 💰

---

## 💡 Brain Bytes from Day 3 🧠

- **'terraform apply' is Real Power!**: Transforms code into live cloud infrastructure.
- **Layered Deployments**: Start simple, build complexity.
- **'user_data'** for Automation: Automates server setup right after launch.
- **Security Groups as Firewalls**: Essential for controlling network access.
- **Full Lifecycle**: Remember init -> plan -> apply -> destroy!
Budgeting: Always terraform destroy when done!

---

## What's Next? ➡️

- Day 3: Mission accomplished! Code was tangible and deployed real infrastructure. 
- Stay tuned for more awesome automation on Day 4!

---

## 🔗 Biteʒ 3 Blog Post:

* **Read the full detailed post on dev.to:** [Instance Gratification](https://dev.to/mercyndonga/terra-bitez-3-instance-gratification-3bol)

---
