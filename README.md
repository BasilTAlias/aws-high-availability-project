# aws-high-availability-project
A project to create a highly available and secure web application using AWS services

## Features

- Secure hosting of MySQL database using Amazon RDS.
- High availability with Application Load Balancer.
- Auto Scaling group for scaling based on demand.


# Step 1: Creating an Amazon RDS MySQL database

## Steps

1.  Launch an Amazon RDS MySQL Database

- Sign in to the AWS Management Console and navigate to the RDS service.
- Click "Create database" and select the following options:
- Database creation method: Standard Create.
- Engine type: MySQL.

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/3.png)

created RDS MySQL database

$~$

## Create a new secret:

- Secret type: Credentials for RDS database.
- Database: Select the RDS MySQL instance.
- Enter the username and password for the database.


![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/4.png)

configured the Secret 

# Step 2: Creating an Application Load Balancer

## Objective
Set up an Application Load Balancer (ALB) to distribute incoming traffic across multiple EC2 instances.

## Steps
1. Open the EC2 Dashboard → Load Balancers.
2. Click "Create Load Balancer."
3. Select "Application Load Balancer."
4. Configure the following:
   - Name: `MyApp-ALB`
   - Scheme: Internet-facing
   - IP address type: IPv4
   - Availability Zones: Select at least 2 public subnets.
5. Configure security groups, listeners, and target groups.


  
