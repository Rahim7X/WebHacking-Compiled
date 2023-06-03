### No XSS But TBI

- Found A Parameter That Reflects User Input
```bash
https://app.example.com/API/Public/Login/HasCustomSAML/web?callback=text
https://app.clicktime.com/API/Public/Login/HasCustomSAML/web?callback=clicktime.com__has__been__moved_to::[attacker.com]
```

