# Cross Site Request Forgery
It happens when a webserver processes a request based on session and fails to validate.
If the request is not forged

## CSRF Checklist
- Remove Header Based Tokens
- Manipulate Token In Request Body
- Use same csrf token for different accounts
- Replace token with a different value
- Change Request method
- Append _method for PUT/PATCH requests
- Check alternative content type
- Remove referer
- Steal CSRF Token using XSS
- Bypass Json based CSRF protection

## CSRF vulnerability with no defenses
#### CSRF no defence just content type application / json is checked
- CSRF bypass using flash file + 307 redirect method at plugins endpoint
ShuttlerTech
```bash
login to your account at https://my.xyz.email
visit https://thehackerblog.com/crossdomain/
use this link as php redirector https://testingsubdomain.000webhostapp.com/stripo.php
in the request headers : Content-Type: application/json;charset=UTF-8
the payload
code:

{“email”:”attacker@example.com”,”name”:”csrf poc”,”webUrl”:”csrf poc “}
```
1. [Writeup](https://jjainam16.medium.com/csrf-bypass-using-flash-file-307-redirect-method-at-plugins-endpoint-dcd217a5d701)
