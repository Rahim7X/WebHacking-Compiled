# Information Disclosure
Information disclosure is when attack can see any data from target assets
which is unintentional. The Impact is judge by the type of data which is disclosure
It is also reffered as Data Leakage.

### Such As 
- Data about other users
- Senstive commercial or business data
- Technical detials about the website and infrastructure

### Some Examples
- Revealing the name of hidden folders and files
- Can see backend sourcecode
- Database column names and table name in error messages
- Exposing high senstive information without need
- Hard-coding api keys

### Common sources of information disclosure

- Files for web crawlers
- Directory listings
- Developer comments 
- Error messages 
- Debugging data 
- User account pages 
- Backup files 
- Insecure configuration 
- Version control history (.git)

### Some Common Functions
- Leaking APIs
A leaking API is when a functioning-as-intended API, returns too much information.
- Dorking
Dorking for information is by far my personal favourite method.
Git Dork : postgress://username:password@subdomain
- Work Less
If you find any framework / endpoint low hanging bug then crrate a nuclei template
- Accidentally Public
Source Code, JS Files, API Keys, Crendetials
Meta Data Of Downloaded Image
- Directory Fuzzing (.json,.git)
- API ABuse
IDOR , SQLi

###Perils of Spring Boot Actuators Misconfiguration
- Endpoints
```bash
/heapdump
/threadump 
/trace 
/logfile
/shutdown
/mappings
/env
/restart
/health
/prometheus
/auditevents
/beans
/caches
/conditions
/configprops
/flyway
/httpexchanges
/integrationgraph
/liquibase
/scheduledtasks
/threaddump
/sessions
/quartz
/mappings
/metrics
```
### LAB
#### Information disclosure in error messages
```bash
To solve the lab, obtain and submit the version number of this framework. 
Just added ' in end of url
https://0ad000fa0353934f80c64ac500750045.web-security-academy.net/product?productId=13'
```

#### Information disclosure on debug page
```bash
Found a comment in souce code
<!-- <a href=/cgi-bin/phpinfo.php>Debug</a> -->
```

#### Source code disclosure via backup files
```bash
/robots.txt leaked backup endpoint which disclosed source code
```

#### Authentication bypass via information disclosure
```bash
# Admin Interface Is Only Available To Local Users
Intercept Request Then Add
X-Custom-Ip-Authorization: 127.0.0.1
```

####  Information disclosure in version control history
```bash
.git exposed

```

#### Password Reset Token Leakage In Referer Header
```bash
I have found that if user open the link of reset password and than click on any external
links within the reset password page its leak password reset token in referer header.
```


### Insecure Local Data Storage
```bash
Righclick Inspect
Click Storage / Or Application/Storage
CHeck all values and data 


```

### Try To Access
```bash
example.com/phpmyadmin/setup
example.com/phpmyadmin/setup.php
example.com/phpMyAdmin/setup/index.php
```
