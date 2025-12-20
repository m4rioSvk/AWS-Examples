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
aws ec2 create-network-acl --vpc-id vpc-02e856b237501a67f
```

## Get AMI for Amazon Linux 2
Amazon Linux 2 AMI (HVM), SSD Volume Type (64-bit x86) Operating System
AWS SSM public AMI parameters always reference Amazon-owned images.
This command is to grab the latest AMI image.

```sh
$ aws ssm get-parameter \
  --region ap-northeast-3 \
  --name /aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2 \
  --query Parameter.Value \
  --output text
```

## Find out eligible Free tiers

aws ec2 describe-instance-types \
  --region ap-northeast-3 \
  --filters Name=free-tier-eligible,Values=true \
  --query 'InstanceTypes[*].InstanceType' \
  --output table