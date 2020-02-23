# aws-account-bootstrap

## Admin role

Create an IAM role that temporarily grants admin permissions. 

The role can only be assumed by a specified MFA enabled IAM user.

### Create an admin role

With a privileged user:

    # This MFA enabled IAM user may assume the admin role
    IAM_USER='my-iam-user'

    # This cloudformation stack creates the admin role
    aws cloudformation create-stack \
      --stack-name 'aws-account-bootstrap-admin-role' \
      --template-body file://iam/admin-role.yml \
      --parameters ParameterKey=IamUserThatMayAssumeRole,ParameterValue="$IAM_USER" \
      --capabilities CAPABILITY_NAMED_IAM

### Command line: Assuming the admin role (so you can start using it)

Use the AWS CLI for that. 

It can take a few steps before you're set to go. I suggest you just grab the bash script here:
 [iam/assume-role](iam/assume-role). This is how to use it:

     . iam/assume-role my-admin-profile admin

Where `my-admin-profile` is the name of the AWS profile in `~/.aws/credentials` and `admin` is the 
name (not full ARN) of the IAM role to assume.