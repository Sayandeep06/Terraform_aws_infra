Terraform AWS Project Documentation
===================================

Overview
--------

This Terraform script is designed to create an AWS infrastructure for a simple web application. The infrastructure includes a Virtual Private Cloud (VPC), two subnets in different availability zones, an Internet Gateway, a Route Table, a Security Group, an S3 bucket, two EC2 instances, and an Application Load Balancer (ALB).

Prerequisites
-------------

1.  AWS CLI configured with the necessary credentials.
2.  Terraform installed on your machine.

Project Structure
-----------------

-   `main.tf`: Defines the main infrastructure components.
-   `variables.tf`: Defines input variables used in the script.
-   `userdata.sh`: User data script for the first EC2 instance.
-   `userdata1.sh`: User data script for the second EC2 instance.

Configuration
-------------

### VPC

-   Resource: `aws_vpc.myvpc`
    -   Creates a Virtual Private Cloud (VPC) with the specified CIDR block.

### Subnets

-   Resources: `aws_subnet.subnet1` and `aws_subnet.subnet2`
    -   Creates two subnets in different availability zones within the VPC.

### Internet Gateway

-   Resource: `aws_internet_gateway.igw`
    -   Attaches an Internet Gateway to the VPC for internet access.

### Route Table

-   Resources: `aws_route_table.RT`, `aws_route_table_association.rta1`, and `aws_route_table_association.rta2`
    -   Creates a route table and associates it with the subnets for routing internet-bound traffic through the Internet Gateway.

### Security Group

-   Resource: `aws_security_group.websg`
    -   Creates a security group to control inbound and outbound traffic for the EC2 instances.
    -   Allows inbound traffic on ports 80 (HTTP) and 22 (SSH).
    -   Allows all outbound traffic.

### S3 Bucket

-   Resource: `aws_s3_bucket.example`
    -   Creates an S3 bucket for storing application data.

### EC2 Instances

-   Resources: `aws_instance.webserver1` and `aws_instance.webserver2`
    -   Creates two EC2 instances with specified AMI, instance type, security group, and subnet.
    -   Attaches user data scripts for additional configuration.

### Application Load Balancer (ALB)

-   Resources: `aws_lb.myalb`, `aws_lb_listener.listener`, `aws_lb_target_group.tg`, `aws_lb_target_group_attachment.attach1`, and `aws_lb_target_group_attachment.attach2`
    -   Creates an Application Load Balancer (ALB) with a listener forwarding traffic to the target group.
    -   Associates the ALB with the security group and subnets.
    -   Configures health checks for the target group.
    -   Attaches EC2 instances to the target group.

### Outputs

-   Output: `loadbalancerdns`
    -   Displays the DNS name of the created ALB for accessing the web application.

Usage
-----

1.  Ran `terraform init` to initialize the working directory.
2.  Ran `terraform plan` to see what the changes and infra will be made.
3.  Ran `terraform apply` to create the AWS infrastructure.
4.  Confirmed the changes by typing `yes` when prompted.
5.  After completion, the DNS name of the ALB is displayed in the output.

Clean Up
--------

To destroy the created infrastructure, run:



`terraform destroy`

Confirm the destruction by typing `yes` when prompted.

Note
----

-   Ensure that sensitive information such as AWS credentials and private keys are handled securely.
-   Review the AWS regions, availability zones, and AMI IDs based on your requirements.

References
----------

-   [Terraform AWS Provider Documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
