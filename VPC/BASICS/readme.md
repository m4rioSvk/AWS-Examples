If bash commands not working load 
source ~/.bashrc

log-in to log into AWS profile :-)

## Create our VPC
VPC_ID=$(aws ec2 create-vpc \
--cidr-block "172.1.0.0/16" \
--region ap-northeast-3 \
--tag-specifications 'ResourceType=vpc,Tags=[{Key=Name,Value=my-vpc3}]' \
--output json \
--query Vpc.VpcId)

echo $VPC_ID

## Create Internet GAteway IGW


## Attach IGW


## Create a new subnet


## Explicitily associate subnets


## Add a route for our Route Table to our IGW


