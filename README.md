# AWS High-Availability Web Application Project

This project demonstrates the creation of a highly available and secure web application using AWS services. The architecture includes an Amazon RDS MySQL database for secure data storage, an Application Load Balancer (ALB) for high availability, and an Auto Scaling group to dynamically scale EC2 instances based on demand.

## Key Features
- **Secure Database Hosting**: Amazon RDS MySQL database with encrypted credentials stored in AWS Secrets Manager.
- **High Availability**: Application Load Balancer (ALB) to distribute traffic across multiple EC2 instances.
- **Auto Scaling**: Auto Scaling group to automatically adjust the number of EC2 instances based on CPU utilization.
- **Secure Connectivity**: Properly configured security groups to ensure secure communication between components.


## Step 1: Creating an Amazon RDS MySQL Database

### Objective
Set up a secure and highly available MySQL database using Amazon RDS.

### Steps

1. **Launch an Amazon RDS MySQL Database**:
   - Navigate to the RDS service in the AWS Management Console.
   - Click "Create database" and configure the following:
     - **Database creation method**: Standard Create.
     - **Engine type**: MySQL.
   - Configure additional settings such as instance size, storage, and connectivity.



![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/3.png)

RDS MySQL Database Creation

$~$

2. **Store Database Credentials in AWS Secrets Manager**:
   - Create a new secret in AWS Secrets Manager.
   - Select **"Credentials for RDS database"** as the secret type.
   - Link the secret to the RDS MySQL instance and provide the database username and password.


![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/4.png)

Configured Secret in AWS Secrets Manager 

## Step 2: Creating an Application Load Balancer (ALB)

### Objective
Set up an Application Load Balancer to distribute incoming traffic across multiple EC2 instances.

### Steps
1. **Create the Application Load Balancer**:
   - Open the EC2 Dashboard → Load Balancers.
   - Click "Create Load Balancer" and select "Application Load Balancer."
   - Configure the following:
     - **Name**: `countries-alb`
     - **Scheme**: Internet-facing
     - **IP address type**: IPv4
     - **Availability Zones**: Select at least two public subnets.
   - Configure security groups, listeners, and target groups.

2. **Verify ALB Creation**:
   - Confirm the successful creation of the ALB and ensure it is associated with the correct subnets and security groups.

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/5.png)

Created Application load balancer

$~$

## Step 3: Setting Up the Application Server in an Auto Scaling Group

### Objective
Deploy the application server in an Auto Scaling group to ensure scalability and high availability.

### Steps
1. **Create an Auto Scaling Group (ASG)**:
   - Use a pre-configured launch template (`Project-LT`).
   - Name the ASG `countries-asg`.
   - Attach the target group from the Application Load Balancer (ALB).

2. **Configure Network and Subnets**:
   - Select the same VPC and public subnets used for the ALB.
   - Ensure instances are launched in at least two Availability Zones.

3. **Set Scaling Policies**:
   - Use a **Target Tracking Policy** based on CPU utilization (50%).
   - Configure the ASG with:
     - **Desired capacity**: 2
     - **Minimum capacity**: 1
     - **Maximum capacity**: 5

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/6.png)

Launch Template details

$~$

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/7.png)

Autoscaling group details

$~$

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/ALB%20details.png)

Target group details

$~$

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/instances%20details.png)

Launched instance details

$~$

## Step 4: Connecting to the RDS MySQL Database

### Objective
Ensure secure connectivity between the application servers and the RDS MySQL database.

### Steps
1. **Modify Security Group Rules**:
   - Update the inbound rules of the database security group to allow traffic from the EC2 instances.

2. **Verify Connectivity**:
   - Use tools like `telnet` or `MySQL client` to confirm connectivity to the RDS MySQL database.

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/DB%20SG.png)

Modifying inbound rule under the Database Security group 

$~$

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/8.png)

Checking open ports on the EC2 instance

$~$

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/9.png)

Connecting to RDS DB using DB endpoint

$~$

## Conclusion
This project demonstrates the implementation of a highly available and secure web application on AWS. By leveraging services like Amazon RDS, Application Load Balancer, and Auto Scaling, the architecture ensures scalability, reliability, and security. The use of AWS Secrets Manager for credential management and proper security group configurations further enhances the security posture of the application.

