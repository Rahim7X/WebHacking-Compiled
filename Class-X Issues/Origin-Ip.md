# Shodan
```bash
hostname:test.com
```

# security trails
- old dns records revealing the ip address

# Cynses
```bash
https://censys.io/ipv4?q=example.com
```

# Through Error
```bash
Open request page of (graphql2.trint.com) with "getUser" Operation name.
Remove "authorization: Bearer" line and error will raise.
You can see ("ip":"::ffff:10.6.127.182) and ("data":{"user":null}) in error. It is happening only on "getUser" operation name.
```
# Impact
- Unfiltered Payload Processing
- Waf Bypass
- Potential Dos


# Reports
- [Report 1](https://hackerone.com/reports/687908)
- [Report 2](https://hackerone.com/reports/1637577)
- [Report 3](https://hackerone.com/reports/1536299)
- [Report 4](https://hackerone.com/reports/1327443)
- [Report 5](https://hackerone.com/reports/360825)
- [Report 6](https://hackerone.com/reports/1105673)
- [Report 7](https://hackerone.com/reports/315838)

