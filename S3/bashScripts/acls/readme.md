## Create a new bucket

aws s3 mb s3://morning-bucket-acls

## Create a file

echo "ACLs testing access rights" > acls.txt

## Upload a file to bucket 

aws s3 cp acls.txt s3://morning-bucket-acls

## Turn off public access

aws s3api put-public-access-block \
    --bucket morning-bucket-acls \
    --public-access-block-configuration "BlockPublicAcls=false,IgnorePublicAcls=false,BlockPublicPolicy=true,RestrictPublicBuckets=true"

## Check public access

aws s3api get-public-access-block \
    --bucket morning-bucket-acls