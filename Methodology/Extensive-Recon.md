# Recon
- Horizontal Correlation 
- Vertical Correlation
- FIngerprinting
- Content Discovery 


## Horizontal Correlation 
- The process of finding different domains owned by the same organisation
- It is the first step of recon process

### Methods to find root domains
- The WHOIS Method
- The CIDR and ASN Method
- Google Dorks
- Researching Subsidiaries and Acquisitions

#### The WHOIS Method
- Target : domain.com
- Find The Email that registered domain.com
```bash
whois domain.com
```
Found wiener@emial.com
- Use reverse whois service, Such as [ViewDNS](https://viewdns.info/reversewhois/)
Now you can see wiener@emial.com also registered secretdomain.com and personaldomain.com

#### CIDRs and ASNs Method
- Classless Inter Domain Routing (CIDR) is a range of IP belong to a company
EG : 127.0.0.0/24
- Autonomous System Number (ASN) is a collection id that is used to reference list of CIDRs
ASN : 12345 
Can contain lots of CIDR ranges

- How to detect company is using ASN
dig command on different subdomains to check what their
```bash
dig a subdomain.domain.com +short
```
- If lots of the subdomains are consistent with their ASN, we could assume that they own their own ASN.
- Find IP's from ASN [BGPview](https://bgpview.io/)

#### Google Dorking
- Go to known target page
- Find something that would be common to all domains.
- copyright line in the footer,  Term’s and Conditions
- “©2021 imaginaryCompany All rights
- intext:”©2021 imaginaryCompany All rights reserved.”
BONUS TIP: If you’re hacking a target that owns a top level domain such as .gov or .mil, you can use the site:*.tld dork to find all the domains google has indexed. Eg, site:*.gov

#### Subsidiaries and Acquisitions
A Subsidiary Company is a company owned by a holding company. You may have heard of this in terms of a “Parent company” and “Child companies”
If the scope of your target is very broad, it may include subsidiary companies. We can use google, other search engines, or specific sites in order to find these.
Example: If we google “Yahoo subsidiaries” we see there is a child company names “Flurry”. This has expanded our target surface. (Always refer to the scope of engagement before pentesting a new asset).
An Acquisition is when a Company buys another company. This new company may also be included in the scope of the program.
Similarly to the subsidiary, we can use OSINT skills for acquisitions of a company to find new domains.


## Vertical Correlation
The process of finding subdomains from a root domain.

### Methods
- BruteForce
- Abusing transparency : crt.sh
- OSINT skills
- Existing Database

We Know More From SUbdomain ENumration cheatsheet by intigrity

#### BruteForce
- Best Subdomain Bruteforce Tool Amass
```bash
amass enum -df rootdomains.txt -max-dns-queries 100 -w subdomains.txt -o foundSubdomains.txt
```
Use Seclist 1 million subdomain list

#### Crt.sh
I know how to do it
### Google Dork 
Manual is best
[Find Sub From Github Codes](https://github.com/gwen001/github-search/blob/master/github-subdomains.py)


#### Exisiting Dataase
[DNS Dumper](https://dnsdumpster.com/)

#### Use ALTdns tool


## Best Wordlist Site
https://wordlists.assetnote.io/
Search sub download subd wordlist


## Fingerprinting
Finding and Indexing Services and Technologies used by your target.

Example: if our target is domain Inc, how do we find out there is a vulnerable or soon-to-be exploitable service running somewhere on their infrastructure?

### It Includes
- Open Ports
- Fingerprinting WebApps
- Indexing

#### Open Ports
GOAL : First Create A Curated IP List Of Target And Scan
```bash
httpx -l subdomains.txt -p 22,25,80,443,3306 -probe
````

- Shodan 
org:filter is used to find assets from an orgnisation name
net: filter, which is used to get assets from CIDR ranges
ssl: filter, which is used to get assets from an orgnisation name

- Censys

NOTE : These are not free and furstrating 
Solution MASSSCAN

- Masscan
```bash
sudo masscan -p<port num> <CIDR Range here> --exclude <Exclude IP> --banners -oX <Out File Name>
```

#### Fingerprinting Web Apps
- wapplyzer extension
- whatweb

#### Firewall Fingerprinting and Bypassing  
- Use [HackOriginFinder](https://github.com/hakluke/hakoriginfinder) to find real ip of host
# WAF (Real pain)
Most amateur bug hunters will throw <img src=x onerror=alert(1)> into an a reflected input field, look at the dreaded &lt; and &gt; in the source code, noticing it has been filtered, and then give up. But you can go further.
WAFs (firewalls) will block many payloads, but not all…

If we know the WAF, we can know a bypass! So it’s important to fingerprint, and record, which sites use which WAFs.

##### Bypass WAF
[Introducing wafw00f](https://github.com/EnableSecurity/wafw00f)
it is a command line tool which automatically tries to detect which firewall is in use.

#### Awesome-WAF
[Awesome WAF](https://github.com/0xInfection/Awesome-WAF#known-bypasses)

The Awesome-WAF repository has lots of amazing information, including WAF Bypasses for:

- SQL injection
- XSS (Stored and Reflected)
- HTML Injection
- Username Enumeration
- RCE
- XXE


## Content Discovery
The process of finding endpoints; URLs, Parameters and Resources

### Methods
- Active Discovery — Brute Force (the right way) and Self Crawling.
- Passive Discovery — Common Crawl, WayBackMachine, Existing databases, and More.
- Manual Discovery — Google Dorking, Aquatone.
- Essential Utility Tools

#### Active Discovery
- Manually Browse Target And Functions
- Fexobuster Best | Gobuster slow 
url : https://github.com/epi052/feroxbuster

- Meg
Another thing most hunter’s overlook: websites don’t like being spammed with requests.
Meg will take two parameters, a list of domains to h̶a̶r̶a̶s̶s̶ test, and a wordlist of url paths (or just one). It will then try every domain against one entry from the wordlist

- Self Crawling
[hakrawler](https://github.com/hakluke/hakrawler)

### Passive Discovery
- Gau | It user common crawl datesheet
- WayBackurls | It uses wayback datesheet
- Google Dorks | you know
- Take ScreenShort of all url and subdomain eyewitness and aquatone
- Url Enumeration — Subset of Content Discovery: finding existing endpoints.
- [gauplus Faster than gau much much much](https://github.com/bp0lr/gauplus)

### Harnessing The Potential Of Gauplus
```bash
cat allsub.txt | gauplus -subs | grep -i "\.xlsx" allurl.txt | anew xlsx.txt
cat allsub.txt | gauplus -subs | grep -i "\.sql" allurl.txt | anew sql.txt
cat allsub.txt | gauplus -subs | grep -i "\.log" allurl.txt | anew log.txt
cat allsub.txt | gauplus -subs | grep -i "\.git" allurl.txt | anew git.txt
cat allsub.txt | gauplus -subs | grep -i "\.bak" allurl.txt | anew bak.txt
```

#### Low hanging fruits one liner
```bash
cat allsub.txt | gauplus -subs | grep "=" | Gxss -c 100 | anew reflected.txt
cat allsub.txt | gauplus -subs | grep "=" > url.txt;httpx-l url.txt -path "/////../../../../../../../../etc/passwd" -status-code -mc 200 -ms 'root:'
cat allsubs.txt | gauplus -subs | qsreplace "burp.collan" | httpx
```

```bash
#### High hanging fruits one liner
cat allsub.txt | gauplus -subs | httpx -sc -nc | grep "403\|401" | anew unauthed.txt
cat allsub.txt | gauplus -subs | httpx -title | grep -i "admin\|login\|dashboard" | anew loginpanel.txt
```

### Take ScreenShots
```bash
httpx -l liveDomains.txt -srd subsScreens -ss
```
### Filter working urls
```bash
cat target.txt  | waybackurls | httpx -mc 200 -ct | grep application/json | tee json-data
### Downloading The Source Code Of Subdomains
```bash
$ cat subd.txt | aquatone
$ cat subd.txt | fff -d 1 -S -o scode
```

