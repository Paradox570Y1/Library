
# SQL commands
- create database db_name; -> to create a database
- use db_name; -> to use the db.
- select \*from sys.databases; -> to see all  databases.
![[Pasted image 20240709145508.png]]
- select \*from emp; -> To see the created table
	![[Pasted image 20240709144323.png]]
	![[Pasted image 20240709144334.png]]
	![[Pasted image 20240709150138.png|300]]
	
#### char vs varchar
- CHAR(10) -> It allocates resources to all 10 blocks.
- VARCHAR(10) -> It allocates resources based on the size of input if we input only 3 characters then it will only occupy 3 blocks.

---

```sql
CREATE DATABASE XYZ;
USE XYZ;
CREATE TABLE  Employee(
	id INT PRIMARY KEY,
	name VARCHAR(30),
	salary INT
);
-- MS SQL uses single quote for string while mySQL uses double quotes
INSERT INTO Employee (id,name,salary) 
VALUES 
(1,'adam',25000),
(2,'bob',30000),
(3,'casey',40000);

SELECT *FROM Employee;
```

![[Pasted image 20241106181440.png|400]]
![[Pasted image 20241106181841.png|400]]
![[Pasted image 20241106181856.png|400]]

```sql
SELECT * FROM table_name;
SELECT col1,col2 FROM table_name;
SELECT DISTINCT city FROM table_name;
```

![[Pasted image 20241106182401.png|400]]

![[Pasted image 20241106182444.png|400]]
![[Pasted image 20241106182541.png|400]]

![[Pasted image 20241106182825.png|400]]
```sql
--for MySQL
SELECT * FROM table_name LIMIT 5;
--for SQL Server
SELECT TOP 5 * FROM table_name;
```
![[Pasted image 20241106183036.png|150]]

![[Pasted image 20241106183107.png|400]]
![[Pasted image 20241106183250.png|200]]
![[Pasted image 20241106183406.png|400]]
![[Pasted image 20241106183521.png|400]]

![[Pasted image 20241106202005.png|400]]
```sql
CREATE TABLE customer(
customer_id INT,
customer VARCHAR(20),
mode VARCHAR(20),
city VARCHAR(20));

INSERT INTO customer (customer_id,customer,mode,city)
VALUES
(101,'Olivia Barrett','Netbanking','Portland'),
(102,'Ethan Sinclair','Credit Card','Miami'),
(103,'Maya Hernandez','Credit Card','Seattle'),
(104,'Liam Donovan','Netbanking','Denver'),
(105,'Sophia Nguyen','Credit Card','New Orleans'),
(106,'Caleb Foster','Debit Card','Minneapolis'),
(107,'Ava Patel','Debit Card','Phoenix'),
(108,'Lucas Carter','Netbanking','Boston'),
(109,'Isabella Martinez','Netbanking','Nashville'),
(110,'Jackson Brooks','Credit Card','Boston');


SELECT mode,COUNT(customer_id) AS Total_payments
FROM customer
GROUP BY mode;
```
![[Pasted image 20241106202021.png]]

![[Pasted image 20241106202115.png|400]]
> Use Having Clause when applying condition on group rather than a row.

![[Pasted image 20241106202407.png|200]]

![[Pasted image 20241106202530.png|200]]

![[Pasted image 20241106202723.png|200]]
![[Pasted image 20241106204151.png|400]]
Use above command to cascade the changes into the connecting table.

```sql
CREATE TABLE dept(
	id INT PRIMARY KEY,
	name VARCHAR(50)
);
CREATE TABLE teacher(
	id INT PRIMARY KEY,
	name VARCHAR(50),
	dept_id INT,
	FOREIGN KEY (dept_id) REFERENCES dept(id)
	ON UPDATE CASCADE
	ON DELETE CASCADE
);

INSERT INTO dept (id,name)
VALUES
(101,'english'),
(102,'IT');
SELECT * FROM dept;

INSERT INTO teacher
VALUES
(101,'Adam',101),
(102,'Eve',102);

SELECT *FROM teacher;

UPDATE dept
SET id = 1012
WHERE id = 101;
```


![[Pasted image 20241106205126.png|400]]
![[Pasted image 20241106205313.png|400]]

![[Pasted image 20241106205711.png|200]]
![[Pasted image 20241106205604.png|400]]
![[Pasted image 20241107170122.png|200]]
![[Pasted image 20241107170145.png|200]]

