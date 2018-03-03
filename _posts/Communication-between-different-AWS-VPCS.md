title: Ansible module to create AWS EndPoint Service
author: ChenPan
tags:
  - Deploy
categories: []
date: 2018-02-12 16:52:00
---
#### How to enable connection between different VPCs
1. Public IP
   <br>It is easy; But the speed will dependes on public net; also 
2. VPC Peering; 
  <br> After peering, two VPC share a same subnet. But it has a number limition.[(Detail)](https://docs.aws.amazon.com/AmazonVPC/latest/PeeringGuide/vpc-peering-basics.html#vpc-peering-limitations)
3. EndPoint Interface 
<br>High speed and safty.  But it is charged.


Method  |  Speed | Safety | Number limitation | Cross Region |  Price 
---------- | ---------- | ---------------- |  ---------   |  -----------------  |  -------------------
VPC Peering   | High | High | [(50/84)](https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Appendix_Limits.html#vpc-limits-peering) | US East (N. Virginia), US West (Oregon), EU (Ireland), and US East (Ohio).| Free
EndPoint  | Good    |   Good  |  No limit  |  Impossible |  High (in proportion to number of HUE VPCs) 
Public IP |  Low (possible to fix by route table)  |  Low | No limit | Possible | Free if OCR VPC not shutdown

** **
#### Ansible module of endPoint Service
In our project, we use endPoint to establish connection between two different VPCs. 
However endPoint interface is a new technique borned around 11/2017, so ansible don't have related module about endPoint interface and endPoint Service. The ec2_vpc_endpoint module(Ansible version 2.4) can only create endPoint gateway.
<br>So i write a customer ansible module to create endPoint interface and endPoint service. Detail


