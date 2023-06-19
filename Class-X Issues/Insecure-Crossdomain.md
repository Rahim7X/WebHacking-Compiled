# Insecure Crossdomain
It is a vulnerbility caused by misconfiguration in website. Which can lead to perform remote request and responses

## Example example.com/crossdomain.xml
```bash
<cross-domain-policy>
    <site-control permitted-cross-domain-policies="by-content-type"/>
    <allow-access-from domain="*" secure="false"/>
    <allow-http-request-headers-from domain="*" headers="*"/>
</cross-domain-policy>
```
- There all sites are allows for cross domain actions
- [Report 1](https://hackerone.com/reports/43070)
- [Report 2](https://hackerone.com/reports/105463)
- [Report 3](https://hackerone.com/reports/96662)