```sql
-- To rename COL in SQL Server
EXEC sp_rename 'student.name' ,'full_name' , 'COLUMN';
-- To rename TABLE in SQL SERVER
EXEC sp_rename 'student' ,'stu';
```

**`EXEC sp_rename`:** This stored procedure is used to rename objects in SQL Server, including columns. The first argument specifies the fully qualified name of the object to be renamed, the second argument is the new name, and the third argument indicates the type of object being renamed (`COLUMN` in this case).

```sql

ALTER TABLE student
ADD grade CHAR DEFAULT 'C';-- DEFAULT  will work for next column not existing
-- To make all have some default value
UPDATE student
SET grade = 'C'
WHERE grade IS NULL;

```

```sql
CREATE TABLE student (
	rollno INT PRIMARY KEY,
	name VARCHAR(50),
	marks INT NOT NULL,
	grade VARCHAR(1),
	city VARCHAR(20)
);
--
INSERT INTO student
(rollno,name,marks,grade,city)
VALUES
(101,'anil',78,'C','Pune'),
(102,'bhumika',93,'C','Mumbai'),
(103,'chetan',85,'C','Mumbai'),
(104,'dhruv',96,'C','Delhi'),
(105,'emanuel',12,'C','Delhi'),
(106,'farah',82,'C','Delhi');

SELECT * FROM student;

EXEC sp_rename 'student.name' ,'full_name' , 'COLUMN';

EXEC sp_rename 'stu','student';

SELECT name
FROM XYZ.sys.tables;
ALTER TABLE student
ADD grade CHAR DEFAULT 'C';

UPDATE student
SET grade = 'C'
WHERE grade IS NULL;

ALTER TABLE student
ALTER COLUMN rollno VARCHAR(2);

ALTER TABLE student
DROP CONSTRAINT PK__student__FABA8B5B4F99EA39;

ALTER TABLE student
DROP COLUMN rollno;
```

![[Pasted image 20241107131306.png]]
![[Pasted image 20241107131330.png]]
![[Pasted image 20241107131409.png]]
![[Pasted image 20241107131508.png]]
![[Pasted image 20241107131518.png]]
![[Pasted image 20241107131633.png]]
![[Pasted image 20241107132027.png]]

In **SQL**, a **CROSS JOIN** is a type of join operation that produces the **Cartesian product** of two tables. It combines every row of the first table with every row of the second table, without any condition to match the rows.

### Syntax:

`SELECT *  FROM Table1  CROSS JOIN Table2;`

###Key Points:

1. **No Condition**: Unlike other types of joins (like INNER JOIN or LEFT JOIN), a CROSS JOIN does not require a condition to match rows.
2. **Output**: If `Table1` has mmm rows and `Table2` has nnn rows, the resulting table will have m×nm \times nm×n rows.
3. **Use Case**: It is often used when:
    - You want all combinations of rows from two tables.
    - Testing or debugging.
    - Generating all possible pairings of data.

---

### Example:

#### Table1: `Products`

|ProductID|ProductName|
|---|---|
|1|Laptop|
|2|Smartphone|

#### Table2: `Regions`

|RegionID|RegionName|
|---|---|
|A|Asia|
|B|Europe|

### Query:
`SELECT * FROM Products CROSS JOIN Regions;`

###Result:

|ProductID|ProductName|RegionID|RegionName|
|---|---|---|---|
|1|Laptop|A|Asia|
|1|Laptop|B|Europe|
|2|Smartphone|A|Asia|
|2|Smartphone|B|Europe|

### Caution

CROSS JOINs can generate a **large number of rows**, especially if the tables involved have many rows. Always use it carefully to avoid performance issues.

### Natural JOIN

A **NATURAL JOIN** in SQL is a type of join that combines rows from two tables based on the columns they have in common. It automatically matches columns by their names and data types without explicitly specifying the condition for the join.

### Syntax:

`SELECT *  FROM Table1  NATURAL JOIN Table2;`

### Key Points:

1. **Implicit Matching**: A **NATURAL JOIN** automatically identifies columns with the same name and compatible data types in both tables and uses them to perform the join.
2. **No Duplicate Columns**: In the result, duplicate columns (columns with the same name) appear only once.
3. **Inner Join Behavior**: By default, a NATURAL JOIN behaves like an INNER JOIN, including only rows where the values in the common columns match.

---

### Example:

#### Table1: `Employees`

