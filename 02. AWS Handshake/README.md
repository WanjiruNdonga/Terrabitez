# Day 2: AWS Handshake 🤝

**TerraBiteʒ** challenge, Day 1 was all about setting up the workstation. Day 2, it's time to teach Terraform how to talk to AWS – because what's IaC without a cloud to manage? It's all about establishing that crucial handshake! 🤝☁️

---

## The Essentials: Connecting Terraform to AWS 🔑

This day was focused on ensuring my newly installed Terraform CLI and AWS CLI could properly authenticate and communicate with my AWS account.

### 1. AWS Account Setup (If Not Done Yet)

* **Action:** Created/verified my AWS account.
* **Key Step:** Set up an IAM User with **Programmatic Access** and obtained the Access Key ID and Secret Access Key. (This is *crucial* for CLI/Terraform access, *not* your root account credentials!)
* **Security Note:** Remember to store these keys securely and ideally use IAM roles/temporary credentials in production environments. For learning, direct access keys are common.

### 2. AWS CLI Configuration ☁️

Even though the AWS CLI was installed on Day 1, today was about getting it *configured* to point to my specific AWS account.

* **Command:** I used `aws configure` in PowerShell.
* **Inputs:**
    * `AWS Access Key ID`: (Pasted my Access Key ID)
    * `AWS Secret Access Key`: (Pasted my Secret Access Key)
    * `Default region name`: `[Your AWS Region]` (e.g., `us-east-1` or `eu-west-2`)
    * `Default output format`: `json` (or `text`, `table`)

### 3. Verification Checkpoint ✅

To ensure Terraform and AWS are truly talking to each other, I performed a quick check:

* **AWS CLI Check:**
    ```bash
    aws sts get-caller-identity
    ```
* **Expected Output:** This should tell you about the IAM user you configured, confirming AWS CLI is working.

        ```json
        {
          "UserId": "AIDACKCEVSQ6C2EXAMPLE",
          "Account": "123456789012",
          "Arn": "arn:aws:iam::123456789012:user/my-iam-user"
        }
        ```

* **Terraform Check:**
    After `terraform init`, the presence of the `.terraform` directory and no errors indicate success.

### 4. Terraform AWS Provider Configuration 🏗️

This is where Terraform truly begins its conversation with AWS.

* **Action:** Created a `main.tf` file in my `02-aws-handshake` folder.
* **Content:** Added the basic AWS provider block. Terraform automatically looks for AWS credentials configured by `aws configure` or environment variables.

    ```terraform
    terraform {
      required_providers {
        aws = {
          source  = "hashicorp/aws"
          version = "~> 5.0" # Use a version compatible with your setup
        }
      }
    }

    # Configure the AWS Provider
    provider "aws" {
      region = "[Your AWS Region]" # e.g., "af-south-1"
      # No need to specify access_key/secret_key here if configured via AWS CLI
    }
    ```

* **Initialization:** Ran `terraform init` in PowerShell from the directory containing `main.tf`. This downloads the necessary AWS provider plugin.
    ```bash
    terraform init
    ```
---

## Troubleshooting Corner 🚧

* **`Error: No valid credential sources found`**: This is a classic! Usually means your `aws configure` wasn't done correctly, or Terraform can't find your `~/.aws/credentials` file. Double-check your `aws configure` steps.
* **Region Mismatch:** Ensure the region in your `provider "aws" {}` block matches your AWS CLI configuration, or where you intend to deploy resources.

---

## What's Next? ➡️

Terraform and AWS are now officially shaking hands! Day 2 wrapped up the critical authentication setup. Time to actually *deploy* something small in Day 3!

---

### 🔗 Biteʒ 2 Blog Post:

* **Read the full detailed post on Dev.to:** [AWS Handshake](https://dev.to/mercyndonga/terra-bitez-2-aws-handshake-k3p/)

---
