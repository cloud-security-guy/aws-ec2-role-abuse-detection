Detection Logic for EC2 IAM Role Abuse

Objective

The goal of detection is to identify suspicious AWS API activity that may indicate stolen IAM role credentials from an EC2 instance.

Security teams should focus on identifying abnormal behavior rather than every assumed role event.

Key Detection Signals

1. Assumed Role Identity

CloudTrail logs will show:

userIdentity.type = AssumedRole

This indicates the action was performed using temporary role credentials.

2. High-Risk IAM API Calls

Certain API actions are strong indicators of privilege escalation attempts.

Examples include:

- CreateUser
- AttachUserPolicy
- PutRolePolicy
- CreateAccessKey
- DeleteTrail
- StopLogging

3. Unusual Source IP

If the request originates from an unexpected IP address outside the normal infrastructure, this may indicate credential misuse.

4. Unusual Role Behavior

Application roles typically have limited permissions.

If a role that normally accesses S3 suddenly performs IAM administrative actions, it should trigger investigation.

Example Detection Rule

Alert when:

- userIdentity.type = AssumedRole
- AND eventName is a high-risk IAM API
- AND role normally does not perform administrative actions

Investigation Steps

When such an alert occurs, security teams should:

1. Review all CloudTrail events in the session
2. Check whether new IAM users or access keys were created
3. Verify the source IP address
4. Investigate the EC2 instance associated with the IAM role

Mitigation

- Apply least privilege to IAM roles
- Monitor CloudTrail logs continuously
- Use automated detection rules for high-risk API activity
