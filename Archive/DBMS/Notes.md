### Database
- Collection of related data.
- Types of data:
	- Structured - They generally uses RDBMS for its structure. Used by IRCTC , University.
	- Unstructured - Collection of photos, videos , chats etc. Used on Webpages.

> 90% of Worlds Data is Structured.

- Operations are performed after storing the data on server. User will fetch the data and and can insert new data, modify data or delete old data. These are the 3 basic `operations` performed on the database. To do these operations we require DBMS. 
- DBMS provides an interface to perform these operations like database creation, storing data in it, updating data, creating a table in the database and a lot more.
- DBMS also provides protection and security to the database. In the case of multiple users, it also maintains data consistency.

**DBMS allows users the following tasks:**

- **Data Definition:** It is used for creation, modification, and removal of definition that defines the organization of data in the database.
- **Data Updation:** It is used for the insertion, modification, and deletion of the actual data in the database.
- **Data Retrieval:** It is used to retrieve the data from the database which can be used by applications for various purposes.
- **User Administration:** It is used for registering and monitoring users, maintain data integrity, enforcing data security, dealing with [[Concurrency control|concurrency control]] monitoring performance and recovering information corrupted by unexpected failure.

> Data is stored in table form or relation form.

[All about database](https://www.javatpoint.com/what-is-database)
### DBMS (Data Base Management System)

Database management System is software which is used to store and retrieve the database. For example, Oracle, MySQL, etc.; these are some popular DBMS tools.

- DBMS provides the interface to perform the various operations like creation, deletion, modification, etc.
- DBMS allows the user to create their databases as per their requirement.
- DBMS accepts the request from the application and provides specific data through the operating system.
- DBMS contains the group of programs which acts according to the user instruction.
- It provides security to the database.
###### Types of DBMS Software
1. SQL Server by Microsoft
2. Oracle by Oracle Corporation (version 9i,11,12c etc.)
3. MySQL by Oracle Corporation
4. DB2 by IBM
###### Advantage of DBMS

**Controls redundancy**

It stores all the data in a single database file, so it can control data redundancy.

**Data sharing**
An authorized user can share the data among multiple users.

**Backup**
It providesBackup and recovery subsystem. This recovery system creates automatic data from system failure and restores data if required.

**Multiple user interfaces**
It provides a different type of user interfaces like GUI, application interfaces.

###### Disadvantage of DBMS

**Size**
It occupies large disk space and large memory to run efficiently.

**Cost**
DBMS requires a high-speed data processor and larger memory to run DBMS software, so it is costly.

**Complexity**
DBMS creates additional complexity and requirements.

### RDBMS (Relational Database Management System)
RDBMS is system in which we can perform various operations like INSERT, UPDATE, DELETE on **Relations**.

The word RDBMS is termed as 'Relational Database Management System.' It is represented as a table that contains rows and column.

RDBMS is based on the Relational model; it was introduced by E. F. Codd.

**A relational database contains the following components:**

- Table
- Record/ Tuple
- Field/Column name /Attribute
- Instance
- Schema
- Keys

An RDBMS is a tabular DBMS that maintains the security, integrity, accuracy, and consistency of the data.
>The instance is a table with rows or columns
>Schema specifies the structure like name of the relation, type of each column and name.

