### 1. **DDL (Data Definition Language)**

- **Full Form**: Data Definition Language
- **Explanation**: DDL is used to define the structure of the database, such as creating, altering, or dropping tables and other database objects.
- **Examples**:
    - `CREATE TABLE`: To create a new table.
    - `ALTER TABLE`: To modify an existing table structure.
    - `DROP TABLE`: To delete a table from the database.

### 2. **DML (Data Manipulation Language)**

- **Full Form**: Data Manipulation Language
- **Explanation**: DML is used to manipulate data stored in the database, such as retrieving, inserting, updating, and deleting data.
- **Examples**:
    - `SELECT`: To fetch data from the database.
    - `INSERT`: To add new data.
    - `UPDATE`: To modify existing data.
    - `DELETE`: To remove data from the database.

### 3. **DCL (Data Control Language)**

- **Full Form**: Data Control Language
- **Explanation**: DCL is used to control access to data in the database, granting or revoking permissions to users.
- **Examples**:
    - `GRANT`: To provide specific privileges to users.
    - `REVOKE`: To take back previously granted privileges.

### 4. **TCL (Transaction Control Language)**

- **Full Form**: Transaction Control Language
- **Explanation**: TCL is used to manage transactions in a database, ensuring data consistency.
- **Examples**:
    - `COMMIT`: To save changes made by a transaction permanently.
    - `ROLLBACK`: To undo changes made by a transaction.
    - `SAVEPOINT`: To set a point within a transaction to roll back to later.

### 5. **DRL (Data Retrieval Language)**

- **Full Form**: Data Retrieval Language
- **Explanation**: DRL is often considered part of DML and is specifically used to retrieve data from the database.
- **Example**:
    - `SELECT`: To query and fetch data from one or more tables.

### 6. **SDL (Storage Definition Language)**

- **Full Form**: Storage Definition Language
- **Explanation**: SDL defines the storage structure and access methods used in the database. It is more theoretical and not commonly implemented directly in modern systems.

### 7. **VDL (View Definition Language)**

- **Full Form**: View Definition Language
- **Explanation**: VDL is used to define user views or virtual tables in the database. It is usually implemented using the `CREATE VIEW` command.

### Summary Table:

| Term | Full Form                    | Purpose                                 | Example Command      |
| ---- | ---------------------------- | --------------------------------------- | -------------------- |
| DDL  | Data Definition Language     | Define database structure               | `CREATE`, `DROP`     |
| DML  | Data Manipulation Language   | Manipulate data in the database         | `INSERT`, `UPDATE`   |
| DCL  | Data Control Language        | Manage user permissions                 | `GRANT`, `REVOKE`    |
| TCL  | Transaction Control Language | Manage database transactions            | `COMMIT`, `ROLLBACK` |
| DRL  | Data Retrieval Language      | Retrieve data (subset of DML)           | `SELECT`             |
| SDL  | Storage Definition Language  | Define storage structures (theoretical) | -                    |
| VDL  | View Definition Language     | Define views in the database            | `CREATE VIEW`        |


---
----

----
----



### **1. GRANT Statement**

- **Purpose**: To give specific privileges to a user or role.
- **Syntax**:
    
    sql
    
    Copy code
    
    `GRANT privilege1, privilege2, ...  ON object_name  TO user_or_role  [WITH GRANT OPTION];`
    
- **Components**:
    - `privilege1, privilege2`: The privileges to be granted (e.g., `SELECT`, `INSERT`).
    - `object_name`: The database object (e.g., table, view) for which permissions are granted.
    - `user_or_role`: The user or role receiving the privileges.
    - `WITH GRANT OPTION`: Allows the user to further grant the same privileges to others.

#### **Example 1 (Granting Privileges to a User)**:

Grant `SELECT` and `INSERT` privileges on the `employees` table to user `john`:

sql

Copy code

`GRANT SELECT, INSERT  ON employees  TO john;`

#### **Example 2 (Granting Privileges with Grant Option)**:

Grant `SELECT` privilege on the `departments` table to user `jane`, allowing her to grant it to others:

sql

Copy code

`GRANT SELECT  ON departments  TO jane  WITH GRANT OPTION;`

---

### **2. REVOKE Statement**

- **Purpose**: To remove previously granted privileges from a user or role.
- **Syntax**:
    
    sql
    
    Copy code
    
    `REVOKE privilege1, privilege2, ...  ON object_name  FROM user_or_role;`
    
