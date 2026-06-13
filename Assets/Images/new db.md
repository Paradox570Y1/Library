CREATE TABLE Sales (
    SaleID INT PRIMARY KEY,
    Product VARCHAR(50),
    SalesAmount DECIMAL(10, 2),
    SaleDate DATE,
    Region VARCHAR(50)
);

INSERT INTO Sales (SaleID, Product, SalesAmount, SaleDate, Region) VALUES
-- North (35 records)
(1, 'Product A', 150.00, '2024-01-10', 'North'),
(2, 'Product A', 160.00, '2024-01-12', 'North'),
(3, 'Product A', 170.00, '2024-01-15', 'North'),
(4, 'Product B', 180.00, '2024-01-20', 'North'),
(5, 'Product B', 190.00, '2024-01-22', 'North'),
(6, 'Product C', 200.00, '2024-02-01', 'North'),
(7, 'Product C', 210.00, '2024-02-05', 'North'),
(8, 'Product D', 220.00, '2024-02-10', 'North'),
(9, 'Product D', 230.00, '2024-02-15', 'North'),
(10, 'Product D', 240.00, '2024-03-01', 'North'),
(11, 'Product E', 250.00, '2024-03-05', 'North'),
(12, 'Product E', 260.00, '2024-03-10', 'North'),
(13, 'Product E', 270.00, '2024-03-15', 'North'),
(14, 'Product F', 280.00, '2024-04-01', 'North'),
(15, 'Product F', 290.00, '2024-04-05', 'North'),
(16, 'Product F', 300.00, '2024-04-10', 'North'),
(17, 'Product G', 310.00, '2024-04-15', 'North'),
(18, 'Product G', 320.00, '2024-05-01', 'North'),
(19, 'Product H', 330.00, '2024-05-10', 'North'),
(20, 'Product H', 340.00, '2024-05-15', 'North'),
(21, 'Product H', 350.00, '2024-06-01', 'North'),
(22, 'Product I', 360.00, '2024-06-05', 'North'),
(23, 'Product I', 370.00, '2024-06-10', 'North'),
(24, 'Product J', 380.00, '2024-07-01', 'North'),
(25, 'Product J', 390.00, '2024-07-10', 'North'),
(26, 'Product J', 400.00, '2024-07-15', 'North'),
(27, 'Product J', 410.00, '2024-08-01', 'North'),
(28, 'Product J', 420.00, '2024-08-10', 'North'),
(29, 'Product A', 430.00, '2024-08-15', 'North'),
(30, 'Product B', 440.00, '2024-09-01', 'North'),
(31, 'Product C', 450.00, '2024-09-05', 'North'),
(32, 'Product D', 460.00, '2024-09-10', 'North'),
(33, 'Product E', 470.00, '2024-09-15', 'North'),
(34, 'Product F', 480.00, '2024-10-01', 'North'),
(35, 'Product G', 490.00, '2024-10-05', 'North'),
(36, 'Product A', 150.00, '2024-01-15', 'South'),
(37, 'Product A', 160.00, '2024-01-20', 'South'),
(38, 'Product B', 170.00, '2024-02-01', 'South'),
(39, 'Product B', 180.00, '2024-02-05', 'South'),
(40, 'Product C', 190.00, '2024-02-15', 'South'),
(41, 'Product C', 200.00, '2024-03-01', 'South'),
(42, 'Product D', 210.00, '2024-03-05', 'South'),
(43, 'Product D', 220.00, '2024-03-10', 'South'),
(44, 'Product E', 230.00, '2024-03-20', 'South'),
(45, 'Product E', 240.00, '2024-04-01', 'South'),
(46, 'Product F', 250.00, '2024-04-10', 'South'),
(47, 'Product F', 260.00, '2024-04-15', 'South'),
(48, 'Product G', 270.00, '2024-05-01', 'South'),
(49, 'Product G', 280.00, '2024-05-10', 'South'),
(50, 'Product H', 290.00, '2024-05-20', 'South'),
(51, 'Product H', 300.00, '2024-06-01', 'South'),
(52, 'Product I', 310.00, '2024-06-10', 'South'),
(53, 'Product I', 320.00, '2024-06-20', 'South'),
(54, 'Product J', 330.00, '2024-07-01', 'South'),
(55, 'Product J', 340.00, '2024-07-10', 'South'),
(56, 'Product J', 350.00, '2024-07-15', 'South'),
(57, 'Product A', 360.00, '2024-08-01', 'South'),
(58, 'Product B', 370.00, '2024-08-10', 'South'),
(59, 'Product C', 380.00, '2024-08-15', 'South'),
(60, 'Product D', 390.00, '2024-09-01', 'South'),
(61, 'Product E', 400.00, '2024-09-10', 'South'),
(62, 'Product F', 410.00, '2024-09-15', 'South'),
(63, 'Product A', 140.00, '2024-01-10', 'East'),
(64, 'Product A', 150.00, '2024-01-15', 'East'),
(65, 'Product B', 160.00, '2024-02-01', 'East'),
(66, 'Product B', 170.00, '2024-02-05', 'East'),
(67, 'Product C', 180.00, '2024-02-15', 'East'),
(68, 'Product C', 190.00, '2024-03-01', 'East'),
(69, 'Product D', 200.00, '2024-03-05', 'East'),
(70, 'Product D', 210.00, '2024-03-10', 'East'),
(71, 'Product E', 220.00, '2024-03-15', 'East'),
(72, 'Product E', 230.00, '2024-04-01', 'East'),
(73, 'Product F', 240.00, '2024-04-10', 'East'),
(74, 'Product F', 250.00, '2024-04-15', 'East'),
(75, 'Product G', 260.00, '2024-05-01', 'East'),
(76, 'Product G', 270.00, '2024-05-10', 'East'),
(77, 'Product H', 280.00, '2024-05-20', 'East'),
(78, 'Product H', 290.00, '2024-06-01', 'East'),
(79, 'Product I', 300.00, '2024-06-10', 'East'),
(80, 'Product I', 310.00, '2024-06-20', 'East'),
(81, 'Product J', 320.00, '2024-07-01', 'East'),
(82, 'Product J', 330.00, '2024-07-10', 'East'),
(83, 'Product A', 340.00, '2024-07-15', 'East'),
(84, 'Product B', 350.00, '2024-08-01', 'East'),
(85, 'Product C', 360.00, '2024-08-10', 'East'),
(86, 'Product D', 370.00, '2024-08-20', 'East'),
(87, 'Product E', 380.00, '2024-09-01', 'East'),
(88, 'Product F', 390.00, '2024-09-10', 'East'),
(89, 'Product G', 400.00, '2024-09-15', 'East'),
(90, 'Product H', 110.00, '2024-01-10', 'West'),
(91, 'Product H', 120.00, '2024-01-20', 'West'),
(92, 'Product I', 130.00, '2024-02-01', 'West'),
(93, 'Product I', 140.00, '2024-02-15', 'West'),
(94, 'Product J', 150.00, '2024-03-01', 'West'),
(95, 'Product J', 160.00, '2024-03-15', 'West'),
(96, 'Product A', 170.00, '2024-04-01', 'West'),
(97, 'Product A', 180.00, '2024-04-15', 'West'),
(98, 'Product B', 190.00, '2024-05-01', 'West'),
(99, 'Product B', 200.00, '2024-05-15', 'West'),
(100, 'Product C', 210.00, '2024-06-01', 'West');

