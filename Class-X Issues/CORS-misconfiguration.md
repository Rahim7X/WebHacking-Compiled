# CORS stands for Cross Origin Resource Sharing
- By default the web protocol is allowed to make request from 1 domain to another domain.
They can't read responses.

## Dynamic WebApps
- Dynamic WebApps need get response from different subdomain or payment gateway , analytics page, APi etc.
In order to read response from different domain the thirdparty domain should have
```bash
Access-Control-Allow-Origin: Webap.com
```
This header in place

- It can also fetch account related informations such as score, balance,privilege but to get access from authenticated page
It should have this header
```bash
Access-Control-Allow-Credentials: True
```

# Rules Of CORS protocol
- There are 3 methods supported by CORS
```bash
Access-Control-Allow-Origin: onlyonedomain.com
Access-Control-Allow-Origin: *
Access-Control-Allow-Origin: null
```
- Note if it is set to */wildcard The
```bash
Access-Control-Allow-Credentials: True
```
- It will not work for security reasobs

# Where is the vulnerbility
- Since only single domain is allowd to be in Access-Control-Allow-Origin Header. The modern web app uses dynamic generation of hostnames to put in headers in each request.
- So it uses regex for allowing multiple domains to access resources.

# Bugs to check
- add origin as null
- use suffix or prifix of allowd domain to check
- try other ways to bypass regex

### Resources
- [Report 1](https://hackerone.com/reports/426165)
- [Report 2](https://hackerone.com/reports/470298)
-[Writeup](http://blog.portswigger.net/2016/10/exploiting-cors-misconfigurations-for.html)
