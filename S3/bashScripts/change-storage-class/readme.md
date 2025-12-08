## Create a bucket

aws s3 mb s3://mario-evening-33 

## Create a file

echo "Ahoj Majko">hello.txt

## Upload a file

aws s3 cp hello.txt s3://mario-evening-33 --storage-class STANDARD_IA