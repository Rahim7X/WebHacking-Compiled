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

### MASS Email Flooding Using Any Endpoint
- Any page that takes email as input and send any email
```bash
go to forgot password page add email 
Interceot Request
If Json data in being sent
Add multiple valid email parameter and valid emails
Now Send to intruder booom Flood
```
