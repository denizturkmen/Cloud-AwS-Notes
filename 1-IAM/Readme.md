# IAM: Identity Access Management

IAM stands for Identity Access Management

Global service

**Root account** created by default. it shouldn't **shared and usaged**.

**Users = people**

Groups: Only contain user

User -> N groups. Users can belong to more than one groups

**Permissions:** Users or Groups can be assigned JSON documents called policies.
``` bash
{
  "Version": "2012-10-17",  # policy language version, always include "2012-10-17"
  "Id": "S3 Account Permissions" # an identifier for the policy (optional)
  "Statement": [ # one or more individual statements (required)
    {
      "Sid": "FirstStatement", # an identifier for the statement (optional)
      "Effect": "Allow", # whether the statement allows or denies access (Allow, Deny)
      "Action": ["iam:ChangePassword"],  # list of actions this policy allows or denies
      "Resource": "*" # list of resources to which the actions applied to
    },
    {
      "Sid": "SecondStatement",
      "Effect": "Allow",
      "Action": "s3:ListAllMyBuckets",
      "Resource": "*"
    },
    {
      "Sid": "ThirdStatement",
      "Effect": "Allow",
      "Action": [
        "s3:List*",
        "s3:Get*"
      ],
      "Resource": [
        "arn:aws:s3:::confidential-data",
        "arn:aws:s3:::confidential-data/*"
      ],
      "Condition": {"Bool": {"aws:MultiFactorAuthPresent": "true"}} # conditions for when this policy is in effect (optional)
    }
  ]
}
```

**IAM – Password Policy** Strong passwords = higher security for your account

**Multi Factor Authentication - MFA** You want to protect your Root Accounts and IAM users

**How can users access AWS**
To access AWS, you have three options:
 • AWS Management Console (protected by password + MFA)
 • AWS Command Line Interface (CLI): protected by access keys
 • AWS Software Developer Kit (SDK) - for code: protected by access keys

Access Keys are secret, just like a password. Don’t share them
Access Key ID == username
Secret Access Key == password


**What’s the AWS CLI**


**IAM Roles for Services**
we will assign permissions to AWS services with IAM Roles


**IAM Guidelines & Best Practices;**
• Don’t use the root account except for AWS account setup
• One physical user = One AWS user
• Assign users to groups and assign permissions to groups
• Create a strong password policy
• Use and enforce the use of Multi Factor Authentication (MFA)
• Create and use Roles for giving permissions to AWS services
• Use Access Keys for Programmatic Access (CLI / SDK)
• Audit permissions of your account using IAM Credentials Report & IAM
Access Advisor
• Never share IAM users & Access Keys