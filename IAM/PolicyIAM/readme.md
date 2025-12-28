## Convert to json

yq -o json policy.yaml > policy.json

## Create policy 

```sh
aws iam create-policy \
--policy-name IAMfunPolicy \
--policy-document file://policy.json
```
## Update policy

```sh
aws iam create-policy-version \
    --policy-arn arn:aws:iam::794038257497:policy/IAMfunPolicy \
    --policy-document file://policy.json \
    --set-as-default
```
## Attach policy to a user

aws iam attach-user-policy \
--policy-arn arn:aws:iam::794038257497:policy/IAMfunPolicy \
--user-name IAM-policy-user

## The least privilege access

In json file, just update Resouce tab for example
"Resource": "*"   ---->   "Resource": "arn::aws:s3:::bucket-name"
    }
  ]

  Also change actions from s3*  to only specific action, such as ListBucket

## You can only have 5 updated versions of policy, you need to delete the first 4 to be able to keep updating it

aws iam delete-policy-version --policy-arn arn:aws:iam::123456789012:policy/MyPolicy --version-id v1
aws iam delete-policy-version --policy-arn arn:aws:iam::123456789012:policy/MyPolicy --version-id v2
aws iam delete-policy-version --policy-arn arn:aws:iam::123456789012:policy/MyPolicy --version-id v3
aws iam delete-policy-version --policy-arn arn:aws:iam::123456789012:policy/MyPolicy --version-id v4
## v1 is the first one 