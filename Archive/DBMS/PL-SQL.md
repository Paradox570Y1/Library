- Whenever changes are made on the database then we need to reflect those changes on the endpoints so in order to trigger those changes we use PL-SQL.
### PL/SQL Block :
#### 1. Anonymous Block
- **Description**: Anonymous blocks are unnamed PL/SQL blocks that do not have a defined name. They are typically used for one-time tasks or quick data processing and do not remain stored in the database.
- **Usage**: Anonymous blocks are commonly used for ad hoc operations like testing, data updates, or quick computations.

- In Microsoft SQL
```sql
-- Anonymous Block
DECLARE @message VARCHAR(50);
SET @message = 'Hello';
PRINT @message;
```


#### Named Blocks
- **Description**: Named blocks include named PL/SQL subprograms such as procedures, functions, packages, and triggers. Named blocks are stored in the database, allowing for repeated use and ease of access by other programs.
- **Types**:
    - **Procedures**: Perform a specific action but do not return a value.
    - **Functions**: Perform a specific task and return a single value.
    - **Packages**: A collection of related procedures, functions, and variables.
    - **Triggers**: Execute automatically in response to specific database events, such as INSERT, UPDATE, or DELETE operations.

- Stored Procedure
```sql
CREATE PROCEDURE GreetUserss
AS
BEGIN 
	 PRINT 'Hello,User!';
END;
EXEC GreetUserss;

```

## Procedures parameters
### Parameter Modes in Procedures (Beginner-Friendly Explanation)

When creating stored procedures in databases, you often need to pass **parameters** (inputs or outputs) to or from the procedure. **Parameter modes** define how these parameters behave—whether they act as inputs, outputs, or both.

Think of parameters like variables that help your procedure communicate with the outside world.

---

### Three Main Parameter Modes

1. **IN (Input Parameter)**
    
    - **Definition**: Passes data _into_ the procedure. The procedure can use this value, but it cannot change it.
    - **Analogy**: It’s like giving a calculator a number to process; the calculator can use the number, but it won’t modify it.
    - **Key Point**: The parameter is **read-only** inside the procedure.
    
    **Example:**
    
    sql
    
    Copy code

```sql
CREATE PROCEDURE greet_user(IN user_name VARCHAR(50)) 
BEGIN     
	SELECT CONCAT('Hello, ', user_name, '!') AS Greeting; 
END;
```

    
    **Usage:**
    
```sql
CALL greet_user('Alice'); -- Output: Hello, Alice!
```
    

---

2. **OUT (Output Parameter)**
    
    - **Definition**: Passes data _out_ of the procedure. The procedure assigns a value to this parameter, and the caller receives the result.
    - **Analogy**: It’s like a vending machine. You press a button, and the machine gives you a snack.
    - **Key Point**: The parameter is **write-only** inside the procedure.
    
    **Example:**
    
    ```sql
CREATE PROCEDURE get_total_salary(OUT total_salary DECIMAL(10, 2)) 
BEGIN     
    SELECT SUM(salary) INTO total_salary FROM employees; 
END;
```
    
    **Usage:**

    
    ```sql
    CALL get_total_salary(@total);  
    SELECT @total; -- Output: The total salary from the employees table
```
    

---

3. **INOUT (Input and Output Parameter)**
    
    - **Definition**: Acts as both an input and an output. You pass a value _into_ the procedure, and the procedure can modify and return it.
    - **Analogy**: It’s like lending someone a pen. They can use it, refill it, and give it back to you.
    - **Key Point**: The parameter is **read-write** inside the procedure.
    
    **Example:**

    
    ```sql
    CREATE PROCEDURE increment_number(INOUT number INT) 
    BEGIN     
      SET number = number + 1; 
    END;
```
    
    **Usage:**

    ```sql
    SET @num = 5; 
    CALL increment_number(@num);  
    SELECT @num; -- Output: 6
```

### In SQL Server
```sql
CREATE PROCEDURE increment_number 
    @number INT OUTPUT
AS
BEGIN
    SET @number = @number + 1;
END;
```
    
```sql
DECLARE @num INT = 5; -- Declare and initialize a variable
EXEC increment_number @num OUTPUT; -- Call the procedure and pass the variable as OUTPUT
PRINT @num; -- Output: 6
```
---

### Summary Table for Quick Reference

|Mode|Can Pass Value In?|Can Return Value Out?|Modifiable Inside Procedure?|
|---|---|---|---|
|**IN**|Yes|No|No|
|**OUT**|No|Yes|Yes|
|**INOUT**|Yes|Yes|Yes|

---

### Why Use Parameter Modes?

1. **IN Parameters**: When you only need to provide inputs, like filtering data (e.g., `WHERE user_id = ?`).
2. **OUT Parameters**: When you need to send results back to the caller (e.g., total salary, status, or messages).
3. **INOUT Parameters**: When the same variable is needed as input and modified output (e.g., counters or accumulators).