|EmployeeID|Name|DepartmentID|
|---|---|---|
|1|Alice|101|
|2|Bob|102|
|3|Charlie|103|

#### Table2: `Departments`

|DepartmentID|DepartmentName|
|---|---|
|101|HR|
|102|Finance|
|104|IT|

---

### Query:
`SELECT *  FROM Employees  NATURAL JOIN Departments;`

### Result:

|EmployeeID|Name|DepartmentID|DepartmentName|
|---|---|---|---|
|1|Alice|101|HR|
|2|Bob|102|Finance|

---

### How It Works:

1. **Common Column**: The query looks for columns common to both tables. In this case, the common column is `DepartmentID`.
2. **Matched Rows**: Only rows where `DepartmentID` in `Employees` matches `DepartmentID` in `Departments` are included in the result.
3. **No Need for Explicit ON Clause**: Unlike an INNER JOIN, you don’t need to specify an `ON` condition.

---

### Differences Between NATURAL JOIN and Other Joins:

- **INNER JOIN**: Requires explicitly specifying the matching condition (`ON` clause).
- **CROSS JOIN**: Combines all rows without any condition.
- **NATURAL JOIN**: Automatically uses all columns with the same name and data type to match rows.

### Caution:

1. Avoid using NATURAL JOIN if column names in the tables are ambiguous or if additional clarity is needed. It’s safer to use **INNER JOIN** with explicit conditions in most cases.
2. The behavior of NATURAL JOIN can change if new columns with the same name are added to the tables.

```sql

CREATE TABLE emp(
	id INT PRIMARY KEY,
	name VARCHAR(30),
	manager_id INT
);
INSERT INTO emp
VALUES
(101,'adam',103),
(102,'bob',104),
(103,'casey',NULL),
(104,'donald',103);
TRUNCATE TABLE emp;
SELECT a.name AS Manager_name,b.name
FROM emp AS a
JOIN emp AS b
ON a.id = b.manager_id;
```
![[Pasted image 20241107133241.png]]

> Query always executes from right to left


![[Pasted image 20241107154945.png|400]]

- Union all includes duplicate values too 
![[Pasted image 20241107162636.png|200]]

![[Pasted image 20241107155152.png]]
![[Pasted image 20241107155415.png|300]]


![[Pasted image 20241107161020.png]]
![[Pasted image 20241107161008.png|400]]
![[Pasted image 20241107161120.png|400]]

![[Pasted image 20241107164147.png]]
![[Pasted image 20241107213217.png]]
![[Pasted image 20241107213112.png]]
![[Pasted image 20241107213248.png]]




![[Pasted image 20241107181712.png]]
![[Pasted image 20241107181905.png|400]]
![[Pasted image 20241107182436.png|400]]
![[Pasted image 20241107182446.png|400]]

![[Pasted image 20241107183412.png|400]]
![[Pasted image 20241107183433.png|400]]
![[Pasted image 20241107190137.png|400]]

# Trigger

Trigger is a named database object that is executed automatically when an _INSERT_, _UPDATE_ or _DELETE_ statement is issued against the associated table.
Triggers are database callback functions, which are automatically performed/invoked when a specified database event occurs.
### Create Trigger
Below given is the basic syntax for creating a trigger:
```sql
CREATE TRIGGER [IF NOT EXISTS] trigger_name
  [BEFORE|AFTER|INSTEAD OF] [INSERT|UPDATE|DELETE]
  ON table_name
  [WHEN condition]
BEGIN
statements;
END;
```

In this syntax, it can be noticed that:
- A trigger can be created with CREATE TRIGGER statement
- After that determine when the trigger will be executed, BEFORE, AFTER, or INSTEAD OF. BEFORE will execute the trigger before the statement next specified will execute, AFTER will execute after the statement will be executed, and INSTEAD OF will execute the trigger instead of the statement.
- After determining the time of execution of the trigger, determine the statement on which the trigger will execute, INSERT, UPDATE or DELETE.
- After that, indicate the table to which the trigger belongs.
- Finally, place the trigger logic in the BEGIN END block, which can be any valid SQL statements.

If we want to create a trigger on an **employee** table that runs after every insert statement, we would write a query as follows:
```sql
CREATE TRIGGER emp_trigger
  AFTER INSERT
  ON employee
 
BEGIN
	select null; /*Just for creating a empty valid trigger*/
END;
```
The above example creates a trigger and whenever data is inserted into the table that trigger will execute.

