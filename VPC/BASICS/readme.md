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


## Create Internet GAteway IGW


aws ec2 create-internet-gateway \
--query InternetGateway.InternetGateway.Id \
--output text


## Attach IGW

aws ec2 attach-internet-gateway --internet-gateway-id $IGW_ID --vpc-id $VPC_ID

## Create a new subnet

aws ec2 create-subnet --vpc-id $VPC_ID --cidr-block 172.1.0.0/20

## Find a default route table through query

aws ec2 describe-route-tables \
--filters "Name=vpc-id,Values=$VPC_ID" \
--query "RouteTables[?Associations[?Main==\`true\`]].RouteTableId" \
--output text

## Explicitily associate subnets

aws ec2 associate-route-table --route-table-id rtb-22574640 --subnet-id subnet-9d4a7b6c


## Add a route for our Route Table to our IGW


