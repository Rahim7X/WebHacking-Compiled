# Server Side Request Forgery
- In this type of attack attacker controls a url which server sends a request 
to fetch information

## Basic SSRF against the local server
- Lab uses stock check feature where it fetches stock number from a api url
- We changed that url to https://localhost/admin

## Basic SSRF against another back-end system
- Lab uses http://ip:port/checkstock to check stock
- I scanned entire ip range using intruder
- Found http://192.168.159.151/admin is accesable

## SSRF with blacklist based protection
- Site is detecting 127.0.0.1 , localhost, admin using regex
- Changed 127.0.0.1 to 127.1
- changed admin to %25%36%31dmin

## SSRF with filter bypass via open redirection vulnerability
- Found open redirect bug and server follows redirecct 
- bypassed using /redirect=localhost/admin

## SSRF With Whitelist based input filter
- http://localhost:80%2523@stock.weliketoshop.net/admin/delete?username=carlos


