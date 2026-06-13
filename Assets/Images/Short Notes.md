# Maven

- it is a build tool and do bundling for you.
- manifest file, .jar file, main class, all these files you have to organize and create a zip file is automatically handled by Maven.
- It creates pom file has build instructions in xml format , which can be used to decide which profile to use in it.
- dependency version control can be specified.

![[Pasted image 20260206205058.png|300]]
.m2 file has settings.xml

New Jar required info
<com.spring.xyz>
<.spring>
<1.2>  // version

Repository -> com -> sp2 -> xyz  -> version 1.2
automatically works on lib folder
![[Pasted image 20260206205313.png|300]]
- Do not download jar file again if it is in directory.

It does:
- Versioning
- dependency management
- build tool
- test tool
- profile management


# Gradle

- It is advanced tool and under the hood make use of maven
- It is light weight and builds faster
- It uses XML layout.
- The file you touch it makes jar for that file only , hence it is faster.
- It has a watcher on your workspace.
- Maven always picks all files make complete build again that's why gradle is made.



# ORM

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

# Rest API

Spring - singleton
dependency injection - If a service is changed somehow then Spring will automatically handle the changes where ever the service was getting used to perform any task as Spring knows how to build the service.
AOP
Inversion of Control (IC) - Spring container has all control of object creation, object deletion, dependency management etc.

![[Pasted image 20260206212021.png]]

what spring boot is to spring , JT is to hibernate.

Spring feature
@aspert
pointcut before after

SpringBoot feature
introduced annotation
writes boiler plate code for you
tomcat or jackery is embedded in it
it's dependency management is better
provides you UI to use it
![[Pasted image 20260206212328.png|300]]

@Rest Controller
@Service Controller
@ Repository
aspect and token stuff

![[Pasted image 20260206212903.png|300]]

