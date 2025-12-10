## Create a new bucket

```sh
aws s3 mb s3://morning-bucket-acls
```

## Create a file

```sh
echo "ACLs testing access rights" > acls.txt
```


## Upload a file to bucket 
```sh
aws s3 cp acls.txt s3://morning-bucket-acls
```


## Turn off public access
```sh
aws s3api put-public-access-block \
    --bucket morning-bucket-acls \
    --public-access-block-configuration "BlockPublicAcls=false,IgnorePublicAcls=false,BlockPublicPolicy=true,RestrictPublicBuckets=true"
```
## Check public access
```sh
aws s3api get-public-access-block \
    --bucket morning-bucket-acls
```
## Change bucket ownership


aws s3api put-bucket-ownership-controls \
    --bucket morning-bucket-acls \
    --ownership-controls='Rules=[{ObjectOwnership=BucketOwnerPreferred}]'


## Suggested fix

aws s3api put-public-access-block \
    --bucket morning-bucket-acls \
    --public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true"


aws s3api put-bucket-ownership-controls \
  --bucket morning-bucket-acls \
  --ownership-controls '{"Rules":[{"ObjectOwnership":"ObjectWriter"}]}'

## Stage 2

aws s3api put-object-acl --bucket morning-bucket-acls --key myfile.txt --acl public-read

## Add permissions to another account

aws s3api put-bucket-acl 
--bucket morning-bucket-acls 
--grant-full-control emailaddress=user1@example.com,emailaddress=user2@example.com 
--grant-read uri=http://acs.amazonaws.com/groups/global/AllUsers

