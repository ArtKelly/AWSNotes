↼ [[Index]]
## Securing the root account
- Ensure Root account has MFA setup
- Create an admin group for your adminsitrators and assign the appropriate permissions for this group
- Create user accounts for administrators
- Add your users to the admin group

## Controlling Users with IAM policy documents
- Assign to groups / users / roles

## Permanent IAM Credentials
- Its best practice for users to inherit permissions from groups
- Never share user credentials. 1 user = 1 person
- Principle of least privilege
	- Only assign a user the minimum amount of privileges they need to do their job
- By default users have no permissions
- Always setup password rotations
- IAM Federation: You can combine your existing user account with AWS. e.g. when you login to windows using Active Directory, you can use the same credentials to log into AWS if you setup federation
- Identity Federation: Uses the SAML standard, which is active directory

## Review
