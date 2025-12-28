## Setting up a profile

aws configure

## two files config or credentials

## Change profile
export AWS_PROFILE=dev
echo "Current AWS profile: $AWS_PROFILE"

## Set up a region

aws configure set region us-west-2 --profile studentMario

## Clear the region out

aws configure set region "" --profile studentMario

## Print out specific value 

aws configure get region

## List profile

aws configure list-profiles

## Change the output

AWS_DEFAULT_OUTPUT=json

## ALWAYS SET UP THIS

export AWS_CLI_AUTO_PROMPT=on-partial
aws --cli-auto-prompt

## Update new profile with using Codespaces secret from the website

aws configure set aws_access_key_id "$AWS_ACCESS_KEY_ID" --profile codespaces-new
aws configure set aws_secret_access_key "$AWS_SECRET_ACCESS_KEY" --profile codespaces-new
aws configure set region "$AWS_DEFAULT_REGION" --profile codespaces-new

## Check profile credentials 

aws sts get-caller-identity --profile codespaces-new --output json

## Get permissions 

aws iam get-user --profile codespaces-new
