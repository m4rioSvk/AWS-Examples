## Create a bucket

aws s3 mb s3://encryption-ms-222

## Create a file

echo "hello encryption" > hello2.txt
aws s3 cp hello.txt s3://encryption-ms-222


## Put object with encryption SSE-KMS

aws s3api put-object --bucket encryption-ms-222 --key hello2.txt \
--body hello2.txt \
--server-side-encryption aws:kms \
--ssekms-key-id 2d7ae591-95bb-4a5b-a9d7-049fe00b81a0

<!-- ## aws kms list-keys -->
```sh AWS managed KEYS----KEY ID
                    2d7ae591-95bb-4a5b-a9d7-049fe00b81a0
```
encryption2-ms-333

## Download object 
aws s3 cp s3://encryption-ms-222/hello.txt hello.txt

<!-- we were able to do it because we were granted permission -->

## Put object with SSE-C

aws s3api put-object --bucket encryption-ms-222 --key hello2.txt \
--body hello2.txt \
--sse-customer-algorithm AES256 \
--sse-customer-key AElzOhMGiUgFvVgsDD5M39ttubt/Oi7UCHESRW8ezzA= \
--sse-customer-key-md5 48sDPFV8JbEIRczyANq+9g==


## Generate your own AES256 key (the key cannot be in hex value but must be in base64 value, therefore must be converted)

## Step 1.
openssl rand -hex 32

## Step 2.
echo -n "0049733a1306894805bd582c0c3e4cdfdb6db9bb7f3a2ed4087112456f1ecf30" \
| xxd -r -p \
| base64

## Generate md5 value of your AES256 key

echo -n "0049733a1306894805bd582c0c3e4cdfdb6db9bb7f3a2ed4087112456f1ecf30" \
| xxd -r -p \
| openssl md5 -binary \
| base64
