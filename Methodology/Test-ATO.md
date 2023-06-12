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

### IDOR to ATO
- Change Email To Anyone Else WHen Resetting The Password
- Chnage UID to reset another user's passweord

### Parameter Pollution
- Add Two Email In Same Request
- CHange Email Order
- Provide list of email

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
