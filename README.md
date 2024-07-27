# AWS-Project-1
My First AWS PROJECT To Demonstraste Apps In Private Subnet

![images (2)](https://github.com/user-attachments/assets/3d4f62ba-bdb5-421d-9e0d-78f1a3950803)


AWS Project
VPC with Public-Private Subnet in Production

About:

This project demonstrates how to create a VPC that you can use for servers in a production environment.
-To improve resiliency, you deploy the servers in two Availability Zones by using an Auto Scaling group and an Application Load Balancer.
-For additional security, you deploy the servers in private subnets.
-The servers receive requests through the Load Balancer.
-The servers can connect to the internet by using NAT gateway.
-To improve resiliency, you deploy the NAT gateway in both Availability Zones.

Overview:

-The VPC has public subnets and private subnets in two Availability Zones.
-Each public subnet contains a NAT gateway and a load balancer node.
-The servers run in the private subnets, are launched and terminated by using an Auto Scaling group, and receive traffic from the load balancer.
-The servers can connect to the internet by using the NAT gateway.

Before we start:

-Auto Scaling Group: Automatically adjusts the number of EC2 instances based on traffic demand to maintain performance and minimize costs.
-Load Balancer: A Load Balancer is a service that distributes incoming network traffic across multiple servers to ensure no single server becomes overwhelmed.
-Target Group
-Bastion Host or Jump Server

Let's Start the Project Implementation:
-Go to the search bar, type VPC, and click on that.
-You will find an option that says "Create VPC."
-Select VPC and more options.
-Select a name.
-Go with the default in CIDR.
-No IPv6.
-Number of availability zones: 2.
-Number of public subnets: 2.
-Number of private subnets: 2.
-NAT gateway: 1 per AZ.
-VPC endpoint: none.
-Create VPC.

So now we need an EC2 instance where our application is actually deployed, and also we need an Auto Scaling Group.

Now go to the search bar, search for EC2.
-Go to the Auto Scaling Group section.
-Create Auto Scaling Group.
Note: Auto Scaling Groups in AWS cannot be created directly.

you can use launch template.
-Create launch template.
-Give name and description.
-Select OS: Ubuntu.
-Instance type: t2.micro.
-Key pair.
-Network settings go with default - Create a new security group.
-Provide a name and description.
-Select your custom VPC.
-Inbound security group rules - Add security group rules.
-SSH source type: Anywhere.
-Add one more inbound rule for custom TCP 8000 port, accessible from anywhere.
-Create launch template.
-Go back to your auto scaling group.
-Provide a name.
-Select your template (restart).
-Click Next button.
-Select VPC again.
-Now select AZs so our instances will be in private subnets: Select Private1 and Private2 both.
-Click on Next.
-Go without load balancer.
-We will create load balancer in Public subnet later.
-Click on Next.
Desired capacity: 2.
Minimum: 1.
Maximum: 4.
-Scaling policies: NONE.
-Next - Next - Next - Next - Create auto scaling group.
Note: Now Auto Scaling Group has created instances. Now before going to create load balancer, you have to install application inside the servers.