To maintain records of changes occurring in the database, we use triggers. Triggers also can be used for validating input such that if there is a valid input it will insert at that time only.For this we use the WHEN clause in the trigger. Sometimes after inserting the data we have to calculate. Also for that, we can use triggers.

## Trigger on Insert Statement
Let’s look at how to use a trigger on table **employee**
![[Pasted image 20241107205918.png]]

```sql
CREATE TRIGGER emp_trigger
 AFTER INSERT
 ON employee
BEGIN
  update employee set total_sal = NEW.salary + (NEW.salary*NEW.increment)/100 where emp_id=NEW.emp_id;
END;
```

In the above example, we can see that we created a trigger named ‘emp_trigger’ that works after the data is inserted into the table and increments the salary given to the employee by the percent given in the data.

We can see something called ‘New’ in the trigger body.

Well, there are two extensions to triggers 'OLD' and 'NEW'. OLD and NEW are not case sensitive.

- Within the trigger body, the OLD and NEW keywords enable you to access columns in the rows affected by a trigger
- OLD is used to get the old value of the column before it gets updated or deleted. Therefore OLD is used only with delete or update statements triggers
- NEW is used to get the value that is updated or just inserted in the database. Therefore NEW is used with the only update and insert statements triggers



**Task: C**reate a trigger named ‘**calc_marks**’ which calculates the total marks of the student and updates the column ‘**total_marks**’.
```sql
CREATE TRIGGER calc_marks
  AFTER INSERT
  ON students
BEGIN
  UPDATE students
  SET total_marks = NEW.sub1_marks + NEW.sub2_marks + NEW.sub3_marks
  WHERE roll_no = NEW.roll_no;
END;
```

**Task:** Create 2 triggers named ‘stud_update’ and ‘stud_delete’. Whenever a student is updated or deleted the respective triggers add the student’s roll number and adds the status ‘updated’ or ‘deleted’ based on the operation performed.

```sql
/*
create table students(
  roll_no INTEGER PRIMARY KEY,
  stud_name VARCHAR(50),
  marks INT);

create table stud_logs(
  roll_no INTEGER,
  status VARCHAR(15));

Tables already created
*/
CREATE TRIGGER stud_update
  AFTER UPDATE
  ON students
BEGIN
  INSERT INTO stud_logs
  VALUES
  (OLD.roll_no,'updated');
END;

CREATE TRIGGER stud_delete
  AFTER DELETE
  ON students
BEGIN
  INSERT INTO stud_logs
  VALUES
  (OLD.roll_no,'deleted');
END;
```

To destroy or delete a trigger use the **DROP TRIGGER**  command.
Following is the syntax to delete or drop or remove triggers in SQL.

```sql
DROP TRIGGER [IF EXISTS] trigger_name.
```

![[Pasted image 20241108081851.png|400]]
### **Introduction to Triggers**

A **trigger** is a procedural code in a database that automatically executes in response to certain events on a particular table or view. Triggers are often used to enforce business rules, maintain data integrity, or perform audit tasks.

- Triggers are associated with **INSERT**, **UPDATE**, or **DELETE** operations.
- They are activated automatically whenever the specified database event occurs.
- Triggers help automate repetitive tasks like logging changes or cascading updates/deletes.

---

### **Types of Triggers**

1. **DML Triggers**  
    Triggered by **Data Manipulation Language** operations (INSERT, UPDATE, DELETE) on a table or view.  
    Examples:
    
    - **AFTER Triggers:** Executed after the triggering event has occurred.
    - **INSTEAD OF Triggers:** Executes in place of the triggering event.
2. **DDL Triggers**  
    Triggered by **Data Definition Language** operations (CREATE, ALTER, DROP) on the database schema.
    
3. **LOGON Triggers**  
    Triggered by a user logging into the database. Commonly used for session control or auditing login attempts.
    
4. **Database-Level Triggers**  
    These are triggers defined at the database level and can respond to server-wide events like startup, shutdown, or errors.


### **Introduction to Package**

In database systems, particularly in **Oracle PL/SQL**, a **package** is a schema object that groups logically related **procedures**, **functions**, **variables**, **constants**, **cursors**, and **exceptions**. Packages help organize and modularize code, making it easier to maintain and reuse.

A package consists of two parts:

1. **Package Specification**: Declares the public interface (procedures, functions, and variables accessible to users or other programs).
2. **Package Body**: Contains the implementation of the procedures and functions declared in the specification.