```sql
--In SQL Server
--User-Defined Function
CREATE FUNCTION GetGreeting()
RETURNS VARCHAR(50)
AS BEGIN
    RETURN 'Hello,User!';
END;
SELECT dbo.GetGreeting() AS Greeting;


-- In My SQL
DELIMITER // 
CREATE FUNCTION GetGreeting() 
RETURNS VARCHAR(50) 
DETERMINISTIC 
BEGIN 
	RETURN 'Hello, User!'; 
END; 
// 
DELIMITER ;
```

```sql
--If Statement
DECLARE @score INT = 85;
DECLARE @grade VARCHAR(2);
IF @score >=90
	SET @grade = 'A';
ELSE IF @score >= 80
	SET @grade = 'B';
ELSE IF @score >= 70
	SET @grade = 'C';
ELSE
	SET @grade = 'D';

PRINT 'Grade: ' + @grade;
```

```sql
--Using Switch
DECLARE @day INT = 3;
DECLARE @dayName VARCHAR(10);

SET @dayName  = CASE @day
	WHEN 1 THEN 'Monday'
	WHEN 2 THEN 'Tuesday'
	WHEN 3 THEN 'Wednesday'
	WHEN 4 THEN 'Thursday'
	WHEN 5 THEN 'Friday'
	WHEN 6 THEN 'Saturday'
	WHEN 7 THEN 'Sunday'
	ELSE 'Invalid Day'
END;
PRINT 'Day: ' + @dayName;
```

```sql
--While loop 
DECLARE @counter INT = 1;
WHILE @counter <=5
BEGIN
	PRINT 'Counter: ' + CAST(@counter AS VARCHAR); --Requires type casting
	SET @counter = @counter +1;  -- Increment the counter
END;
```

```sql
--For loop
DECLARE @counter INT = 1;
DECLARE @max INT = 5;

WHILE @counter <= @max
BEGIN
    PRINT 'This is iteration ' + CAST(@counter AS VARCHAR(10));
    SET @counter = @counter + 1;  -- Increment the counter like in a FOR loop
END;
```

```sql
CREATE TABLE Employees(
	EmployeeID INT PRIMARY KEY,
	FirstName NVARCHAR(50),
	LastName NVARCHAR(50),
	Salary DECIMAL(10,2),
	DepartmentID INT
);

CREATE TABLE Departments (
	DepartmentID INT PRIMARY KEY,
	DepartmentName NVARCHAR(50),
	Budget DECIMAL(10,2),
	Expenditure DECIMAL(10,2)
);

INSERT INTO Departments (DepartmentID, DepartmentName, Budget, Expenditure)
VALUES
(1,'Sales',50000,30000),
(2,'Marketing',60000,65000),
(3,'IT',70000,60000),
(4,'HR',40000,35000);
TRUNCATE TABLE Employees;
INSERT INTO Employees (EmployeeID,FirstName,LastName,Salary,DepartmentID)
VALUES

(1,'Alice','Johnson',40000,1),
(2,'Bob','Smith',45000,1),
(3,'Charlie','Brown',50000,2),
(4,'David','Wilson',55000,3),
(5,'Eve','Davis',60000,4);

CREATE TABLE SalaryChanges(
	EmployeeID INT,
	OldSalary DECIMAL(10,2),
	NewSalary DECIMAL(10,2),
	ChangeDate DATETIME
);

--Cursor to process each employee
DECLARE @EmployeeID INT,@FirstName NVARCHAR(50), @LastName NVARCHAR(50), @OldSalary DECIMAL(10,2);
DECLARE @NewSalary DECIMAL(10,2);

--Cursor definition
DECLARE EmployeeCursor CURSOR FOR
SELECT e.EmployeeID, e.FirstName,e.LastName,e.Salary
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DepartmentID
WHERE d.Expenditure < d.Budget;

--Error handling variables
DECLARE @ErrorMessage NVARCHAR(4000), @ErrorSeverity INT;

--Open the CURSOR
OPEN EmployeeCursor;

--BEGIN TRY
	FETCH NEXT FROM EmployeeCursor INTO @EmployeeID,@FirstName, @LastName, @OldSalary;

	WHILE @@FETCH_STATUS =0
	BEGIN
		--Calculate the new salary
		SET @NewSalary = @OldSalary * 1.10;

		--Update the employee's salary
		UPDATE Employees
		SET Salary = @NewSalary
		WHERE EmployeeID = @EmployeeID;
		--Insert a record into SalaryChanges
		INSERT INTO SalaryChanges (EmployeeID, OldSalary,NewSalary,ChangeDate)
		VALUES (@EmployeeID,@OldSalary,@NewSalary,GETDATE());

		--Fetch the next employee
		FETCH NEXT FROM EmployeeCursor INTO @EmployeeID,@FirstName, @LastName, @OldSalary;

END
		-- Close the cursor
		CLOSE EmployeeCursor;
		DEALLOCATE EmployeeCursor;
--END TRY

--BEGIN CATCH
	--Handle errors
	--SET @ErrorMessage = ERROR_MESSAGE();
	---SET @ErrorSeverity = ERROR_SEVERITY();
SELECT * FROM SalaryChanges;
```

