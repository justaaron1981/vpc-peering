<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** Aaron  
**Email:** justaaron1981@yahoo.com

---

## VPC Peering

![Image](http://learn.nextwork.org/gleeful_red_proud_durian/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is foundation networking service that let's us create our own networks control traffic flow, security and, orginise our public and private resources into public/private subnets.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to set up a multi VPC architecture (I set up two VPCs), create a peering connection between them and update security group rules to run a succeful connectivity test to validate my VPC peering set up. 

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was to need a public IPv4 address for EC2 instance connect to worko

### This project took me...

This project took me two hours

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I will be using the VPC resource map/launch wizard to create two VPCs and their componets in just minutes.

### Step 2 - Create a Peering Connection

In this step, I will be setting up a VPC peering connection which is a component designed to directly connect to directly connect two VPCs together.

### Step 3 - Update Route Tables

In this step, I will edit the routetable for VPC 1 and VPC 2 so that trafic can be directed to the peering conncetion set-up

### Step 4 - Launch EC2 Instances

In this step I will launch an EC2 instances inside of a VPCs ( VPC1 and VPC2), so that I can directly connect with my EC2 instance later and test my VPC peer connection 

---

## Multi-VPC Architecture

I started my project by launching two VPCs thy have unique CIDR blocks and they each have one public subnet.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16 respectivly  They have to be unique because once I setup VPC peering connection (between two VPCs). Route tables need unique addresses for correct routing accross VPCs

### I also launched 2 EC2 instances

I didn't set up key pairs for these EC2 instances as because I using EC2 instance connect to directly connect with my EC2 instance later in this project, which handles key pair management and creation for me

![Image](http://learn.nextwork.org/gleeful_red_proud_durian/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is a private, direct network connection between two Virtual Private Clouds (VPCs) that allows resources in one VPC to communicate with resources in the other VPC using private IP addresses as if they were on the same network. 

VPCs would use peering connections to route traffic privately between two Virtual Private Clouds (VPCs)

The difference between a Requester and an Accepter in a peering connection is the Requester is the party that initiates the connection by sending the request, while the Accepter is the other party that must explicitly accept the request for the connection to be established and activated.  

![Image](http://learn.nextwork.org/gleeful_red_proud_durian/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs' route tables need to be updated because trafic between VPCs still need directions from the route table in order to get the the other VPC. The default route table dooesn't have a route using the peering connection yet - this needs to be set up so that resources can directed to the peering connection when trying to reach the other VPC 

My VPCs' new routes have a destination of the other VPC's CIDR block The routes' target was peer connection

![Image](http://learn.nextwork.org/gleeful_red_proud_durian/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will be using EC2 instance connect to connect directly to my first EC2 instance. I need to do this because i need to use my EC2 instance for connectivity test (to validate my VPC peering set up) later in this project.

### Step 6 - Connect to EC2 Instance 1

In this step, I will reattempting my VPC connection to instance -Nextwork VPC 2 and resolving another error preventing me from using  EC2 instance connect to directly connect with an instance.

### Step 7 - Test VPC Peering

In this step, I will use the instance in nextwork VPC 2. to attempt a direct connection with - nextwork VPC-1 so I can validate that my peering connection is set up properly because...

---

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to directly connect with instance - Nextwork VPC 2. Just by using AWS management console.

I was stopped from using EC2 Instance Connect as my instance did not have an IPV4 address. in order for EC2 instance to work. The EC2 instance must have a public IPv4 address and be in a public subnet

![Image](http://learn.nextwork.org/gleeful_red_proud_durian/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses. Elastic IP addresses are static IPv4 address that we can request for our AWS account, and then delegate to spacific resources that will use this this IP address.

Associating an Elastic IP address resolved the error because it gives our EC2 instance a public IP address. fulfillling all the requirements for instance connect to work

![Image](http://learn.nextwork.org/gleeful_red_proud_durian/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran the command ping 10.1.xxx.xx IPv4 address of the other EC2 instance in VPC 1

successful ping test would validate my VPC peering connection because this ping test would not get any replies from the other EC2 instance if the peering connection did not succesfully connect my two VPCs getting ping replies = peering connection was set up properly

I had to update my second EC2 instance's security group because it was not letting in IMCP traffic -which is the traffic type of a ping message I added a new rule that allows ICMP traffic coming in from any resource in VPC 2

![Image](http://learn.nextwork.org/gleeful_red_proud_durian/uploads/aws-networks-peering_7a29d352)

---

---
