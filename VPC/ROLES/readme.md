aws iam create-role \
  --role-name EC2SSMRole \
  --assume-role-policy-document file://ec2-trust-policy.json