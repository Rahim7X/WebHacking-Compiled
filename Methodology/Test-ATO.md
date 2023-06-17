# Account Takeover Cases
- Host Manipulation
- IDOR
- Parameter Pollution
- Password Reset Poisioning
- OTP BruteForcing
- Pre Account Takeovers
### Host Manipulation
- Understand the reset password function. Check how it works normally. Then tamper which it / Change host heeader.
- Host: target.com to Host: evil.com
- Check If Evil.com reflected in reset link

### CSRF On 2Fa Disable Feature

### IDOR to ATO
- Change Email To Anyone Else WHen Resetting The Password
- Chnage UID to reset another user's passweord

### Parameter Pollution
- Add Two Email In Same Request
- CHange Email Order
- Provide list of email

### JSon variable
- ADD {“token”:null} etc
### Password Reset Poisioning
- Change Host heafer to attacker's domain when requesting for password reset link. 
- Usually It Uses host header to determine how to construct reset link

### OTP Bruteforcing
- There should be no rate limit in wrong otp bruteforcing
- If Site Uses OTP Method 
- Then You Are In Luck

### Pre ATO
- It Usually Happens When You Are Able To Bypass Email Verification
- Try Adding Extra Parameter In Change Info Function "email": "victim@gmail.com",

### 2FA Bypass
- Response/Status Code Manipulation (Changing a 403 permissions to a 200 ‘ok’)
- Brute force OTP using a tool like Burpsuite.
- Permanet OTP: One that doesn’t expire after usage, or even if the code doesn’t expire after 3–4 hours.
- Request 2 tokens from account ‘attacker’ and ‘victim’. Use the attacker’s token in victim’s account.
- Try to go directly to the dashboard URL without solving the 2FA. If it fails, try adding the referral header to the 2FA page url in the same request going to dashboard.
- Search the 2FA code for response or Javascript files (.js) using Burp search.
- CSRF/Clickjacking to disable 2FA.
- Enabling 2FA doesn’t expire previous sessions.
- Password can be reset via forgot password without 2FA, or 2FA can be disabled in personal settings without a 2FA code.
- Enter 0’s in the code. For example, if it’s a 6 digit code use 000000 as 2FA.
- Request Manipulation: Null JSON response, change the “OTP required” parameter from true to false, remove the 2fa code, remove both code and parameter, in JSON give email as an array. (More - information)
- You may able to get the backup codes using the following request 
- ADD json value as null 

## Underrated Methods
```bash
1 : ClickJacking To Account Takeover
:: User Deleted The account at the same point you created an account with same username
:: Now You Will Get Deleted Account Session
3 : If two app works the same copy 1 app cokie and paste in another app check if action is sucessful
eg : amzon india cookei on amzom.com
4 : Braking Authentication Flow Using Response Manipulation
5 : SSO Takeover & redirect_uri[0=attacker.com
6 : changing Email on o-auth confirmation
```

# Firing 8 Account Takeover Methods 🔥

### 1. Unicode Normalization Issue
- Victim account `victim@gmail.com`
- Create an account using Unicode
- Example: `vićtim@gmail.com`
- List of Unicode character: [https://en.wikipedia.org/wiki/List_of_Unicode_characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters)
- Note: check where verification doesn’t require
<br>&nbsp;

### 2. Authorization Issue
- Change email of Account `A` and put email `B`
- Check confirmation mail in account `B`
- Open the confirmation mail from account `C`
- Taken over Account `C`
<br>&nbsp;

### 3. Reusing Reset Token
- If target allows you to reuse the reset link then hunt for more reset link via `gau`, `wayback` or `urlscan.io`
<br>&nbsp;

### 4. Pre Account Takeover
- Signup using normal signup form as a hacker but hacker has no verification link.
- Then if victim signs up using oauth .
- Verification bypass now attacker can login the victim account without verification link with the password he entered while registering.
<br>&nbsp;

### 5. CORS Misconfiguration to Account Takeover
- Check api , any endpoint has access access token/session/secret/fingerprint
- If yes check for CORS misconfiguration does it allow us to fetch data from target?
- Make a payload to fetch data and replace headers and boom
<br>&nbsp;

### 6. CSRF to Account Takeover
- If profile modification in cookie based authentication doesn’t generate any token
- Open Account `A` change&Put email that you own click save intercept the request and generate a csrf poc.
- If fully cookie based auth then you dont have to modify anything send the csrf file to victim.
- If it requires UUID/UserID or unique token it becomes hard to do that but that doesn't mean it is secure , just start playing with target
- hint: password reset page helps many times for UUID/GUID and UserID
<br>&nbsp;

### 7. Host Header Injection
- Well in this case there are 4 ways do that.
- Click reset password change `host` header.
- Or change proxy header ex: `X-Forwarded-For: attacker.com`
- Or change `host`, `referrer`, `origin` headers at once as `attacker.com`
- Click reset then click resend mail and do all 3 methods above
<br>&nbsp;

### 8. Response Manipulation
1. code manipulation * to `200 OK`
2. code and body manipulation
code * to `200 OK`
body * to `{"success":true}` or `{}`
it works when json is being used to transfer and receive data.
<br>&nbsp;

