# Securing Your VPC with Public and Private Subnets

## Overview
This project demonstrates how to set up a secure Virtual Private Cloud (VPC) with both public and private subnets in AWS. The setup includes an Internet Gateway, Network Address Translation (NAT) Gateway, security groups, and a bastion host for secure access.

## What You Will Learn
By completing this project, you will understand how to:
- Create and configure a Virtual Private Cloud (VPC)
- Set up public and private subnets
- Configure security groups and Network Access Control Lists (NACLs)
- Deploy a Bastion Host for secure SSH access
- Implement a NAT Gateway for internet access in private subnets
- Manage route tables for proper network communication

## Prerequisites
Before starting, ensure you have:
- A basic understanding of AWS EC2 and VPC concepts
- An active AWS account

## Step-by-Step Guide
### 1. Log in to AWS
Sign in to your AWS account using your credentials.

### 2. Create a VPC
- Navigate to **VPC** in the AWS Console.
- Click **Create VPC** and enter:
  - Name: `VPC-Project`
  - CIDR Block: `10.0.0.0/16`
- Click **Create VPC**.

### 3. Set Up an Internet Gateway
- Go to **Internet Gateways** and create a new gateway named `demo-gw`.
- Attach it to `VPC-Project`.

### 4. Create a Public Subnet
- Go to **Subnets** and create a new subnet:
  - Name: `Public-A`
  - CIDR Block: `10.0.20.0/24`
  - Availability Zone: `us-west-2a`
- Associate it with a route table containing a route to the Internet Gateway.

### 5. Create a Bastion Host
- Launch an EC2 instance in `Public-A`.
- Enable SSH (Port 22) access from your IP in the security group.
- Assign a public IP to the instance.

### 6. Create a Private Subnet
- Create a new subnet named `Private-A` with CIDR Block `10.0.10.0/24`.
- Associate it with a private route table (initially pointing to the Internet Gateway, but later updated to use a NAT Gateway).

### 7. Set Up Network ACLs
- Create a **Network ACL** named `Private-NACL`.
- Associate it with the `Private-A` subnet.
- Configure inbound/outbound rules to allow only necessary traffic.

### 8. Launch a Private EC2 Instance
- Create an EC2 instance in `Private-A`.
- Set its security group to allow SSH only from the Bastion Host.

### 9. Configure a NAT Gateway
- Deploy a **NAT Gateway** in `Public-A`.
- Allocate an Elastic IP for the NAT Gateway.
- Update the private route table to use the NAT Gateway for outbound internet traffic.

### 10. Connect to the Private Instance
- SSH into the Bastion Host.
- From the Bastion Host, connect to the private instance using SSH agent forwarding.

## Summary
This project helps you create a secure AWS VPC with properly configured public and private subnets. The Bastion Host ensures secure access to private instances, and the NAT Gateway allows outbound traffic while maintaining security. 

## Next Steps
- Implement additional security measures such as IAM roles and encryption.
- Automate this setup using Terraform or AWS CloudFormation.
- Monitor network activity using AWS CloudWatch and VPC Flow Logs.



