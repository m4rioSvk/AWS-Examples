## Create a user with no permissions

New user with no permissions and grant access keys

```sh
aws iam create-user --user-name sts-machine-user
aws iam create-access-key --user-name sts-machine-user --output json
```

```sh
aws configure 
```
```sh
sts-machine-user
AKIA3RYC6I5MUPTAQTHC
DIhIgHOCVDcmB+qhc28T7gT6JONZWPGBoJZHRhK4
```
## Locate your profiles file
cat ~/.aws/credentials

## You can edit it with 

nano ~/.aws/credentials

Test who you are 
```sh
aws sts get-caller-identity 
aws sts get-caller-identity --profile studentMario    this is to change the profiles 
```
or in Codespaces 

```sh
export AWS_PROFILE=studentMario
echo $AWS_PROFILE
```
## Create a role 

New role that will access resources 

## Use new user credentials and assume role 

```sh
aws sts assume-role \
--role-arn arn:aws:iam::794038257497:role/my-sts-stack-fun-STSRole-DnyE8NZgFfOE \
--role-session-name s3-sts-fun \
--profile default
```

```sh
aws iam put-user-policy \
    --user-name sts-machine-user \
    --policy-name STS-assume \
    --policy-document file://policy.json
```
## Assumed role

 "Credentials": {
        "AccessKeyId": "ASIA3RYC6I5MRXSVXEYQ",
        "SecretAccessKey": "111pt79sQQiibCOQBUCbFbF/TkBVlVYvoUIgao/s",
        "SessionToken": "IQoJb3JpZ2luX2VjEGEaDmFwLW5vcnRoZWFzdC0zIkYwRAIgftyXuWuDM9mRPnIMQ/xrpsvh4B2VyHtTy/qcgq8j2GACIB0s9vp/QWvg2sF3COow5P/lCvTOJsjG+EfzdFCSqZ6PKpcCCCoQABoMNzk0MDM4MjU3NDk3IgwaqKc8wQaj9R9MmiEq9AG0MFo6A+htYtqTcEhemulb8nL+ay3uG2OB5JONyzCtVaarU/Iv7Mb7FdoH9hffaexSULZPG0eoHmzNdULDdQsJ/nPyTRLmrrDj0z2ZMwn29DmfJcJs0084Ms/JdbgJGQVmjvhkfqJxpW8Q2XuG59JL993rzaKnJLQD+2YuXZvOtVpPMngaRdIlI3lzVoKZoC/s6n2l2IbIT+X49CjK8/DXtcBAtehuuySb3+fGC+FzORMSVG9iUAIyJSxHW6VwrUIY8ZldhiS0WcFDDNa471wLjtqKWXalChU4Go/VDwI45zBEZTsR8v89LbNGIvdzoUJeLsccMP6W+MkGOp4BnxFeycm+mfdyrZGDmeCnOwjBIenOISIS2VkfkNDA1lCDiZKHMAVD+lNLWn7GD6+t3lorpGOlOcmHxafSI5fBpJ27F9uaCsEww3eyfBH85RVJgx9km35fFnsjJzXX15TF+7OaTQH1h/AIW/3mP8L12pf4qbRAtWihH9MQ62Wgb4WhVM32Ddh8BFYrsb0462W15Gwz3lgbtBkxxnMOj4U=",
        "Expiration": "2025-12-14T01:57:34+00:00"
    },
## Update new profile "assume" with the temporary credentials and change to updated assume profile through export AWS_PROFILE=assumed

## Test if you new profile works