- **Components**:
    - `privilege1, privilege2`: The privileges to be revoked (e.g., `SELECT`, `INSERT`).
    - `object_name`: The database object (e.g., table, view) for which permissions are revoked.
    - `user_or_role`: The user or role losing the privileges.

#### **Example 1 (Revoking Privileges from a User)**:

Revoke `INSERT` privilege on the `employees` table from user `john`:

sql

Copy code

`REVOKE INSERT  ON employees  FROM john;`

#### **Example 2 (Revoking All Privileges)**:

Revoke all privileges on the `departments` table from user `jane`:

sql

Copy code

`REVOKE ALL PRIVILEGES  ON departments  FROM jane;`


---
----

---
----



### **1. Overview of Database**

A **database** is an organized collection of data that can be easily accessed, managed, and updated. It serves as a storage medium for various types of information, ranging from text to multimedia.

- **Key Features:**
    
    - **Data Organization:** Data is structured into tables, rows, and columns for easy management.
    - **Data Retrieval:** Efficient querying and retrieval mechanisms.
    - **Data Security:** Protects against unauthorized access.
    - **Persistent Storage:** Retains data over time, independent of program termination.
- **Examples:** Banking systems, e-commerce websites, and school management systems.
    

---

### **2. Database Management System (DBMS)**

A **DBMS** is a software system designed to interact with users, applications, and the database itself to store, retrieve, and manage data efficiently.

- **Functions of DBMS:**
    
    - **Data Storage and Retrieval:** Stores data in a structured format and provides tools for querying.
    - **Data Security:** Implements user access controls.
    - **Concurrency Control:** Allows multiple users to work simultaneously.
    - **Backup and Recovery:** Ensures data availability even after failures.
- **Advantages:**
    
    - Reduces data redundancy.
    - Enhances data integrity and security.
    - Provides data independence (discussed later).
- **Examples of DBMS:** MySQL, PostgreSQL, MongoDB, Oracle DB.
    

---

### **3. DBMS Architecture**

DBMS architecture defines how data is stored, accessed, and processed. The commonly used architecture is the **three-tier architecture**, which separates the system into three levels:

- **a. External Level (User View):**
    
    - Closest to the user.
    - Provides multiple user views tailored to individual user needs.
- **b. Conceptual Level:**
    
    - Provides a unified view of the entire database.
    - Defines logical structure and relationships.
- **c. Internal Level:**
    
    - Deals with the physical storage of data.
    - Manages file structures, indexing, and data compression.

This separation supports **data independence** and simplifies system management.

### **1. Single-Tier Architecture**

- Also known as the **monolithic architecture**, this is the simplest form of DBMS architecture.
- The database is directly accessible to the user.
- Both the application and database reside on the same system.

**Characteristics:**

- No abstraction; users interact directly with the database.
- Suitable for smaller systems where all functionalities are local.

**Example:** Personal database systems like Microsoft Access.

**Advantages:**

- Simple to implement and manage.
- Fast for single-user applications.

**Disadvantages:**

- Limited scalability and security.
- Not suitable for multi-user environments.

---

### **2. Two-Tier Architecture**

- This architecture separates the application and database layers.
- The **client tier** (user interface) communicates directly with the **server tier** (database).

**Components:**

- **Client:** Runs the application and sends queries to the database server.
- **Server:** Processes client requests, executes queries, and returns data.

**Examples:** MySQL with applications like Java or Python.

**Advantages:**

- Better security compared to single-tier.
- Reduces client-side workload as the server handles database queries.

**Disadvantages:**

- Scalability is limited when the number of clients increases.
- Tight coupling between client and server.

---

### **3. Three-Tier Architecture**

- This is the most commonly used architecture in modern DBMS.
- It adds a **middle layer (application server)** between the client and database server, enabling separation of concerns.

**Layers:**

1. **Presentation Layer (Client):**
    - User interface where users interact with the system.
    - Example: Web browsers, mobile apps.
2. **Application Layer (Middleware):**
    - Processes business logic, validates data, and interacts with the database.
    - Example: APIs or web servers.
3. **Database Layer (Server):**
    - Manages the actual storage, querying, and retrieval of data.

**Examples:** Web applications using Apache Server, PHP, and MySQL.

**Advantages:**

- Highly scalable and secure.
- Allows independent development and maintenance of layers.
- Enables distributed systems.

**Disadvantages:**

- More complex and costly to implement.
- Slightly slower due to additional communication between layers.

---

