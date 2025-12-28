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
