
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

## JWT authentication bypass via jwk header injection
- JSON WEB KEY sometimes used to embed the correct verification key directly in the token

```bash
    "kty" (Key Type): This parameter specifies the type of key. It can take values like "RSA" for RSA keys, "EC" for elliptic curve keys, or "oct" for symmetric keys.

    "kid" (Key ID): This parameter provides a unique identifier for the key. It helps in key management scenarios where multiple keys are involved.

    "alg" (Algorithm): This parameter indicates the algorithm associated with the key. For example, "RS256" represents the RSA signature algorithm with SHA-256.

    "use" (Key Use): This parameter specifies the purpose of the key, such as "sig" for a key used for signing or "enc" for encryption.

    "n" and "e" (RSA-specific): These parameters represent the modulus and exponent of an RSA public key.

    "crv" and "x"/"y" (Elliptic Curve-specific): These parameters represent the curve type and the coordinates of the public key point on the curve.

    "k" (Symmetric key): This parameter represents the value of the symmetric key.
```

- How to do JWK header injection
 ```
Go to the JWT Editor Keys tab in Burp's main tab bar.
Click New RSA Key.
lick Generate to automatically generate a new key pair, then click OK to save the key.
in JWT  change the value of the sub claim to administrator. 
At the bottom of the JSON Web Token tab, click Attack, then select Embedded JWK. When prompted, select your newly generated RSA key and click OK. 
In the header of the JWT, observe that a jwk parameter has been added containing your public key. 
Send request DONE!!
 ```


## JWT authentication bypass via jku header injection
When the "jku" parameter is present in the JWT header, it indicates that the public keys needed to verify the token's signature can be found at the specified URL. This allows for more efficient key management, as the keys can be rotated or updated independently of the tokens themselves.
```bash
{
  "alg": "RS256",
  "typ": "JWT",
  "jku": "https://example.com/keys.jwks"
}
```

- Solving The Lab

```bash
Go to the JWT Editor Keys Click New RSA Key.  click Generate to automatically generate a new key pair, then click OK to save the key
open exploit.html
add following code inside boy tag



{
    "keys": [

    ]
}

Back on the JWT Editor Keys tab, right-click on the entry for the key that you just generated, then select Copy Public Key as JWK. 
Paste the JWK into the keys array on the exploit server, then store the exploit. The result should look something like this: 
{
    "keys": [
        {
            "kty": "RSA",
            "e": "AQAB",
            "kid": "893d8f0b-061f-42c2-a4aa-5056e12b8ae7",
            "n": "yy1wpYmffgXBxhAUJzHHocCuJolwDqql75ZWuCQ_cb33K2vh9mk6GPM9gNN4Y_qTVX67WhsN3JvaFYw"
        }
    ]
}

in the header of the JWT, replace the current value of the kid parameter with the kid of the JWK that you uploaded to the exploit server. 
Add a new jku parameter to the header of the JWT. Set its value to the URL of your JWK Set on the exploit server.
{
  "alg": "RS256",
  "typ": "JWT",
  "jku": "https://example.com/keys.jwks"
}

change the value of the sub claim to administrator.
click Sign, then select the RSA key that you generated in the previous section
then click OK. 
DONE!!

```


### JWT authentication bypass via kid header path traversal
 the server uses the kid parameter in JWT header to fetch the relevant key from its filesystem
```bash
Go to the JWT Editor Keys tab in Burp's main tab bar. Click New Symmetric Key. click Generate
Replace the generated value for the k property with a Base64-encoded null byte (AA==). 
Click OK to save the key. 
change the value of the kid parameter to a path traversal sequence pointing to the /dev/null file:
../../../../../../../dev/null 
 change the value of the sub claim to administrator
 click Sign, Clck ok
 DONE !!

```

### JWT authentication bypass via algorithm confusion
- found jwks.json leaking RSA public key in /jwks.json
```bash
Copy JWK object from inside of key array
go to jwt key editor tab
Say New RSA Key
Paste JWK Object
ANd click ok
righclick And copy as public pem
run python script for algo confusion
DONE!!!
```
