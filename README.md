
A VPC is a virtual network inside AWS where you can isolate your setup using private IP addresses. A VPC consists of several subnets. Each subnet is bound to an Availability Zone. A public subnet has a direct route to the Internet. As long as your EC2 instances have an public IP they can communicate (in and out) with the Internet. A private subnet does not have a route to the Internet. Instances in private subnets can not be accessed from the public Internet. If you want to access the Internet from a private subnet you need to create a NAT gateway/instance


![alt text](https://raw.githubusercontent.com/Kasunmadura/AWS_VCP/blob/master/vpc.jpg)

This template describes a highly available Network Address Translation (NAT) instance that forwards HTTP, HTTPS and NTP traffic from a single private subnet to the Internet. You need one stack per availability zone. Example: If you use the vpc-2azs.yaml template, you will need two Nat Gateway stack in A and B.


# Installation Guide AWS command line 


1. You need to set up a proper IAM account which has the permission to run the cloud formation.
2. Install AWS cli and configure a profile with proper region
3. Run below awscli to implement the cnf
```bash

aws cloudformation create-stack --stack-name VPC-Management-Stack --template-body 
file://vpc-2azs.yaml --parameters file://vpc-2azs-temp.json --capabilities CAPABILITY_IAM --region us-west-2
```

4. Then run the natgw cloudformation template.For this you need to pass the parent stack name as parameter. (eg :VPC-Management-Stack ) 

```bash

aws cloudformation create-stack --stack-name VPC-Management-Natgw-StacK --template-body 
file://vpc-nat-gateway.yaml --parameters file://vpc-natgw.json --capabilities CAPABILITY_IAM --region us-west-2
```


Dependencies

vpc/vpc-*azs.yaml (required)
operations/alert.yaml (recommended)

author : Kasun Rathnayake
