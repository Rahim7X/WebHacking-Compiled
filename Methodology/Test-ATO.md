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