---

### **Advantages of Creating Packages**

1. **Code Reusability**: Centralized, reusable code reduces duplication.
2. **Encapsulation**: Allows you to hide implementation details and expose only necessary components.
3. **Performance Optimization**: The entire package is loaded into memory on first access, reducing the cost of subsequent calls.
4. **Improved Security**: Control access by exposing only specific components in the package specification.
5. **Ease of Maintenance**: Group related subprograms in one place, making code easier to manage and debug.
6. **Modularity**: Simplifies complex applications by breaking them into manageable modules.

---

### **Package Specification**

The package specification is the interface for the package. It declares:

- Procedures
- Functions
- Public variables
- Constants
- Cursors
- Exceptions

### **Developing a Package**

To create a package in a database, you need to define its **specification** and, optionally, its **body**. A package specification defines the interface (what the package offers), while the package body contains the implementation of its functionalities.

#### **Steps to Develop a Package**

1. **Define the Package Specification**:
    - Declare procedures, functions, variables, and cursors.
    - These declarations are accessible to users or other programs.
2. **Define the Package Body** (if required):
    - Provide the implementation of the declared procedures and functions.
    - Optionally include private procedures, functions, or variables not exposed in the specification.

#### **Package Specification Syntax**
```sql
CREATE OR REPLACE PACKAGE package_name IS
    -- Public variables
    variable_name data_type;

    -- Function declarations
    FUNCTION function_name (parameters) RETURN data_type;

    -- Procedure declarations
    PROCEDURE procedure_name (parameters);

END package_name;

```

#### **Package Body Syntax**

```sql
CREATE OR REPLACE PACKAGE BODY package_name IS
    -- Implementations of functions
    FUNCTION function_name(parameters) RETURN data_type IS
    BEGIN
        -- Logic here
    END function_name;

    -- Implementations of procedures
    PROCEDURE procedure_name(parameters) IS
    BEGIN
        -- Logic here
    END procedure_name;

END package_name;

```

### **Calling Packages**

Once the package is developed, its components (procedures or functions) can be invoked using the package name as a prefix.

#### **Syntax for Calling**
```sql
package_name.procedure_name(parameters);
variable := package_name.function_name(parameters);
```


EXAMPLE
```sql
CREATE OR REPLACE PACKAGE Math_Package IS
    FUNCTION add_numbers(a NUMBER, b NUMBER) RETURN NUMBER;
    PROCEDURE print_message(message VARCHAR2);
END Math_Package;


CREATE OR REPLACE PACKAGE BODY Math_Package IS
    FUNCTION add_numbers(a NUMBER, b NUMBER) RETURN NUMBER IS
    BEGIN
        RETURN a + b;
    END add_numbers;

    PROCEDURE print_message(message VARCHAR2) IS
    BEGIN
        DBMS_OUTPUT.PUT_LINE(message);
    END print_message;
END Math_Package;

BEGIN
    -- Calling the function
    DBMS_OUTPUT.PUT_LINE('Sum: ' || Math_Package.add_numbers(10, 20));

    -- Calling the procedure
    Math_Package.print_message('Hello, Package!');
END;

```

### **Bodiless Packages**

A bodiless package is a package that **does not require a body**. These are used when:

1. The package contains only constants, types, variables, or cursors.
2. The package contains no procedures or functions requiring implementation.


```sql
CREATE OR REPLACE PACKAGE package_name IS
    -- Declarations of variables, constants, or cursors
    constant_name CONSTANT data_type := value;
    variable_name data_type;
END package_name;

--example
CREATE OR REPLACE PACKAGE Config_Package IS
    -- Constants
    max_limit CONSTANT NUMBER := 100;
    app_name CONSTANT VARCHAR2(50) := 'Finance Tracker';

    -- Variables
    current_user VARCHAR2(50);
END Config_Package;


BEGIN
    -- Accessing constants
    DBMS_OUTPUT.PUT_LINE('App Name: ' || Config_Package.app_name);

    -- Assigning and accessing variables
    Config_Package.current_user := 'John Doe';
    DBMS_OUTPUT.PUT_LINE('Current User: ' || Config_Package.current_user);
END;

```


### **Key Benefits of Bodiless Packages**

1. Simplifies declaration of constants and global variables.
2. Reduces the complexity of implementation by removing unnecessary package bodies.
3. Enhances modularity and organization for managing configuration or static data.