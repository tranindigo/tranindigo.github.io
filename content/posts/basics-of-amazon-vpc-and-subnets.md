---
title: "Basics of Amazon VPC and Subnets"
date: "2020-07-18"
categories: 
  - "aws"
tags: 
  - "access-contro-list"
  - "devops"
  - "nat-gateway"
  - "route-table"
  - "subnet"
  - "vpc"
---

Amazon Virtual Private Cloud (VPC) is a private data center within the AWS infrastructure. You are able to decide the range of network IPv4 address range when you create the VPC. There is no way to change your VPC's network block after it has been created.

A VPC consists of many components. A few that will be highlighted in this article are: subnets, Internet Gateway, NAT Gateway, Route Table, and Network Access List.

## Subnets

Subnets divide your VPC into discernible blocks of interdependent networks, which allow your VPC traffic to travel a shorter distance without passing through unnecessary routers to reach its destination.

Imagine you're sending mail to your friend who lives in a neighboring city. For the letter to reach your friend, it should be delivered from your post office to the post office in your friend's city, and then to your friend. If the letter if sent to a post office that is hundreds of miles away, your friend's letter could take a lot longer to arrive.

Similarly, when a network receives data packets from another network, it will sort and route those packets so that they do not take an inefficient route to their destination. Subnetting, the segmentation of a network address space, improves address allocation efficiency.

## Internet Gateway (IGW)

The Internet Gateway allows instances with public IPs to access the internet, and also allows resources within the VPC to access the internet. In order for this to happen a route table entry needs to allow a subnet to access the IGW.

## NAT Gateway

A NAT Gateway allows resources in a private subnet to access the internet. However, it does not allow the reverse unless you explicitly allow it.

## Route Table

A route table contains routes that determine where network traffic from your subnet or gateway is directed. It basically tells network packets which way they need to go to get to their destination. A subnet can only be associated with one route table at a time, but you may associate multiple subnets with the same subnet route table.

Imagine a network packet that arrives from the Internet to your VPC. To reach its destination, it must first go through a routes table, which will tell it where to go based on its request information. For instance, it might go heading toward a subnet within your VPC that will process the network packet.

## Network Access List

AWS also has a network access control list (ACL) that acts as a firewall that controls which traffic can come in and out of your subnets. ACLs can control both inbound and outbound traffic.

When you create a VPC, the default ACL allows all inbound and outbound rules. You can attach an ACL to one or more subnets in your VPC.
