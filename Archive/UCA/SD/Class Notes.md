
![[WhatsApp Image 2025-07-08 at 19.51.25_0fccf2b7.jpg]]![[Pasted image 20250708200541.png]]

- [[System Design vs System Architecture]]

---

![[Pasted image 20250715184201.png]]

![[Pasted image 20250715184207.png]]
![[Pasted image 20250715184219.png]]
4th is microservice architecture
![[Pasted image 20250715184224.png]]
![[Pasted image 20250715184228.png]]
![[Pasted image 20250715184236.png]]

Q1.  How many types of [[models]] are there for designing or building a system  or software? What model should be used in what situation?

Q2. What is the difference between [[client side and server side development]]?

Q3. What is the difference between [[alpha testing and beta testing]]?

Q4. How many [[types of testing]] are there and what are their differences?

Q5. Difference between [[micro kernel and monolithic kernel]]?

---

![[Pasted image 20250717102952.png]]
![[Pasted image 20250717103000.png]]

Q. [[Which OS has monolithic architecture and which has micro-kernel architecture]].


# HLD
- Top level view of the application.
- It talks about layered Architecture.
- Alignment to business objectives
- Example in CRM app what CRUD operations to setup not how they will be implemented is done in HLD.
- Core Components:
	- GUI Design
	- Database Design
# LLD
- It is extension of HLD.
- In low level design we think about how to implement the functionality in the system.
- Example in CRM app we want to manage user data by setting up CRUD operations , so like things like what parameters are required to implement that , what should it return etc. is define under LLD.
- UML diagram is a way of representing design.
- Core Components:
	- Class Diagrams
	- Sequence Diagrams
	- Data Flow Diagrams
		- Highlights user inputs and outputs.
	- Database Schema
	- User Interface Design
- Procedure for low level design:
	- OOPS (Object Oriented Principles)
	- Process of analyzing & design
	- Design patterns
		- Creational Patterns
		- Behavior Patterns
		- Structural Patterns
	- UML Diagrams
	- SOLID Principles
		- Single Responsibility Principle (SRP)
			- Each operation or module should perform only one functionality
		- Open-closed principle (OCP)
			- Classes can be extended by incrementing functionality.
		- Liskov's Substitution Principle(LSP)
			- It was introduced by **Barbara Liskov** in 1987.
			![[Pasted image 20250813121511.png|400]]
		- Interface Segregation Principle(ISP)
			- Client can't be forced to depend on methods they do not want to use.
			- Even if you know their is better way or new modern way to implement some functionality but still if client don't want that then do not use it.
		- Dependency Inversion Principle(DIP)
			- High level module should not depend on low level modules. They should depend on the abstraction.
			![[Pasted image 20250813121813.png|400]]
			![[Pasted image 20250813122330.png|400]]


---

# SQL

