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

## Set up created NACLS
myIPv4 = 123.48.34.98

## MUST BLOCK INBOUND AND OUTBOUND TRAFFIC SEPPARATELY


```sh
aws ec2 create-network-acl-entry \
--network-acl-id acl-0095fd7779f125037 \
--rule-number 90 \
--protocol -1 \
--rule-action deny \
--ingress \
--cidr-block 123.48.34.98/32
```

  ## /32 means SINGLE IP only !!

## Outbound = egress true
aws ec2 create-network-acl-entry \
  --network-acl-id acl-0095fd7779f125037 \
  --rule-number 90 \
  --protocol -1 \
  --rule-action deny \
  --egress true \
  --cidr-block 123.48.34.98/32


## Verify

aws ec2 describe-network-acls \
  --network-acl-ids acl-0095fd7779f125037 \
  --output table















### EC2 SECTION ### EC2 SECTION
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