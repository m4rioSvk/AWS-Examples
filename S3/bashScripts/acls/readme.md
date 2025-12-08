## Create a new bucket

aws s3 mb s3://morning-bucket-acls

## Create a file

echo "ACLs testing access rights" > acls.txt

## Upload a file to bucket 

aws s3 cp acls.txt s3://morning-bucket-acls
