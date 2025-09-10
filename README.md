Task: Provision an AWS VPC with an EC2 Instance Using Terraform

Prerequisites
1. **AWS Account**: You need an active AWS account with access keys (Access Key ID and Secret Access Key).
2. **Terraform Installed**: Download and install Terraform from [terraform.io](https://www.terraform.io/downloads.html).
3. **AWS CLI (Optional)**: For configuring AWS credentials locally.
4. **Basic Knowledge**: Familiarity with AWS and basic command-line usage.

---

### Steps to Accomplish the Task

#### Step 1: Set Up Your Environment
1. Install Terraform:
   - Download the appropriate Terraform binary for your operating system from the official website.
   - Unzip and add Terraform to your system’s PATH (e.g., `/usr/local/bin` on Linux/Mac).
   - Verify installation: `terraform --version`.

2. Configure AWS Credentials:
   - Run `aws configure` (if using AWS CLI) to set your Access Key ID, Secret Access Key, region (e.g., `us-east-1`), and output format (e.g., `json`).
   - Alternatively, set environment variables:
     ```bash
     export AWS_ACCESS_KEY_ID="your-access-key"
     export AWS_SECRET_ACCESS_KEY="your-secret-key"
     export AWS_DEFAULT_REGION="us-east-1"
     ```

Step 2: Create a Terraform Configuration
1. Create a Project Directory:
   ```bash
   mkdir terraform-aws-example
   cd terraform-aws-example
   ```

2. Write Terraform Configuration Files:
   Create a file named `main.tf` with the following code to define the AWS provider, VPC, subnet, security group, and EC2 instance.

3. Create a Variables File (Optional):
   To make the configuration reusable, create a `variables.tf` file:
   ```hcl
  
4. Create a Key Pair:
   - In the AWS Management Console, navigate to EC2 > Key Pairs.
   - Create a key pair named `my-key-pair` and download the `.pem` file.
   - Update the `key_name` in `main.tf` or pass it as a variable.

Step 3: Initialize and Apply the Terraform Configuration
1. Initialize Terraform:
   Run the following command to download the AWS provider and set up the working directory:
   ```bash
   terraform init
   ```

2. Preview the Plan:
   Check what resources Terraform will create:
   ```bash
   terraform plan
   ```

3. Apply the Configuration:
   Deploy the infrastructure:
   ```bash
   terraform apply
   ```
   - Type `yes` when prompted to confirm.
   - Terraform will provision the VPC, subnet, internet gateway, route table, security group, and EC2 instance.
   - After completion, it will output the public IP of the EC2 instance.

Step 4: Verify the Infrastructure
1. Check AWS Console:
   - Log in to the AWS Management Console.
   - Navigate to EC2 > Instances to confirm the instance is running.
   - Verify the VPC, subnet, and security group under VPC > Your VPCs and EC2 > Security Groups.

2. SSH into the EC2 Instance:
   Use the public IP output by Terraform to connect:
   ```bash
   ssh -i my-key-pair.pem ec2-user@<public-ip>
   ```

Step 5: Manage and Clean Up
1. **Update Infrastructure**:
   - Modify `main.tf` (e.g., change the instance type to `t3.micro`).
   - Run `terraform plan` to preview changes and `terraform apply` to update.

2. Destroy Infrastructure:
   When done, clean up to avoid AWS charges:
   ```bash
   terraform destroy
   ```
   - Type `yes` to confirm.
