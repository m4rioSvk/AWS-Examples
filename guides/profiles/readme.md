## Setting up a profile

aws configure

## two files config or credentials

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