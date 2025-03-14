# Deploy a High-Availability Web App Using CloudFormation

# Overview
This project involves deploying a high-availability web application using AWS CloudFormation. The infrastructure setup includes network resources, EC2 instances, a Load Balancer, S3 buckets, security groups, and auto-scaling for the web servers. The goal is to create a scalable solution that serves static content, provides redundancy, and ensures high availability.

# Infrastructure Diagram

![Alt Text](devops-IaC-diagram.JPG)

An infrastructure diagram has been created to illustrate the AWS resources involved in this project. The diagram includes the following resources:

# Network Resources:

# VPC
Subnets (two public and two private subnets for high availability)
Internet Gateway
NAT Gateways
EC2 Resources:
![Screenshot 2025-03-12 232217](https://github.com/user-attachments/assets/e205fefd-d2e5-44fd-91fe-b5be7cbe014d)
![Screenshot 2025-03-12 232232](https://github.com/user-attachments/assets/d0dec738-3e7a-4833-bfbd-e82765314075)
![Screenshot 2025-03-12 232245](https://github.com/user-attachments/assets/31493c22-bdea-44ef-9a97-f268e06f6e0a)
![Screenshot 2025-03-12 232258](https://github.com/user-attachments/assets/34975983-7169-476e-a47e-dfb52e586a12)
![Screenshot 2025-03-12 232311](https://github.com/user-attachments/assets/29bc6541-964a-4e98-8fef-d249c8272673)
![Screenshot 2025-03-12 232324](https://github.com/user-attachments/assets/214c0b32-5f77-40cd-9c7a-5e26635f3284)

# Auto Scaling Group with EC2 instances

![Screenshot 2025-03-12 232507](https://github.com/user-attachments/assets/37d649b9-a03d-4122-89b0-436ab9dbe454)
![Screenshot 2025-03-12 233434](https://github.com/user-attachments/assets/1cd65ffd-cf4b-455c-a547-34f156407f35)


# S3 Bucket for storing static content
The diagram shows the relationships between these resources (e.g., the Load Balancer connects to EC2 instances, the EC2 instances access the S3 bucket for static content).
![Screenshot 2025-03-12 233340](https://github.com/user-attachments/assets/19b565e3-d870-44b2-b2c5-09dc6ee309fd)
![Screenshot 2025-03-12 233355](https://github.com/user-attachments/assets/8e97db73-e38e-43de-a01b-63cead80ce68)
![Screenshot 2025-03-12 233407](https://github.com/user-attachments/assets/6dca2237-07d2-4e0a-a716-0ee5e4785a7a)


# Network and Servers Configuration
VPC & Subnets:
The infrastructure is deployed within a VPC that includes four subnets: two public and two private for high availability.
![Screenshot 2025-03-12 232232](https://github.com/user-attachments/assets/af021c67-b397-4de3-aff3-1d074ffb75c7)
![Screenshot 2025-03-12 232245](https://github.com/user-attachments/assets/2906e1ef-9337-4a00-b137-d2cf7ac3bd07)


# Internet and NAT Gateways:

An Internet Gateway is attached to the VPC for public internet access.
NAT Gateways are used to provide internet access to private subnets.
![Screenshot 2025-03-12 232232](https://github.com/user-attachments/assets/710535b7-0051-43cd-b590-931f7aaff99a)
![Screenshot 2025-03-12 232245](https://github.com/user-attachments/assets/7fa484b6-89f5-4b41-a6ef-fa8f347ae799)
![Screenshot 2025-03-12 232258](https://github.com/user-attachments/assets/876b4ef1-4f4a-4ee3-b737-5ab3a481f371)


# The Auto Scaling Group uses Launch Templates to deploy EC2 instances.
t2.micro instances with Ubuntu 22 are used for the application servers.
Two instances are deployed in each of the private subnets.
Load Balancer:
The Application Load Balancer (ALB) is exposed to the internet on port 80 and routes traffic to the EC2 instances.
![Screenshot 2025-03-12 233419](https://github.com/user-attachments/assets/338afdda-1d8a-41c8-a3cd-61d3d82e6e44)
![Screenshot 2025-03-12 233434](https://github.com/user-attachments/assets/fbeb05f9-5fab-4783-b738-fea3ee4ab43d)
![Screenshot 2025-03-12 233444](https://github.com/user-attachments/assets/24e7a083-6a34-4e43-971a-91372a43dc98)


# S3 Bucket:
A public-read S3 bucket is used for storing static content. The EC2 instances have an IAM role allowing read and write permissions to the bucket.
![Screenshot 2025-03-12 233355](https://github.com/user-attachments/assets/8f1ca37e-4e6a-4bc5-9e1e-72d60d26c385)

# CloudFormation Templates
Networking Stack-
The networking stack contains resources to set up the VPC, subnets, internet gateway, and NAT gateways.

# Outputs:

VPC ID
Subnet IDs
These outputs are imported into the application stack to set the correct VPC and subnets for the resources.
![Screenshot 2025-03-12 232340](https://github.com/user-attachments/assets/040059d0-6dea-4dcd-aa54-f0ce67076e29)
![Screenshot 2025-03-12 232353](https://github.com/user-attachments/assets/c813863f-e8ba-45b7-a93b-31be10c90c7e)



Application Stack-
The application stack contains resources specific to the application, including:

EC2 instances
Application Load Balancer
Auto Scaling Group
S3 Bucket
Security Groups-
The stack uses outputs from the networking stack to configure the correct VPC and subnets.

# Output:

Public URL of Load Balancer:
The Load Balancer DNS name is output with http:// added for convenience, so the public URL is easily accessible.
Security Groups
Security groups are configured following the least privilege principle.
![Screenshot 2025-03-12 233444](https://github.com/user-attachments/assets/5d40c048-9b06-43f4-8146-f4ad1b7ac5a3)


# EC2 Instances:

Allow inbound traffic on port 80 for HTTP communication with the Load Balancer.
Allow unrestricted outbound access for updates and internet access.
Load Balancer:

Allow inbound traffic from any source (0.0.0.0/0) on port 80.
Scripts for Automation
Automation scripts are provided to create and destroy the infrastructure without UI interaction. The scripts can be written in Bash or Python (Boto3), and they use the CloudFormation CLI to deploy the templates.

# Deployment
If the infrastructure is set up correctly, you should see the following message on the webpage:
nginx
It works! Udagram, Udacity

# Parameters
CIDR blocks for VPC, subnet configurations.
Resources-
EC2 Instances: Should meet the minimum requirements (t2.micro or better).
Load Balancer: Must be configured with a Target Group, Health Check, and Listener.
![Screenshot 2025-03-12 232138](https://github.com/user-attachments/assets/04937fb7-e89a-4a39-bcf2-7c8c7abf26e6)
![Screenshot 2025-03-12 232435](https://github.com/user-attachments/assets/308222f7-9dd4-4fed-9141-d81d209b90dd)
![Screenshot 2025-03-12 232217](https://github.com/user-attachments/assets/d9e77691-2847-4547-be64-e8c9ad0b6f06)


# Conclusion
This README outlines the necessary steps for deploying a high-availability web application using CloudFormation. The infrastructure includes networking resources, EC2 instances in an Auto Scaling group, an Application Load Balancer, and an S3 bucket for static content. CloudFormation templates, security group configurations, and automation scripts are provided to facilitate the creation and deletion of the entire infrastructure.

## Spin up instructions
1. change directory (cd) to starter root
2. execute command- ./create.sh networkinfra network.yml network-paramters.json
3. when networkinfra stack is created, execute command- ./create.sh udagraminfra udagram.yml udagram-parameters.json to create second stack.
 ![Screenshot 2025-03-12 232044](https://github.com/user-attachments/assets/ef24c913-3220-464e-8a4d-c73d3f06ab83)
   

## Tear down instructions
1. execute command- aws cloudformation delete-stack --stack-name udagraminfra
2. When network stack is deleted, execute command- aws cloudformation delete-stack --stack-name networkinfra
![Screenshot 2025-03-12 232126](https://github.com/user-attachments/assets/abe4bfc1-4435-42ed-858d-6191b93ea4bc)


## URL verifying servers are running properly

![Screenshot 2025-03-02 124718](https://github.com/user-attachments/assets/24bb5ad4-0855-43eb-b69c-d4ed31413b1d)

---

![Screenshot 2025-03-02 124747](https://github.com/user-attachments/assets/5992a2eb-1904-47a6-926e-2956102605ed)
