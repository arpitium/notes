# IAM : Identity and access management

## 1: Users and Groups

- Global service
- Root account created by default, shoudnt be used or shared
- Groups and users -> many to many

---

## 2 Policies

- Polcies are inherited to users from groups
- If a user is part of multiple groups, he/she will inteherit policies assigned to both groups

### 2.1 Policy Structure

Policy 1: DenyCustomerBucket

```json
{
  "Version": "2012-10-17",
  "Id": "Deny-Customer-Bucket",
  "Statement": [
    {
      "Sid": "FullAccess",
      "Effect": "Allow",
      "Action": ["s3:*"],
      "Resource": ["*"]
    },
    {
      "Sid": "DenyCustomerBucket",
      "Effect": "Deny",
      "Action": ["s3:*"],
      "Resource": ["arn:aws:s3:::customer", "arn:aws:s3:::customer/*"]
    }
  ]
}
```

Policy consists of:

- Version
- Id: An identifier for the policy (optional)
- Statement : One or more individual statements (required)

Statement consists of:

- Sid: An identifier for the statement
- Effect: Allow/Deny
- Principal : account/user/role to which this policy appied to (optional)
- Action: List of actions that this policy allows or denies
- Resource: List of resources to which the actions applied to

---

## 3. MFA : Multi factor authentication

### 3.1 AWS Password policy

- Set minimum password length
- Require specific character types (lower, upper, numeric, special)
- ALlow all IAM users to change their own passwords
- Require users to change their password after some time (password expiration)
- Prevent password reuse

### 3.2 MFA

- Multifactor authentication
- Along with password, this makes aws account more secure
- Device types:
  - Virtual (Google Authenticator, Microsoft Authenticator, Okta, Authy)
  - Physical (Universal 2nd factor U2F key): Yubikey by yubico
  - Hardware key Fob MFA device
  - AWS GovCloud SurePassID

---

## 4. IAM Roles

- Permissions assigned to AWS executable services like EC2, lambda, ECS/EKS containers, Roles for cloud formation

---

### 5. IAM security tools

- IAM Credentials report (Account level)

  - A report that lists all your account's users and the status of their various credentials

- IAM access advisor
  - Shows the service premissions granted to a user and when those services were last accessed
