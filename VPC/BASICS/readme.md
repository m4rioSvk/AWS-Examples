If bash commands not working load 
source ~/.bashrc

log-in to log into AWS profile :-)

## Create our VPC
aws ec2 create-vpc \
--cidr-block "172.1.0.0/16" \
--region ap-northeast-3 \
--tag-specifications 'ResourceType=vpc,Tags=[{Key=Name,Value=my-vpc3}]' \
--output json \
--query Vpc.VpcId

## Create default VPC if accidentaly deleted

aws ec2 create-default-vpc --region


## Create Internet GAteway IGW


aws ec2 create-internet-gateway \
--query InternetGateway.InternetGateway.Id \
--output text


## Attach IGW

aws ec2 attach-internet-gateway --internet-gateway-id $IGW_ID --vpc-id $VPC_ID

## Create a new subnet

aws ec2 create-subnet --vpc-id $VPC_ID --cidr-block 172.1.0.0/20

## Add auto-assign public IPv4 on launch

aws ec2 modify-subnet-attribute \
--subnet-id $SUBNET_ID \
--map-public-ip-on-launch

## Find a default route table through query
aws ec2 describe-route-tables --output table
echo "VPC_ID=[$VPC_ID]"

aws ec2 describe-route-tables \
--filters "Name=vpc-id,Values=$VPC_ID" "Name=association.main,Values=true" \
--output text


echo "RT_ID: $RT_ID"

## Explicitily associate subnets

aws ec2 associate-route-table --route-table-id $RT_ID --subnet-id $SUBNET_ID

# Deployment extra set-ups

## DNS-hostname resources MUST BE ALLOWED FIRST (usually default ON) RESOLUTION

aws ec2 modify-vpc-attribute \
--vpc-id "$VPC_ID" \
--enable-dns-support

## Enable DNS-hostname ON

aws ec2 modify-vpc-attribute \
--vpc-id $VPC_ID \
--enable-dns-hostnames "{\"Value\"true:"}"


## Add a route for our Route Table to our IGW

aws ec2 create-route --route-table-id $RT_ID --destination-cidr-block 0.0.0.0/0 --gateway-id $IGW_ID

