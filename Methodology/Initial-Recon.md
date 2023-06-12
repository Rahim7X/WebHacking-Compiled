# Initial Recon

**NOTE : We are using geturls as gau and gf**

### Make a list of inscope assets and valid urls

```bash
*# Mass Testing On Entire Scope*
_______________________________

$ cat inscope.txt | assetfinder --subs-only | anew subdomains.txt 
$ cat inscope.txt | subfinder --subs-only | anew subdomains.txt
$ cat subdomains.txt | httpx | anew valid-domains.txt
$ amass enum -d domain.com 
$ cat  valid-domains.txt |waybackurls|  anew urls.txt
$ echo "subdomains.txt"| gau | anew urls.txt
$ cat urls.txt | grep ".js" | anew jsfiles.txt
$ mkdir scripts;redjs -f jsfiles.txt -o scripts
$ redjs -t scripts
$ cat urls.txt | gf <paramms>
*# Create Different Files For Different Paramns*
```

### Divide scope and do procedural testing

```bash
$ cat inscope.txt | assetfinder --subs-only | anew subdomains.txt 
$ cat subdomains.txt | httpx | anew valid-domains.txt
$ cat valid-domains.txt | sed -e 's/[^/]*\/\/\([^@]*@\)\?\([^:/]*\).*/\2/' | anew subdomains.txt
$ eyewitness -f valid-domains.txt
# Choose Intresting Domain And Test Further
$ mkdir domain1 && cd domain1
$ echo "domain1.com" | gau | urls.txt
$ echo "domain1.com" | waybackurls | anew urls.txt
$ gf urls.txt <param> # do further enum and create different files
```

### 

```bash
$ nuclei -l /path/to/list-of-targets.txt
# detect frameworks
$ subfinder -d targetdomain.com -silent | httpx | nuclei -t technologies/tech-detect.yaml
```

### Directory Fuzzing

```bash
$ ffuf -u https://example.com/FUZZ -w list.txt
$ Use Burp 403 Bypasser For 403 Bypass
```

## Github Dorking

```bash
"tesla.com" password
"tesla.com" secret
"tesla.com" credential
"tesla.com" token
"tesla.com" config
"tesla.com" key
"tesla.com" pass
"tesla.com" login
"tesla.com" pwd
"tesla.com" ftp
"tesla.com" ssh

"tesla.com" security_credentials
"tesla.com" connectionstring
"tesla.com" JDBC
"tesla.com" ssh2_auth_password
"tesla.com" send_keys or send,keys
GitHub Dorks for Finding Files
filename:manifest.xml
filename:travis.yml
filename:vim_settings.xml
filename:database
filename:prod.exs NOT prod.secret.exs
filename:prod.secret.exs
filename:.npmrc _auth
filename:.dockercfg auth
filename:WebServers.xml
filename:.bash_history <Domain name>
filename:sftp-config.json
filename:sftp.json path:.vscode
filename:secrets.yml password
filename:.esmtprc password
filename:passwd path:etc
filename:dbeaver-data-sources.xml
path:sites databases password
filename:config.php dbpasswd
filename:prod.secret.exs
filename:configuration.php JConfig password
filename:.sh_history
shodan_api_key language:python
filename:shadow path:etc
JEKYLL_GITHUB_TOKEN
filename:proftpdpasswd
filename:.pgpass
filename:idea14.key
filename:hub oauth_token
HEROKU_API_KEY language:json
HEROKU_API_KEY language:shell
SF_USERNAME salesforce
filename:.bash_profile aws
extension:json api.forecast.io
filename:.env MAIL_HOST=smtp.gmail.com
filename:wp-config.php
extension:sql mysql dump
filename:credentials aws_access_key_id
filename:id_rsa or filename:id_dsa
GitHub Dorks for Finding Languages
language:python username
language:php username
language:sql username
language:html password
language:perl password
language:shell username
language:java api
HOMEBREW_GITHUB_API_TOKEN language:shell
GiHub Dorks for Finding API Keys, Tokens and Passwords
api_key
“api keys”
authorization_bearer:
oauth
auth
authentication
client_secret
api_token:
“api token”
client_id
password
user_password
user_pass
passcode
client_secret
secret
password hash
OTP
user auth
GitHub Dorks for Finding Usernames
user:name (user:admin)
org:name (org:google type:users)
in:login (<username> in:login)
in:name (<username> in:name)
fullname:firstname lastname (fullname:<name> <surname>)
in:email (data in:email)
GitHub Dorks for Finding Information using Dates
created:<2012–04–05
created:>=2011–06–12
created:2016–02–07 location:iceland
created:2011–04–06..2013–01–14 <user> in:username
GitHub Dorks for Finding Information using Extension
extension:pem private
extension:ppk private
extension:sql mysql dump
extension:sql mysql dump password
extension:json api.forecast.io
extension:json mongolab.com
extension:yaml mongolab.com
[WFClient] Password= extension:ica
extension:avastlic “support.avast.com”
extension:json googleusercontent client_secret
grep.app

https://github.com/random-robbie/keywords/blob/master/keywords.txt 
```

## Check For Broken Links

```bash
$ blc -rof --filter-level 3 http://testphp.vulnweb.com
```

## Find Senstive Information using google dork

```bash
https://pentest-tools.com/information-gathering/google-hacking

```

### FUZZING

```bash
dirsearch.py -l target.txt -e php,asp,aspx,jsp,py,txt,conf,config,bak,backup,swp,old,db,sqlasp,aspx,aspx~,asp~,py,py~,rb,rb~,php,php~,bak,bkp,cache,cgi,conf,csv,html,inc,jar,js,json,jsp,jsp~,lock,log,rar,old,sql,sql.gz,sql.zip,sql.tar.gz,sql~,swp,swp~,tar,tar.bz2,tar.gz,txt,wadl,zip -i 200 — full-url
```

## Get Actual Ip SHodan

```bash
hostname:example.com
```

### Find github

```bash
site:github.com | site:gitlab.com "aseelapp.com"
```

### Finding Directory Listing Issues

```bash
Index:Index of /wp-admin
Index:Index of /wp-content/uploads

```

### Port Scanning

```bash
cat subd.txt | naabu -top-ports 1000 -o port-scan.txt
```
