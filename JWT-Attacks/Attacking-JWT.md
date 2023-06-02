
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

