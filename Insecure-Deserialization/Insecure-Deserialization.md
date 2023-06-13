# Insecure Deserialization
Serialization is used to store a state of an object in bytecode. So it can be used again
The Insecure Deserialization occures when the object values are not checked.

# How to identify serilized data
- in php
```bash
Raw Data : 
$user->name = "carlos";
$user->isLoggedIn = true;

Serilized Data : 
O:4:"User":2:{s:4:"name":s:6:"carlos"; s:10:"isLoggedIn":b:1;}
```

-in Java
```bash
It uses binary serialization format. This is more difficult to read
The Hava objects always begin with same bytes which are encoded as 

in hexadecimal:
ac
ed


In base 64:
r00
```


https://portswigger.net/web-security/deserialization/exploiting#how-to-identify-insecure-deserialization

