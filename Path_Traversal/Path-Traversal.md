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

