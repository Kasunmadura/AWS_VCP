# Installation Guide AWS command line 

![alt text](https://raw.githubusercontent.com/username/projectname/branch/path/to/img.png)

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