```sql
CREATE TABLE STUDENT (
    ROLL_NO INT PRIMARY KEY,
    NAME VARCHAR(50),
    ADDRESS VARCHAR(100),
    PHONE VARCHAR(15),
    AGE INT
);

INSERT INTO STUDENT VALUES
(1, 'HARSH', 'DELHI', '98654', 18),
(2, 'PRATIK', 'BIHAR', '789456123', 19),
(3, 'RIYANKA', 'SILIGURI', '1456324', 20),
(4, 'DEEP', 'RAMNAGAR', '7896542', 18);

CREATE TABLE COURSE (
    COURSE_ID INT,
    ROLL_NO INT,
    COURSE_NAME VARCHAR(50),
    FOREIGN KEY (ROLL_NO) REFERENCES STUDENT(ROLL_NO)
);

CREATE TABLE COURSE_DETAILS (
    COURSE_ID INT PRIMARY KEY,
    INSTRUCTOR VARCHAR(50),
    DURATION INT
);

INSERT INTO COURSE VALUES
(1, 1, 'Mathematics'),
(2, 2, 'Physics'),
(2, 3, 'Physics'),
(3, 4, 'Chemistry');

INSERT INTO COURSE_DETAILS VALUES
(1, 'Dr. Sharma', 12),
(2, 'Prof. Verma', 10),
(3, 'Dr. Singh', 8);


-- Get all students names, course name who are enrolled in same course

SELECT s.NAME, c.COURSE_NAME
FROM STUDENT as s INNER JOIN COURSE as c
ON s.ROLL_NO = c.ROLL_NO;

-- Get all students names, course name who are enrolled in same course whose age is greater than 18

SELECT s.NAME, c.COURSE_NAME, s.AGE
FROM STUDENT as s INNER JOIN COURSE as c
ON s.ROLL_NO = c.ROLL_NO
WHERE s.AGE > 18;

-- Get all students names, course name who are enrolled in same course whose age is greater than 18 in descending order

SELECT s.NAME, c.COURSE_NAME, s.AGE
FROM STUDENT as s INNER JOIN COURSE as c
ON s.ROLL_NO = c.ROLL_NO
WHERE s.AGE > 18
ORDER BY s.AGE desc;


-- Find how many students are enrolled in each course but show only courses having more than 1 student

SELECT c.COURSE_NAME, COUNT(s.ROLL_NO) as Total_Students
FROM STUDENT as s JOIN COURSE as c
ON s.ROLL_NO = c.ROLL_NO
GROUP BY c.COURSE_NAME
HAVING Total_Students > 1;

-- OR

SELECT c.COURSE_NAME, COUNT(c.ROLL_NO) as Total_Students
FROM COURSE as c
GROUP BY c.COURSE_NAME
HAVING Total_Students > 1;

-- Show all students in courses taught by Prof. Verma ordered by student name alphabetically

SELECT s.ROLL_NO, s.NAME
FROM COURSE as c, STUDENT as s, COURSE_DETAILS as cd
WHERE c.ROLL_NO = s.ROLL_NO and c.COURSE_ID = cd.COURSE_ID and cd.INSTRUCTOR = "Prof. Verma"
ORDER BY s.NAME;

-- Show all the students and course name including those student who are not enrolled in any course

SELECT s.NAME, c.COURSE_NAME
FROM COURSE as c LEFT JOIN STUDENT as s
ON c.ROLL_NO = s.ROLL_NO;


-- Show all the students enrolled in each course including the unassigned courses but only those courses who have value greater than 1
SELECT c.COURSE_NAME, COUNT(s.ROLL_NO) as Total_Students
FROM STUDENT s LEFT JOIN COURSE c
ON s.ROLL_NO = c.ROLL_NO
GROUP BY c.COURSE_NAME
HAVING Total_Students > 1;

INSERT INTO COURSE_DETAILS VALUES(4, "Mr. Dhanur", 24);

CREATE TABLE EMPLOYEE(
  EID INT PRIMARY KEY,
  NAME VARCHAR(20),
  Mgr_ID INT
);

insert into EMPLOYEE values
(1,"Aniket",NULL),
(2,"Aanandit",1),
(3,"Anishka",1),
(4,"Anikanta",2),
(5,"Jashan",3);

-- Find out all employees having manager
SELECT e.NAME, m.NAME
FROM EMPLOYEE as e JOIN EMPLOYEE as m
WHERE e.Mgr_ID = m.EID;

-- Find all employees who report to manager Aniket
SELECT e.EID, e.NAME
FROM EMPLOYEE as e JOIN EMPLOYEE as m
ON e.Mgr_ID = m.EID
WHERE m.NAME == 'Aniket';

SELECT EID, NAME
FROM EMPLOYEE
WHERE mgr_id = (
  SELECT EID
  FROM EMPLOYEE
  WHERE NAME = 'Aniket'
);
-- List employees and their managers sorted by manager name.


SELECT e.NAME, m.NAME
FROM EMPLOYEE e LEFT JOIN EMPLOYEE m
ON m.EID = e.Mgr_ID
ORDER BY m.NAME;



-- Find out how many subordinates each manager have and display manager name having more than 1 subordinate.

SELECT m.NAME, COUNT(*) as Number_of_Subordinates
FROM EMPLOYEE as e JOIN EMPLOYEE as m
ON m.EID = e.Mgr_ID
GROUP BY e.Mgr_ID
HAVING COUNT(*) > 1;

-- Cross JOIN Student, course name starting by 'A'

SELECT s.NAME, c.COURSE_NAME
FROM STUDENT AS s CROSS JOIN COURSE AS c
WHERE c.COURSE_NAME LIKE 'P%';


ALTER TABLE COURSE
ADD COLUMN FEE INT
CHECK (FEE BETWEEN 50000 AND 100000);

UPDATE COURSE SET FEE = 52000 WHERE ROLL_NO = 1;
UPDATE COURSE SET FEE = 68000 WHERE ROLL_NO = 2;
UPDATE COURSE SET FEE = 75000 WHERE ROLL_NO = 3;
UPDATE COURSE SET FEE = 99000 WHERE ROLL_NO = 4;

-- Find students enrolled in courses fee is greater than 50000

SELECT *
FROM STUDENT
WHERE ROLL_NO IN
(SELECT ROLL_NO
 FROM COURSE
 WHERE FEE > 50000
);

-- Find all students which are enrolled in course with the maximum fees
SELECT *
FROM STUDENT
WHERE ROLL_NO IN(
  SELECT ROLL_NO
  FROM COURSE
WHERE FEE = MAX

```