### Introduction to Cursors in DBMS

A **cursor** in a database management system (DBMS) is a control structure that allows traversal over the rows of a result set retrieved by executing a query. It provides a mechanism for iterating through individual rows and processing them one at a time, which is particularly useful when dealing with large datasets or when row-by-row operations are required.

Cursors are commonly used in stored procedures, triggers, and other database operations that require processing of data row-by-row.

---

### Types of Cursors

Cursors can be broadly classified into the following categories based on their functionality and implementation:

#### 1. **Based on Scope**

- **Implicit Cursor**: Automatically created by the DBMS when a SQL statement is executed (e.g., `INSERT`, `UPDATE`, or `SELECT`). These are managed by the system and do not require explicit declaration.
- **Explicit Cursor**: Defined and controlled explicitly by the programmer in a procedural SQL block, allowing finer control over data retrieval and processing.

#### 2. **Based on Accessibility**

- **Static Cursor**: Creates a snapshot of the data when the cursor is opened. Any changes made to the database after the cursor is opened are not reflected in the cursor.
- **Dynamic Cursor**: Reflects changes made to the database while the cursor is open (e.g., new rows, updated rows).
- **Forward-only Cursor**: Moves in a single direction (from the first row to the last). It does not allow backward movement.

#### 3. **Based on Data Manipulation**

- **Read-only Cursor**: Allows only data retrieval, with no updates or modifications.
- **Updatable Cursor**: Enables updates to the data in the rows currently being accessed by the cursor.

#### 4. **Implementation-based Cursors** (specific to DBMS platforms):

- **Server-side Cursor**: Managed by the database server, often used in client-server applications.
- **Client-side Cursor**: Managed by the client application, suitable for smaller result sets.

---

### Advantages of Cursors

1. **Row-by-row Processing**: Allows processing of one row at a time, enabling complex row-specific operations.
2. **Enhanced Control**: Provides finer control over the result set compared to SQL's set-based processing.
3. **Dynamic Data Handling**: Dynamic cursors allow real-time reflection of changes made to the underlying data.
4. **Useful for Sequential Operations**: Ideal for operations requiring sequential access, like batch processing or hierarchical data traversal.

---

### Disadvantages of Cursors

1. **Performance Overhead**: Cursors can be slower compared to set-based operations since they process rows individually rather than as a set.
2. **Resource Intensive**: Cursors consume additional memory and resources, which may impact database performance.
3. **Complexity**: Writing and managing cursor-based operations can be more complex than set-based SQL queries.
4. **Concurrency Issues**: Cursors can lead to locking problems and reduce the level of concurrency in the database.
5. **Maintenance Challenges**: Code involving cursors may be harder to maintain and debug.

---



# Cursor
```sql
CREATE TABLE Emp (
    EmployeeID INT PRIMARY KEY,
    Name NVARCHAR(100),
    PerformanceRating VARCHAR(20),
    Bonus DECIMAL(10, 2) DEFAULT 0.00,
    Status VARCHAR(20)
);

INSERT INTO Emp (EmployeeID, Name, PerformanceRating, Status)
VALUES
    (1, 'Rahul', 'Excellent', 'Active'),
    (2, 'Vijay', 'Good', 'Active'),
    (3, 'Neha', 'Average', 'Active'),
    (4, 'Prince', 'Poor', 'Inactive'),
    (5, 'Megha', 'Good', 'Active');

CREATE PROCEDURE SetEmployeeBonus
AS
BEGIN
    DECLARE @EmployeeID INT
    DECLARE @Name NVARCHAR(100)
    DECLARE @PerformanceRating VARCHAR(20)
    DECLARE @Bonus DECIMAL(10, 2)

    DECLARE employee_cursor CURSOR FOR
    SELECT EmployeeID, Name, PerformanceRating
    FROM Emp

    OPEN employee_cursor

    FETCH NEXT FROM employee_cursor INTO @EmployeeID, @Name, @PerformanceRating

    WHILE @@FETCH_STATUS = 0
    BEGIN
        
        IF @PerformanceRating = 'Excellent'
            SET @Bonus = 1000.00
        ELSE IF @PerformanceRating = 'Good'
            SET @Bonus = 500.00
        ELSE IF @PerformanceRating = 'Average'
            SET @Bonus = 250.00	
        ELSE
            SET @Bonus = 0.00
----------------------------------------------------------------------------------------------
        UPDATE Emp
        SET Bonus = @Bonus
        WHERE EmployeeID = @EmployeeID

        FETCH NEXT FROM employee_cursor INTO @EmployeeID, @Name, @PerformanceRating
    END

    CLOSE employee_cursor
    DEALLOCATE employee_cursor
END;

EXEC SetEmployeeBonus;
SELECT * FROM Emp;
```