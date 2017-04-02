# Rebuild AMI using SSM Automation

This Automation document demonstrates how to remove ephemeral block device mappings from source AMI by creating a new AMI in your AWS account.

For detailed post see: http://blog.shvetsov.com/

For this example to work you will need to:

- install awscli
- configure your .aws/credentials
- configuring IAM Roles for Automation as described in: https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-ami-permissions.html
- create automation doc in your AWS account with:
```
aws ssm \
create-document \
--name "TVLK-ami-sans-bdm" \
--content "file://TVLK-ami-sans-bdm.json" \
--document-type "Automation"
```
- execute automation, but replace fake `AutomationAssumeRole`, `SubnetId` and `SourceAmiId` values with real parameters:
```
aws ssm \
start-automation-execution \
--document-name "TVLK-ami-sans-bdm" \
--parameters \
"AutomationAssumeRole=arn:aws:iam::123456789012:role/YourAutomationRole,SubnetId=subnet-12345678,SourceAmiId=ami-XXXXXX"
```
