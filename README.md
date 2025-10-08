# VPC-Peering[Uploading README (vpc6).md…]()
<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** Esther Moaweni  
**Email:** moaweniesther@gmail.com

---

## VPC Peering

![Image](http://learn.nextwork.org/daring_silver_jolly_badger/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a virtual private cloud service that provides an isolated network environment in AWS to deploy resources like EC2 instances.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create and configure two VPCs, establish a VPC peering connection and test communication between EC2 instances to validate network connectivity and learn inter-VPC networking.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how critical it was to update both security groups and route tables in each VPC to allow ICMP traffic and direct traffic properly for a successful VPC peering connection.

### This project took me...

This project took me a few hours to complete, as setting up multiple VPCs, configuring the peering connection, updating route tables and security groups and troubleshooting connectivity with ping tests required careful attention to detail.

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I will create two VPCs from scratch using the visual VPC resource map because it provides a clear, graphical representation of the network components, helping me design and configure the VPCs, subnets and routing accurately for the peering setup.

### Step 2 - Create a Peering Connection

In this step, I will create a VPC peering connection because I want to enable private communication between two VPCs without using the public internet.

### Step 3 - Update Route Tables

I will set up a way for traffic coming from VPC 1 to get to VPC 2 and vice versa because I want to enable seamless communication between resources in both VPCs by configuring route tables to direct traffic through the VPC peering connection.

### Step 4 - Launch EC2 Instances

In this step, I will launch an EC2 instance in each VPC, so I can use them to test my VPC peering connection.

---

## Multi-VPC Architecture

I started my project by launching 2 VPCs with unique IPV4 CIDR block, 1 public subnet for each VPC no private subnet.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16 They have to be unique to avoid IP conflict and connectivity issues.

### I also launched 2 EC2 instances

I didn't set up key pairs for these EC2 instances as I plan to use SSH through EC2 Instance Connect to securely access the instances without managing private keys.

![Image](http://learn.nextwork.org/daring_silver_jolly_badger/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is a networking connection between two VPCs that enables direct communication between their resources, such as EC2 instances, using private IP addresses across the AWS network.

VPCs would use peering connections to enable secure and direct communication between resources in different VPCs, such as EC2 instances, allowing data sharing and application integration across isolated network environments in AWS.

The difference between a Requester and an Accepter in a peering connection is that the Requester is the VPC that initiates the peering request, while the Accepter is the VPC that accepts the request to establish the connection.

![Image](http://learn.nextwork.org/daring_silver_jolly_badger/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs' route tables need to be updated because I must add routes to direct traffic between the VPCs through the peering connection, ensuring resources in each VPC can communicate using their respective CIDR blocks.

My VPCs' new routes have a destination of 10.2.0.0/16 and 10.1.0.0/16  for VPC 1 and VPC 2 repectively. The routes' target was Peering Connection.

![Image](http://learn.nextwork.org/daring_silver_jolly_badger/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will use EC2 Instance Connect to connect to my first EC2 instance because I want to test and troubleshoot any connection errors that may arise.

### Step 6 - Connect to EC2 Instance 1

I will use EC2 Instance Connect to connect to instance 1 because I want to test the connection and troubleshoot any errors that may arise.

### Step 7 - Test VPC Peering

In this step, I will get Instance 1 to send test messages to Instance 2 because I want to test the connectivity and troubleshoot any connection errors until Instance 2 can successfully send messages back.

---

## Troubleshooting Instance Connect

I used EC2 Instance Connect to securely connect to my EC2 instance via a browser-based SSH client from the AWS Management Console, allowing me to test and troubleshoot connectivity within my VPC peering setup without needing a local SSH client or key pair.

I was stopped from using EC2 Instance Connect as my EC2 instance did not have a public ipv4 address

![Image](http://learn.nextwork.org/daring_silver_jolly_badger/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses. Elastic IP addresses are are static, public IPv4 addresses allocated to your AWS account that can be associated with an EC2 instance to enable consistent internet access and connectivity for tools like EC2 Instance Connect.

Associating an Elastic IP address resolved the error because it provided my EC2 instance with a static public IPv4 address, enabling EC2 Instance Connect to establish a browser-based SSH connection from the AWS Management Console.

![Image](http://learn.nextwork.org/daring_silver_jolly_badger/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran the command ping 10.1.0.0/16, targeting the private IP address of the EC2 instance in the peered VPC to verify connectivity between the two VPCs.

A successful ping test would validate my VPC peering connection because it confirms that the EC2 instances in the peered VPCs can communicate over their private IP addresses, indicating that the peering connection, route tables and security groups are correctly configured.

I had to update my second EC2 instance's security group because it did not allow ICMP traffic. I added a new rule that permits all ICMP - IPv4 traffic from the IP address EC2 instance to enable successful ping tests between the instances.

![Image](http://learn.nextwork.org/daring_silver_jolly_badger/uploads/aws-networks-peering_7a29d352)

---

---
