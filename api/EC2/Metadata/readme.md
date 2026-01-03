## To get metadata from your EC2 instance

curl http://169.254.169.254/latest/metadata

Token1 or Token2

## IMDSv2
```sh
IMDSv2_TOKEN=$(curl -s -X PUT "http://169.254.169.254/latest/api/token" \
  -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")
```

## For instance ID

```sh
curl -s -H "X-aws-ec2-metadata-token: $IMDSv2_TOKEN" \
http://169.254.169.254/latest/meta-data/instance-id
```