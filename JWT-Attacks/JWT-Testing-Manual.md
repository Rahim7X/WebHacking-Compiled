# Hacking Json Web Tokens

### What is JWT (Json Web Token)

After Login we get a session ID. Then the server checks that session id and which user contains it.
Then provides data by fetching from database

Now a days modern architectures are changed. Theere are multiple web servers managed by a 
single load balancer. So what if one clinet got his session id from server A
and the next request was sent to server B. Server won't be able to identify that user.
That's why JWT was intrduced.

Instead of fetching all data from database we can store it in user's local storage.
With a expiration time using JWT. It is signed with server signature so that user can't change the data inside the token without knowing the secret key.


### How JWT Works
- User Logged In 
- Now Server Will Fetch User's Data From Databse
- Then Server Creates A Secure JWT Token. And Assigns To The User.
- Now From The Client Side The Entire Data Will Be Transferred By Authorization Header to the server
- It is transferred in Base64 Encoded Format

## JWT Build Algorithm

It is a Json Format Based Token Which Contains 3 Parts. 
Encoded in base 64 Separated by .
- Header
- Payload
- Signature

Ex : 

Header : 
base64enc[{
"algo":"HS256",
"typ":"JWT"
}]

- alg - which algorithm is used to create the signature Ex : HS256,RS256,PS256

Payload :
base64enc[{
"firstname:"sss",
"lastname":"tmss",
"userid":"234"
}] 

Signature : 
HMACSHA256{
base64enc(header).base64enc(payload).secret(key)
}


### Seccurity Conserns In JWT

- Confidential Data Stored In JWT
- No Encryption Used In Transport Layer /On Wireshark 
- JWT Hijacking If Stored In Cookie
- Algo = None // Don't Validate The Signature
- Secret Key Bruteforcing


### Bugs
1 - None Algorith Attack
Change algo to none 
And try to perform action
Change algo to none + Remove All Data from Signature field

2 - Algo Change
RSA256 - Uses public key to verify token if we have that public key exposed we might be able to do this
Create own HS256 Signed JWT With Exposed public key
now The Server will Think The public Key is secret key and logs you in

How we found .pem in real senario. We find in leaking through jwk.json
or waybackurl's jwk.json file or .pem url

3 - Change Signature section complete 
Or Leave it blank

4 BruteForce HS256 
jwtbrute tool , jwt cracker


