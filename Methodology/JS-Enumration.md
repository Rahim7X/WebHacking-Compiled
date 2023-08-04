# JavaScript Enumration Complete Guide
Now a days websites use different frameworks and api's which require external client side interaction and all. There is a high possibility that we can find senstive information through javascript

## How to download and save javascript files
```bash
redjs -u http://example.com -o ./scripts -v
cat wayback_links.txt | grep -E "\.js$" | anew jsurl.txt
cat gau_url.txt | grep -E "\.js$" | anew jsurl.txt
redjs -f jsurl.txt -o ./scripts -v 
```

### How to look for senstive information 
```bash
nuclei -l jsurl.txt -t ~/nuclei-templates/exposures/ -o js_exposures_results.txt
redjs -t ./scrpts | grep "Found"
grep -r -E "aws_access_key|aws_secret_key|api key|passwd|pwd|heroku|slack|firebase|swagger|aws_secret_key|aws key|password|ftp password|jdbc|db|sql|secret jet|config|admin|pwd|json|gcp|htaccess|.env|ssh key|.git|access key|secret token|oauth_token|oauth_token_secret" /path/to/directory/*.js

```

### GTM id exposed in javascrip
check it on google tag manager for PII
