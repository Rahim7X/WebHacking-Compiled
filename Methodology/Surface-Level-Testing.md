### No XSS But TBI

- Found A Parameter That Reflects User Input
```bash
https://app.example.com/API/Public/Login/HasCustomSAML/web?callback=text
https://app.clicktime.com/API/Public/Login/HasCustomSAML/web?callback=clicktime.com__has__been__moved_to::[attacker.com]
```

### API Request Updating Data
```bash
There is a api request that changes first name and last name
what if we add subscription=turue
```
### Rate Limit Attacks
- MASS Email Flooding Using Any Endpoint
- Any page that takes email as input and send any email
```bash
go to forgot password page add email 
Interceot Request
If Json data in being sent
Add multiple valid email parameter and valid emails
Now Send to intruder booom Flood
```
- Masss Commenting
- Mass File Uploading / GIF Flood
- No rate limit in faluty OTP Bruteforce
#### Rate Limit Bypasses
- Guess Header By Param Miner
- Insert Spaces At The End Of Paramater
- Insert %00 At The End Of Paramater
- Inserting some standard characters such as %0d (LF) , %2e, %20 %09
- Different User Agnet
- Different Cookie Parameter
- Hidden parameter
- Drop Captcha GET Request / POST request
[IP Block Bypass](https://infosecwriteups.com/bypass-rate-limit-request-fuzzing-etc-with-tor-3a285f3980d2)
### Lack of Password Confirmation When Changing Email
```bash
Attack Scenerio : When some forget to logout from the account in a publc computer, anyone can change the email to its 
own and verify it. And after that using the forget password feature, it can change the password too.
```


### Weak Password Policy
```bash
your website allowing users to set their password to simple, at this time, i can set my password to 123456 Determine the resistance of the application against brute force password guessing using available password dictionaries by evaluating the length, complexity, reuse and aging requirements of passwords.
you should make password policy to protect your user, Uppercase, lowcase. as it makes it much more secure it will be acceptable

REFERENCE : https://hackerone.com/reports/17160
```


