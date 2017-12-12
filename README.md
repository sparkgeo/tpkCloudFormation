# tpkCloudFormation

CloudFormation templates for the tpk back end and front end stacks.

## Usage

Build the back end stack with the following command - This template uses the
[serverless-application-model](https://github.com/awslabs/serverless-application-model/blob/master/HOWTO.md).
Because the serverless-application-model uses a [transform](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/transform-section-structure.html)
it is necessary to use the `deploy` [command](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-cli-deploy.html) to deploy the stack.

## Back end stack

Ensure that the credentials associated with the IAM group used by the [awscli](https://aws.amazon.com/cli/)
have sufficient privleges for creating the resources described in the template.

To create the back end stack run

```bash
aws cloudformation deploy --template-file template.json /
--stack-name stackName --capabilities CAPABILITY_NAMED_IAM /
--parameter-overrides AdministratorEmail=email@email.org /
SourceEmail=email@email.org
```
`stackName` is the name of your back end stack.
`AdministratorEmail` is the email address which will receive notifications when
a tpk job fails in AWS Batch.
`SourceEmail` is the From email address used to send notifications to users when
completed tpks are completed or a tpk job has failed.

For use with SES the `SourceEmail` will need to be [verified](http://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-email-addresses.html)
via the AWS console.

In addition to send email to an unlimited list of recipients the SES account
needs to be [moved out](http://docs.aws.amazon.com/ses/latest/DeveloperGuide/request-production-access.html) of the sandbox via the AWS console.

