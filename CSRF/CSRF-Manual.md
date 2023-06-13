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
