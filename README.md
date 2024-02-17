# AWS CloudFormation Template: VPC with Public and Private Subnets

This CloudFormation template creates a Virtual Private Cloud (VPC) with public and private subnets, along with EC2 instances in each subnet. The public subnet has an EC2 instance running Nginx, while the private subnet has an EC2 instance running Apache Tomcat.

## Templete Architecture
<img src="/Images/VPC_Archi.png">

## Template Overview

- **VPC**: Creates a VPC with a specified CIDR block, enabling DNS support and hostnames.

- **Subnets**: Creates public and private subnets with the specified CIDR blocks. The public subnet has an Internet Gateway attached and maps public IP addresses to instances launched within it.

- **Internet Gateway**: Attaches an Internet Gateway to the VPC to allow outbound internet access for instances in the public subnet.

- **Route Tables**: Creates separate route tables for the public and private subnets. The public route table has a route to the Internet Gateway, while the private route table has a route to a NAT Gateway for outbound internet access.

- **NAT Gateway**: Creates a NAT Gateway in the public subnet to allow instances in the private subnet to initiate outbound traffic to the internet.

- **Elastic IP**: Associates an Elastic IP address with the NAT Gateway.

- **Security Group**: Creates a security group allowing inbound traffic on ports 22 (SSH), 80 (HTTP), 8080, and 3306 (MySQL) from any IP address.

- **EC2 Instances**: Launches two EC2 instances, one in the public subnet running Nginx and another in the private subnet running Apache Tomcat. The Apache Tomcat instance is configured to start automatically using a user data script.

## Usage

1. **Deploy the Stack**: Use AWS CloudFormation to deploy this template in your AWS account.

2. **Access Nginx**: Once the stack is deployed, you can access the Nginx instance in the public subnet using its public IP address.

3. **Access Apache Tomcat**: You can access the Apache Tomcat instance in the private subnet through the Nginx instance or by connecting to the private IP address directly (if you have a VPN or Direct Connect set up).

4. **Cleanup**: Don't forget to delete the CloudFormation stack when you're done to avoid ongoing charges.

## Note

Make sure to replace the `ImageId` values with the appropriate AMI IDs for your region and instance types as needed.

