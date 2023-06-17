# Bugs to check on wordpress
- Data Exposure
- xmlrpc.php Enabled
- Using Wpscan

## Data exposure reports
https://hackerone.com/reports/356047
https://hackerone.com/reports/540301 
https://hackerone.com/reports/384782

### XMLRPC Enabled 
https://hackerone.com/reports/356047 
https://hackerone.com/reports/540301 
https://hackerone.com/reports/384782

# Not Securing wp-config.php WordPress Configuration File


## Findings
- It Discloses Author And Admin Information
```bash
example.com/wp-json/wp/v2/users/
$ curl https://example.com/\?_method\=GET -d rest_route=/wp/v2/users
```
