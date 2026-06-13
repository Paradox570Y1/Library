It is Object Relational Model
java/spring
JPA - Java Persistence API (easy to use)
Hibernate


- If i write native query in my SQL and open a connection (transaction) and send a query and then close the transaction. If it fails it rolls back otherwise a query's response is received.

### SQL Injection Attack
![[Pasted image 20260206210643.png|300]]
- With name hacker can send a delete script along with name which if not filtered will be executed.


JDBC 
- If we want to change the database technology then we need to modify whole code for that which is not the case with ORM.

ORM - handles all such issues
you just need to create entity and use hibernate and setup transaction manager etc. Creates and keeps predefined connection pool. It handles connection and sql connection etc.


Hibernate ORM benefits:
- Security
- Transaction manager
- Connection manager
- No need to know SQL queries, just write java code it will convert it automatically
- In POM file you need to configure which connection is that whether it is MySQL or SQL or postgre SQL, It will automatically convert the java code to that.