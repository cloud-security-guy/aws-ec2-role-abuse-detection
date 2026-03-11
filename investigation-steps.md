Investigation Steps for Suspected EC2 Role Abuse

Step 1 – Identify Suspicious API Activity

Review AWS CloudTrail logs for unusual API actions such as:

- CreateUser
- AttachUserPolicy
- CreateAccessKey
- DeleteTrail

These actions may indicate privilege escalation attempts.

Step 2 – Check the Identity Used

Look at the "userIdentity" field in the CloudTrail event.

If the value shows:

AssumedRole

This indicates the request used temporary credentials from an IAM role.

Step 3 – Identify the IAM Role

Find the role name inside the event:

Example:

AppServerRole

Investigate whether this role normally performs administrative actions.

Step 4 – Check the Source IP

Review the "sourceIPAddress" field.

If the IP address is outside expected infrastructure, it may indicate credential misuse.

Step 5 – Investigate the EC2 Instance

Determine which EC2 instance is associated with the IAM role.

Check:

- Running processes
- Application logs
- Possible vulnerabilities

Step 6 – Contain the Incident

Security teams may need to:

- Remove or restrict the IAM role permissions
- Rotate credentials
- Investigate compromised resources
