## Convert to json

yq -o json policy.yaml > policy.json

## Create policy 

```sh
aws iam create-policy \
--policy-name IAMfunPolicy \
--policy-document file://policy.json
```
