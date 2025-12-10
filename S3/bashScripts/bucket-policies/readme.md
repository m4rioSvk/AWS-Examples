## Create a bucket

aws s3 mb s3://bucket-policies-examples-22

## Upload a policy

aws s3api put-bucket-policy --bucket bucket-policies-examples-22 --policy file://policyMS.json