
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

