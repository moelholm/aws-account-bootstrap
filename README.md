# aws-account-bootstrap

## Admin role

Create an IAM role that temporarily grants admin permissions. 

The role only can be assumed by a specified MFA enabled IAM user.

### Create an admin role

With a privileged user:

    # This MFA enabled IAM user may assume the admin role
    export IAM_USER='my-iam-user'

    # This cloudformation stack creates the admin role
    aws cloudformation create-stack \
      --stack-name 'aws-account-bootstrap-admin-role' \
      --template-body file://iam/admin-role.yml \
      --parameters ParameterKey=IamUserThatMayAssumeRole,ParameterValue="$IAM_USER" \
      --capabilities CAPABILITY_NAMED_IAM
