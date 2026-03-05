EC2 IAM Role Abuse – Attack Scenario

#Introduction

Amazon EC2 instances often use IAM roles to access other AWS services securely. These roles provide temporary credentials that applications running on the instance can use.

However, if an attacker gains access to the EC2 instance or exploits a vulnerability in an application running on it, they may be able to retrieve these credentials.

Step 1 – IAM Role Attached to EC2

An EC2 instance is configured with an IAM role. This role grants permissions to access specific AWS services such as Amazon S3 or CloudWatch.

The role credentials are automatically available through the EC2 metadata service.

Step 2 – Accessing the Metadata Service

The EC2 metadata service is accessible at:

http://169.254.169.254

Applications on the instance can query this endpoint to retrieve temporary credentials associated with the IAM role.

Step 3 – Credential Theft

If an attacker exploits a vulnerability such as Server-Side Request Forgery (SSRF), they may be able to access the metadata endpoint and obtain the IAM role credentials.

These credentials typically include:

- Access Key ID
- Secret Access Key
- Session Token

Step 4 – Using Stolen Credentials

The attacker can configure the AWS CLI using the stolen credentials and start making AWS API calls.

For example:

- Listing S3 buckets
- Creating IAM users
- Attaching policies
- Accessing sensitive data

Step 5 – Detection Opportunity

These API calls will appear in AWS CloudTrail logs under an assumed role identity.

Security teams can detect suspicious behavior by monitoring unusual API activity from EC2 roles.
