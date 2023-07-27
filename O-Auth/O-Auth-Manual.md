# O-Auth Stands For Open Authorization
## O-Auth WorkFlow
### Authorization Code GrantFlow
- User Clicked Login With Facebook
- It will redirect user to Facebook O-Auth Page Where The Data Will Be Sent As Get Parameter
```bash
http://facebook.com/dialogue/oauth?email=bla@mail.com&user_id=1234
```
- User Clicks Continue
- Facebook Redirects The User To Client Application With A Authorization Code
- Then User's Browser makes a get request along with authorization token to facebook server
- Server responds with acess token
- Then the client browser makes a request to his server and assigns a JWT / Authorization token Build With O-Auth Detials 
- And Validates The Client
 
### Implicit Code GrantFlow
- User initiates the flow
- Client redirects the user to the authorization server along with required parameters
- User authenticates and grants permission
- Authorization server redirects back to the client. the authorization server generates an access token and includes it in the redirect URL.
- The access token is included as a fragment identifier in the URL after the '#' symbol.
- Client receives the access token: The client application extracts the access token from the fragment identifier of the redirect URL
- The client application can now use the access token to access protected resources by including it in the Authorization header.

## Vulns To Check

#### Authentication bypass via OAuth implicit flow
- Client App Redirects The User To O-Auth Page With Email, CLient ID , State, Scope, Redirect URI
- User Authenticates And Grants Permission In O-Auth Page
- O-Auth Page Redirected User To Client Redirect URI Parameter Along With Access Token
- Then To Assign A Valid Session To User Client App Made A POST Request To To Their Server Along With That Same Acess Token, Email, Client Id
- Now In This Request Client Is Not Validating Email So If We Change The Email To Victim's App Will Assign Us Victim Session

#### Forced OAuth profile linking via CSRF
- There is an option to link social media account so that we can log in again without username and password
- Log in normally and initate request for add social profile
- Social Media App Redirects To O-Auth-Linking Endpoint After Process Is Done
- This is the request where web server knows who we are
- Dont Initiate /oauth-linking request to webserver
- Do Intercept - Engament Tools - Generate CSRF POc- Send This To Admin
- When Admin CLicks The Link Our Social Account Will Be Connected WIth Admin's Session / Account


#### Resusing acces token
- WHEN browser sending request for code intercept if send to repeater
- then forward request
- now you saved the previous request used that request to check if the code is not expired 
- and you are able to get access to access token then it is a bug
- becouse if the code is leaked any when it can be used to hack user account

#### Use the same code twise to get access token
#### Misconfigured Google O auth can lead to account takeover 
- Employee Login Portals
- If google O -auth page pops up in any subdomain try
```bash
https://accounts.google.com/o/oauth2/auth/identifier?access_type=offline&client_id=xxx.googleusercontent.com&hd=gmail.com&redirect_uri=https://target/oauth/callback&response_type=code&scope=mail
```
- Here hd parameter is set to gmail.com. If misconfigured attacker can log in with own email
#### Account Squatting
- Hacker signed up using victim email but don't have access to verification link
- Victim Signed Up Using O-auth
- Verification Bypassed
- Now hacker can acessed victim account with uname and password

