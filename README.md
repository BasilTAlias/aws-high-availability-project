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
   - Name: `countries-alb`
   - Scheme: Internet-facing
   - IP address type: IPv4
   - Availability Zones: Select at least 2 public subnets.
5. Configure security groups, listeners, and target groups.

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/5.png)

Created application load balancer

$~$

# Step 3: Setting Up the Application Server in an Auto Scaling Group

1. Create Auto Scaling Group (ASG):

- Use the Project-LT launch template.
- Name the ASG countires-asg.
- Attach the target group from the Application Load Balancer (ALB).
  
2. Configure Network and Subnets:
   
- Select the same VPC and public subnets used for the ALB.
- Ensure instances are launched in at least two Availability Zones.
  
3. Scaling Policies:

- Use Target tracking policy based on CPU utilization (50%).
- Set Desired capacity: 2, Min capacity: 1, Max capacity: 5

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/6.png)

Template details

$~$

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/7.png)

Autoscaling group details

$~$

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/ALB%20details.png)

Target group details

$~$

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/instances%20details.png)

launched instance details

$~$

# Step 4: Connecting to RDS MySQL database

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/DB%20SG.png)

Modifying inbound rule under the Database Security group 

$~$

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/8.png)

checking open ports under the EC2 instance

$~$

![Alt text of the image](https://github.com/BasilTAlias/aws-high-availability-project/blob/main/images/9.png)

Connecting to RDS DB using DB endpoint

$~$
