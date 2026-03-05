CloudTrail Log Analysis for EC2 Role Abuse

Introduction

When an attacker uses stolen IAM role credentials from an EC2 instance, their actions will generate AWS API calls. These actions are recorded in AWS CloudTrail logs.

Analyzing these logs helps security teams detect suspicious behavior.

Key CloudTrail Fields to Monitor

userIdentity.type

For EC2 role credentials, this field will usually appear as:

AssumedRole

This indicates that the API call was made using temporary credentials from an IAM role.

userIdentity.sessionContext.sessionIssuer.userName

This field shows the name of the IAM role used.

Example:

AppServerRole

sourceIPAddress

This field shows where the request originated.

If the source IP is unexpected or external, it may indicate credential abuse.

eventName

This field shows the API action performed.

Examples of high-risk actions include:

- CreateUser
- AttachUserPolicy
- CreateAccessKey
- DeleteTrail
- StopLogging

Example Suspicious Pattern

A typical attack pattern may look like:

1. ListBuckets
2. GetObject
3. CreateUser
4. AttachUserPolicy

This sequence may indicate reconnaissance followed by privilege escalation.

Detection Opportunity

Security teams can detect suspicious EC2 role activity by identifying unusual API calls or unexpected behavior from IAM roles in CloudTrail logs