SELECT *FROM new.sys.server_principals
SELECT *FROM sysusers

CREATE LOGIN user1 WITH PASSWORD = 'testing1';
CREATE LOGIN user2 WITH PASSWORD = 'testing2';
USE new;
--To give permission to the user--
CREATE USER user1 FOR LOGIN user1;
CREATE USER user2 FOR LOGIN user2;

-- Grant Select permission to user1--
GRANT SELECT ON Sales TO user1;

-- Grant Select permission to user2--
GRANT SELECT ON Sales TO user2;

-- Grant SELECT and INSERT permissions ot user1
GRANT SELECT, INSERT, UPDATE, DELETE ON Sales TO user2;

-- Revoke SELECT permission from user1
REVOKE SELECT ON Sales FROM user1;

-- Revoke SELECT permission from user2
REVOKE SELECT ON Sales FROM user2;

-- Revoke all permissions from user1
REVOKE SELECT, INSERT, UPDATE, DELETE ON Sales FROM user1;

-- List all the products that have never had sales in the 'west' region
Select Distinct Product 
From Sales
where Product NOT IN (
SELECT distinct Product
From Sales
Where Region = 'West');

-- Better way
SELECT DISTINCT Product
FROM Sales as s
WHERE NOT EXISTS(
SELECT 1
FROM Sales
WHERE Product = s.Product AND Region = 'west' 
);

-- List Regions that have had no sales in the past 60 days

SELECT DISTINCT Region
FROM Sales s
WHERE NOT EXISTS (
SELECT 1
FROM Sales
WHERE Region = s.Region AND SaleDate >= DATEADD(DAY,-60,GETDATE())
);