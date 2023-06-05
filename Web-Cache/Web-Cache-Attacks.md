# Web Cache Poisioning

lab [https://poison.digi.ninja/](https://poison.digi.ninja/)

## Cache

static files were served by cache to reduce load from server

## Cache Keys

This is the key if matches in request then the same cache will be server to all users

- Host
- Request Line

### Goal

Let the cache server to cache harmful response and serve to users
Using This Method We Can Cache Our Own Response And All Users Will See That Unit The Cache Expires

### Keyed Input and unkeyed input

Keyed input matches in request then the same response will be served

So alway inject payload in unkeyed input

**Etag :**

It is a tag that is get to a perticular resource in cache server unique for each cache resource 

if-not-match: payload —> This can overwrite the cache

### How To Detect Keyed And Unkeyed Input
- Rightclick Request IN Burp -> Extensions -> Paraminer -> Guess Headers

### LABS
#### Web cache poisoning with an unkeyed header
- Intercept HomePage In Burp
- Rightclick Request IN Burp -> Extensions -> Paraminer -> Guess Headers
- Send Request Coluple Of Times
- Found 1 Header X-Forwarded-Host:
- inject payload in it

#### Web cache poisoning with an unkeyed cookie
- 1 element from cookei was displayed inside script tag
- inserted fehost="}alert(1)%3b{</script><img src=x onerror="alert(1)"/> in cookie
- Page was cached and displayed to everyone

#### Web cache poisoning with multiple headers
- Paraminer Output X-Forwarded-Scheme
- add X-Forwarded-Scheme: nothttps
- Also X-Forwarded-Host: example.com

#### Targeted web cache poisoning using an unknown header
- 
