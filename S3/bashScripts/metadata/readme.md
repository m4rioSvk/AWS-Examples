## Create a bucket

aws s3 mb s3://metadata-fun-ms333 

## Create a new file

echo "Hello Mars" > hello.txt

## Upload file with metadata

aws s3api put-object --bucket metadata-fun-ms333 --key hello.txt --metadata Planet=Mars

## Get metadata through head object

aws s3api head-object --bucket metadata-fun-ms333 --key hello.txt
 