## GET VPC ID 2 OPTIONS

aws ec2 describe-vpcs \
--query "Vpcs[].VpcId" \
--output text

# GET VPC ID 

aws ec2 describe-vpcs \
--filters "Name=tag:Name,Values=project-NACLS-vpc" \
--query "Vpcs[0].VpcId" \
--output text


## Create a NACL
VPC_ID=vpc-02e856b237501a67f/ project-NACLS-vpc

```sh
aws ec2 create-network-acl --vpc-id $VPC_ID project-NACLS-vpc
```