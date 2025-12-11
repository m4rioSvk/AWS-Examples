## Create a bucket

aws s3 mb s3://encryption-ms-222

## Create a file

echo "hello encryption" > hello.txt
aws s3 cp hello.txt s3://encryption-ms-222


## Put object with encryption

aws s3api put-object --bucket encryption-ms-222 --key hello.txt \
--body hello.txt \
--server-side-encryption aws:kms
--ssekms-key-id 

<!-- ## aws kms list-keys -->

encryption2-ms-333