### **4. N-Tier Architecture**

- Extends the three-tier architecture by introducing additional layers for specialized tasks, such as caching, logging, or analytics.

**Usage:**

- Large-scale, enterprise-level applications.

**Advantages:**

- Enhanced flexibility, scalability, and fault tolerance.
- Easier to manage changes in individual layers.

**Disadvantages:**

- Increased complexity.
- Higher implementation and maintenance costs.

---

### **5. Centralized Architecture**

- All data is stored in a single centralized database.
- Users access the database from remote locations via terminals.

**Characteristics:**

- Suitable for organizations with a single data center.

**Advantages:**

- Easy to manage and secure.
- Low cost of maintenance.

**Disadvantages:**

- Single point of failure.
- Limited scalability and slower for remote users.

---

### **6. Distributed Database Architecture**

- Data is stored across multiple locations (servers) and accessed as a single logical database.
- Can be either **homogeneous** (same DBMS at all locations) or **heterogeneous** (different DBMS at different locations).

**Characteristics:**

- Data is fragmented, replicated, or partitioned across nodes.

**Examples:** Systems like Google Spanner, Cassandra.

**Advantages:**

- High availability and fault tolerance.
- Faster access due to proximity of data.

**Disadvantages:**

- Complexity in managing and synchronizing distributed data.
- Increased cost.

---

### **7. Parallel Database Architecture**

- Designed to execute queries and process data in parallel by using multiple processors.

**Components:**

- Shared-memory, shared-disk, or shared-nothing architectures.

**Advantages:**

- Improved performance for complex queries and large datasets.
- Scalable for massive workloads.

**Disadvantages:**

- Expensive infrastructure.
- Challenging to implement and maintain.

---

### **8. Cloud-Based Architecture**

- Databases hosted in the cloud are accessed via the internet.
- Offered as services like **DBaaS (Database-as-a-Service)**.

**Examples:** Amazon RDS, Google Cloud SQL, Azure SQL Database.

**Advantages:**

- High scalability and flexibility.
- No need for physical hardware.

**Disadvantages:**

- Dependent on network connectivity.
- Potential data privacy concerns.

---

### Summary of Key Architectures:

| Architecture | Key Features                      | Use Cases                       |
| ------------ | --------------------------------- | ------------------------------- |
| Single-Tier  | Local database access             | Small, personal applications    |
| Two-Tier     | Client-server model               | Small to medium applications    |
| Three-Tier   | Middleware layer for logic        | Web and enterprise applications |
| N-Tier       | Multi-layer architecture          | Complex, large-scale systems    |
| Centralized  | Single data center                | Small organizations             |
| Distributed  | Data stored across multiple sites | Global systems, cloud apps      |
| Parallel     | Multi-processor systems           | Data-intensive tasks            |
| Cloud-Based  | Hosted in the cloud               | Scalable, remote applications   |

---

### **4. Data Independence**

Data independence refers to the ability to modify the database schema at one level without affecting the schema at the next higher level.

- **Types of Data Independence:**
    
    - **Logical Data Independence:**
        - Ability to change the conceptual schema without altering external schemas.
        - Example: Adding a new column to a table without affecting user views.
    - **Physical Data Independence:**
        - Ability to change the physical storage without affecting the conceptual schema.
        - Example: Moving a database from one disk to another.
- **Importance:**
    
    - Simplifies database maintenance.
    - Enhances flexibility and scalability.

---

### **5. Integrity Constraints**

Integrity constraints ensure the accuracy and consistency of data in the database.

- **Types of Constraints:**
    
    - **Domain Constraints:** Define permissible values for attributes (e.g., age > 0).
    - **Entity Integrity:** Ensures that each table has a primary key, and its value is unique and not null.
    - **Referential Integrity:** Maintains relationships between tables using foreign keys.
    - **Unique Constraints:** Ensures that specific attributes have unique values.
    - **Check Constraints:** Validates data entered into the database (e.g., salary >= 10000).
- **Benefits:**
    
    - Maintains data quality.
    - Prevents invalid data entry.
![[Pasted image 20241002193605.png|400]]
- Using Foreign key here branch_id
- Foreign key is primary key of another table
![[Pasted image 20241002193747.png|400]]

### Supervisor ID
![[Pasted image 20241002194016.png|400]]
- tells emp 100 is supervisor of emp 101 and 102

### Composite ID
![[Pasted image 20241002194418.png|280]]

![[Pasted image 20241002195304.png]]
