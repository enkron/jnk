# aws
```bash
aws --profile <profile_name> -ccdd --region us-west-2 ec2 describe-instance-status \
--filters Name=instance-state-name,Values=running
# describe aws running instances in specific region

aws codecommit list-repositories --region eu-central-1
# list code commit repos.

aws codecommit get-repository --repository-name MyDemoRepo --region eu-central-1
# get metadata about single repo.

aws lambda --region eu-central-1 list-functions
aws lambda create-function --function-name my-function \
--zip-file fileb://function.zip --handler index.handler --runtime python3.7 \
--role arn:aws:iam::12836736247:role/lambda-cli-role
# create lambda function

aws --region eu-central-1 lambda invoke --function-name test_lambda_invoke out \
--log-type Tail --query 'LogResult' --output text |base64 -e
#trigger lambda func

aws --profile stage s3api put-object --bucket <bucket_name> -np --key some/bucket/path/
# put empty object to s3 (folder in this case)

aws s3api list-object-versions --bucket <bucket_name> --prefix <bucket_path>
#returns metadata about all of the versions of objects in a bucket

aws --profile <profile_name> --region <aws_region> s3api put-bucket-policy \
    --bucket <bucket_name> --policy file://policy.json

aws s3api create-bucket --bucket <bucket_name> --region <aws_region> \
    --create-bucket-configuration LocationConstraint=us-west-2 --acl private
```
