## Host a Static Website on AWS
This project demonstrates the deployment of a static HTML web application on AWS, utilizing various AWS resources and services to ensure a secure, scalable, and fault-tolerant setup. The infrastructure is managed using a combination of AWS VPC, EC2, and other services. Below is a detailed guide to replicate this setup.

## Architecture Overview:

  -VPC with Public and Private Subnets: Distributed across two Availability Zones for high availability.
  
  -Internet Gateway: Enables internet access for instances in public subnets.
  
  -Security Groups: Acts as a virtual firewall to control inbound and outbound traffic.
  
  -EC2 Instances: Hosted in private subnets to enhance security.
  -NAT Gateway: Allows instances in private subnets to access the internet.
  
  -Application Load Balancer: Distributes incoming web traffic across multiple EC2 instances.
  
  -Auto Scaling Group: Automatically manages the number of EC2 instances based on traffic demands.
  
  -Certificate Manager: Secures application communications.
  
  -Simple Notification Service (SNS): Sends notifications regarding activities within the Auto Scaling Group.
  
  -Route 53: Manages DNS and domain registration.

## Step 1: Configure VPC and Subnets
Create a VPC with CIDR block (e.g., 10.0.0.0/16).
Create public and private subnets in two different Availability Zones.
Allocate IP ranges for subnets (e.g., 10.0.1.0/24 for public and 10.0.2.0/24 for private subnets).

## Step 2: Set Up Internet Gateway and NAT Gateway
Attach an Internet Gateway to the VPC.
Create a NAT Gateway in one of the public subnets.
Update route tables:
Public Subnet Route Table: Route all traffic (0.0.0.0/0) to the Internet Gateway.
Private Subnet Route Table: Route all traffic (0.0.0.0/0) to the NAT Gateway.

## Step 3: Establish Security Groups
Create Security Groups for the following:
EC2 instances (allow HTTP and SSH access).
Load Balancer (allow HTTP and HTTPS access).
NAT Gateway (allow HTTP, HTTPS, and other necessary traffic).

## Step 4: Launch EC2 Instances
Launch EC2 instances in private subnets.
Ensure instances have IAM roles allowing necessary permissions.
Use the provided script for user data to set up Apache and deploy the web app.

## Step 5: Configure Application Load Balancer
Create an Application Load Balancer in public subnets.
Set up listeners for HTTP (port 80) and HTTPS (port 443).
Create a target group and register EC2 instances.

## Step 6: Implement Auto Scaling Group
Create an Auto Scaling Group associated with the target group.
Define scaling policies based on CPU utilization or other metrics.
Ensure the Auto Scaling Group spans across both Availability Zones.

## Step 7: Set Up DNS with Route 53
Register a domain name or use an existing one.
Create a hosted zone in Route 53.
Create DNS records to route traffic to the Application Load Balancer.
