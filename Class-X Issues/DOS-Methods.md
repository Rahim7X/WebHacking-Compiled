# No Length In Password Leads Do Dos
- If there is no captcha in login , signup 

# Pixel Flood Attack
- If site is deterimining the size of the image by exif data before processing it. 
- It works like this : pixel 5x5 : App will allocate 25 bytes in memory
- Now uploaded edited pixel image now it crashes before processing
use [lottapixel.jpg ]()

- [Report 1 ](https://hackerone.com/reports/390)
- [Report 2 ](https://hackerone.com/reports/764434)

# Cookie Bomb
- If userinput is stored in cookie somehow 
- Add Long String
```bash
https://target.com/index.php?param1=xxxxxxxxxxxxxx
```
- After input “xxxxxxxxxxxxxx” as a value of param1, check your cookies. If there is cookies the value is “xxxxxxxxxxxxxxxxxxxxxx” it means the website is vulnerable


## DOST Reports

```bash
Title: DoS: type confusion in mrb_no_method_error
Company: shopify-scripts
Bounty: $20.000
Link: https://hackerone.com/reports/181871
```

```bash
Title: Use after free vulnerability in mruby Array#to_h causing DOS possible RCE
Company: shopify-scripts
Bounty: $20.000
Link: https://hackerone.com/reports/181321
```

```bash
Title: Range constructor type confusion DoS
Company: shopify-scripts
Bounty: $10.000
Link: https://hackerone.com/reports/181910
```

```bash
Title: DoS on PayPal via web cache poisoning
Company: PayPal
Bounty: $9.700
Link: https://hackerone.com/reports/622122
```

```bash
Title: Null target_class DoS
Company: shopify-scripts
Bounty: $8.000
Link: https://hackerone.com/reports/183405
```

```bash
Title: Denial of Service in mruby due to null pointer dereference
Company: shopify-scripts
Bounty: $8.000
Link: https://hackerone.com/reports/181232
```

```bash
Title: ruby DoS https://www.mruby.science
Company: shopify-scripts
Bounty: $8.000
Link: https://hackerone.com/reports/180695
```

```bash
Title: DoS through PeerExplorer
Company: IOVLabs
Bounty: $4.000
Link: https://hackerone.com/reports/363636
```

```bash
Title: DoS on the Issue page by exploiting Mermaid.
Company: GitLab
Bounty: $3.000
Link: https://hackerone.com/reports/470067
```

```bash
Title: profile-picture name parameter with large value lead to DoS for other users and programs on the platform
Company: HackerOne
Bounty: $2.500
Link: https://hackerone.com/reports/764434
```

```bash
Title: Denial of service via cache poisoning
Company: HackerOne
Bounty: $2.500
Link: https://hackerone.com/reports/409370
```

```bash
Title: Uploading large payload on domain instructions causes server-side DoS
Company: HackerOne
Bounty: $2.500
Link: https://hackerone.com/reports/887321
```

```bash
Title: ActiveStorage throws exception when using whitespace as filename, may lead to denial of service of multiple pages
Company: HackerOne
Bounty: $2.500
Link: https://hackerone.com/reports/713407
```

```bash
Title: Authorization issue in Google G Suite allows DoS through HTTP redirect
Company: Uber
Bounty: $2.500
Link: https://hackerone.com/reports/191196
```

```bash
Title: [Java] CWE-755: Query to detect Local Android DoS caused by NFE
Company: GitHub Security Lab
Bounty: $1.800
Link: https://hackerone.com/reports/1061211
```

```bash
Title: Denial of Service in Action Pack Exception Handling
Company: Ruby on Rails
Bounty: $1.500
Link: https://hackerone.com/reports/42797
```

```bash
Title: Specially constructed multi-part requests cause multi-second response times; vulnerable to DoS
Company: Ruby on Rails
Bounty: $1.500
Link: https://hackerone.com/reports/431561
```

```bash
Title: DOS in stream filters
Company: PHP (IBB)
Bounty: $1.500
Link: https://hackerone.com/reports/505278
```

```bash
Title: Arbitrary file creation with semi-controlled content (leads to DoS, EoP and others) at Steam Windows Client
Company: Valve
Bounty: $1.250
Link: https://hackerone.com/reports/682774
```

```bash
Title: Denial of Service | twitter.com & mobile.twitter.com
Company: Twitter
Bounty: $1.120
Link: https://hackerone.com/reports/903740
```

```bash
Title: a very long name in hey.com can prevent anyone from accessing their contacts and probably can cause denial of service
Company: Basecamp
Bounty: $1.000
Link: https://hackerone.com/reports/1018037
```

```bash
Title: No redirect_uri in the db for web-internal clientKey leads to one-click DoS on gitter.im
Company: GitLab
Bounty: $1.000
Link: https://hackerone.com/reports/702987
```

```bash
Title: SSRF / Local file enumeration / DoS due to improper handling of certain file formats by ffmpeg
Company: Imgur
Bounty: $1.000
Link: https://hackerone.com/reports/115978
```

```bash
Title: DoS attack via comment on Issue
Company: GitLab
Bounty: $1.000
Link: https://hackerone.com/reports/557154
```


```bash
Title: Fastify denial-of-service vulnerability with large JSON payloads
Company: Node.js third-party modules
Bounty: $500
Link: https://hackerone.com/reports/303632
```
