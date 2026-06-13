### SQL : Structured Query Language

###### Points to Remember
- It's not case sensitive
###### Basic Terms
- `Schema:` It is collection of tables.

##### Create Schema
- Authorization not compulsory
```sql
create schema schema_name authorization 'R'
```

##### Create Database
```sql
create database myData; --To create database
```
- After refreshing you can see it.
![[Pasted image 20240718163637.png|200]]
##### Create Table
- It is good practice to define a primary key
```sql
create table Employee(  -- To create the table
Name varchar(20),
SSN varchar(10),
DOB Date,
Emp_id varchar(10),
Primary Key(SSN)
)
```

### Constraints
- **Primary Key:** Uniquely identifies each record in a table.
- **Foreign Key:** Ensures referential integrity by linking to a primary key in another table.
- **Default:** Sets a default value for a column if no value is specified.
- **Check:** Enforces a condition that each value in a column must satisfy.
- **Unique:** Ensures all values in a column are different.
- **Referential Integrity Constraint:** If our table doesn't have a unique key then it uses a foreign key which is Candidate Key of another table.

##### Select Query
```sql
select *from Employee; --To see the table
```
![[Pasted image 20240718164911.png|200]]


**Q.** Retrieve me Name & Address of all Employee who works for "Research" Department.
```sql
-- If we are using one table
select F_name,M_name,L_name,Address
from Employee
where D_name = "Research" -- D_name is department 

--                        OR

-- If we are using two tables
select F_name,M_name,L_name,Address
from Employee,Department
where D_name="Research" and D_No = D_number; -- D_No is department no.

--                        OR

select F_name,M_name,L_name,Address
from Employee as E,Department as D        -- here we are giving an aliace
where D_name="Research" and D_No = D.D_No;

```

###### To select different names.
```sql
SELECT DISTINCT Fname FROM Employee
WHERE Dno='n'
```

###### UNION
- The `UNION` operator is used to combine the result sets of two or more `SELECT` statements. It removes duplicate rows between the various `SELECT` statements.
```sql
SELECT FirstName, LastName FROM Employees
UNION
SELECT FirstName, LastName FROM Managers;
```

###### INTERSECTION
- SQL does not have a built-in `INTERSECTION` operator, but you can achieve the same result using `INNER JOIN` or using `INTERSECT` if the SQL dialect supports it.
```sql
SELECT FirstName, LastName FROM Employees
INTERSECT
SELECT FirstName, LastName FROM Managers;
```

# TABLES TO BE USED
**Tables to be used**
- `Employee ->` Fname, Mname, Lname, SSN, B-date, address, salary, super-SSN(manager), D_No
- `Department->` Dname, Dnumber, mr(manager)-SSN, mr(manager)-start-date
- `Dept.-Locations->` D_Number, D_location
- `Project->` Pname, Pnumber, Plocation, Dnum
- `Works on->` E_SSN, Dno,Pno, Hours
- `Dependent->` ESSN, Dependent-name, B-date, relationship
#### LIKE Query
- Used for string comparison.
- The `LIKE` operator in SQL is used to search for a specified pattern in a column. It is often used in a `WHERE` clause to filter results based on partial matches of strings.
 **Wildcards in LIKE**
	- `%`: Represents zero, one, or multiple characters.
	- `_`: Represents a single character.

```sql
SELECT * FROM Customers
WHERE Name LIKE 'J%';
--Basic Pattern Matching
-- This query will return all rows from the `Customers` table where the `Name` starts with the letter 'J'. For example, it might return "John", "Jane", and "Jack".
```

```sql
SELECT * FROM Customers
WHERE Name LIKE '%a%';
--Pattern Matching Anywhere in the String
--This query will return all rows where the `Name` contains the letter 'a' anywhere in the string. For example, it might return "Maria", "Hannah", and "James".
```

```sql
SELECT * FROM Customers
WHERE Name LIKE '%son';
--Pattern Matching at the End of the String
--This query will return all rows where the `Name` ends with 'son'. For example, it might return "Johnson", "Wilson", and "Mason".
```

```sql
SELECT * FROM Customers
WHERE Name LIKE 'J_n';
--Single Character Wildcard
--This query will return all rows where the `Name` is three characters long, starts with 'J', and ends with 'n', with any single character in between. For example, it might return "Jon" and "Jan".
```

```sql
SELECT * FROM Customers
WHERE Name LIKE 'J%n';
--Combining Wildcards
--This query will return all rows where the `Name` starts with 'J' and ends with 'n', with any characters in between. For example, it might return "John", "Jordan", and "Julian".
```

- To concatenate use ||  (OR operator)
```sql
SELECT FName||LName FROM Employee;
```

- We can use operations on attribute
```sql
SELECT Fname 0.1*Salary FROM Employee
```

- To get records in some range
	Use `BETWEEN`


Q1. Retrieve list of employee & the project they are working on , ordered by department & within each department ordered by last name, then first name.

```sql
SELECT 
    d.department_name, 
    e.last_name, 
    e.first_name, 
    p.project_name
FROM 
    employees e
JOIN 
    departments d ON e.department_id = d.department_id
JOIN 
    projects p ON e.project_id = p.project_id
ORDER BY 
    d.department_name, 
    e.last_name, 
    e.first_name;
 
```

```sql
SELECT Pname, Fname, Lname, Dname
FROM Employee E, WorksON W,Project P,Department D
WHERE D.Dnumber = E.Dno AND W.Pno = P.Pnumber AND E.SSN = W.ESSN
ORDER BY D.Dname, E.Lname, E.Fname
```

Q2. Find Fname of Employee who works for department located at Mumbai.

```sql
SELECT Fname,Dname,Location_name
FROM Employee E, WorksON W, Department D, Department_location L
WHERE D.Dnumber = E.Dno AND D.Dlocation = "Mumbai" AND E.SSN = W.ESSN

--OR
SELECT Fname FROM Employee
WHERE Dno
IN(SELECT Dnumber FROM Dept_locations
WHERE D_Location = "Mumbai"
)
```



Q4. Find all the employee who have worked on some project on which employee no. 10 has worked for same no. of hours.

```sql
SELECT DISTINCT ESSN
FROM WorksOn
WHERE (Pno,Hours) IN(
SELECT Pno,Hours FROM WorksOn
WHERE ESSN = '10'
)
```

Q5 Select Fname of all employee whose salary is greater than salary of all employee in department 
```sql
SELECT Fname
FROM Employee
WHERE Salary > Salary IN(
SELECT MAX(Salary)
FROM Employee as E
WHERE Dno = 5
)
```

```sql
SELECT Fname FROM Employee
WHERE Salary > (
SELECT Salary FROM Employee
WHERE Dno = 5
)
```

- _Whenever same attribute is involved in inner and outer loop then it is co-related query_.

Q6 Retrieve the Fname of each employee who has dependent with the same first name as the employee.

```sql
SELECT Fname
FROM Employee as E,Dependent as D
WHERE D.Dependent_name == E.Fname
```

```sql
SELECT Fname
FROM Employee as E
WHERE ESSN
IN (SELECT ESSN FROM Dependent as D
   WHERE E.Fname = D.Fname)
```

- Whenever you are writing an aggregation function provide it a name otherwise "no column name" will be displaces hence create alicing/ placeholder for that column.
- COUNT(*) FOR COUNTING ROWS
```sql
SELECT Product,COUNT(*) AS TotalSale
FROM Sales
GROUP BY Product
```