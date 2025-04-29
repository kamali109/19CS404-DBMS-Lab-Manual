# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3.DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4.RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1.NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2.UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3.CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4.PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5.FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6.DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
```
Create a table named Products with the following columns:

ProductID as INTEGER
ProductName as TEXT
Price as REAL
Stock as INTEGER
For example:

Test	Result
pragma table_info('Products');
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     ProductID   INTEGER     0                       0
1     ProductNam  TEXT        0                       0
2     Price       REAL        0                       0
3     Stock       INTEGER     0

```
SQL code:
```
CREATE TABLE Products(
ProductID INTEGER,
ProductName TEXT,
Price REAL,
Stock INTEGER
);
```
**Output:**

![Screenshot 2025-04-29 204424](https://github.com/user-attachments/assets/e649ecb1-fdea-4809-bc76-bdc27c983a96)


**Question 2**
```
Write a SQL query to add a column named Date_of_birth as Date in the Student_details table.

For example:

Test	Result
pragma table_info('Student_details');
cid    name             type             notnu  dflt_value  pk
-----  ---------------  ---------------  -----  ----------  ----------
0      RollNo           int              0                  1
1      Name             VARCHAR(100)     1                  0
2      Gender           TEXT             1                  0
3      Subject          VARCHAR(30)      0                  0
4      MARKS            INT (3)          0                  0
5      Date_of_birth    Date             0                  0
```
SQL code:
```
ALTER TABLE Student_details
ADD COLUMN Date_of_birth Date;
```
**Output:**

![Screenshot 2025-04-29 211225](https://github.com/user-attachments/assets/f8b02a41-4abc-483a-b2e7-23370fc3b54a)


**Question 3**
```
Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.

For example:

Test	Result
SELECT * FROM Products WHERE ProductID = 101;
ProductID   Name        Category     Price       Stock
----------  ----------  -----------  ----------  ----------
101         Laptop      Electronics  1500        50

```
 SQL code:
```
INSERT INTO Products (ProductID, Name, Category, Price, Stock)
VALUES (101, 'Laptop', 'Electronics', 1500, 50);
```
**Output:**

![Screenshot 2025-04-29 211332](https://github.com/user-attachments/assets/5de5077f-52d3-46d5-91cd-c8ad080abd8b)


**Question 4**

```
Write a SQL query to Add a new column Country as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
For example:

Test	Result
pragma table_info('Student_details');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      int         0                       1
1           Name        VARCHAR(10  1                       0
2           Gender      TEXT        1                       0
3           Subject     VARCHAR(30  0                       0
4           MARKS       INT (3)     0                       0
5           Country     TEXT
```
SQL code 
```
ALTER TABLE Student_details
ADD COLUMN Country TEXT;
```

**Output:**

<img width="410" alt="image" src="https://github.com/user-attachments/assets/34266f21-79a0-4ae8-89d4-7002eb11de0f" />


**Question 5**
```
Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0
For example:

Test	Result
INSERT INTO products (product_id, product_name, list_price) VALUES (2, 'Product B', 50.00);
SELECT * FROM products;
```

 SQL code:
```
CREATE TABLE products(
product_id INTEGER PRIMARY KEY,
product_name TEXT NOT NULL,
list_price DECIMAL (10, 2) NOT NULL,
discount DECIMAL (10, 2) default  0 NOT NULL,
CHECK (list_price >= discount),
CHECK (discount >= 0),
CHECK(list_price >=0)
);
```

**Output:**

<img width="403" alt="image" src="https://github.com/user-attachments/assets/3c09167c-3dde-4088-bbb0-9cac81cba308" />


**Question 6**
```
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

For example:

Test	Result
select * from Books;
ISBN            Title           Author              Publisher      YearPublished
--------------  --------------  ------------------  -------------  -------------
978-1234567890  The Lost World  Arthur Conan Doyle  Vintage Books  1912
978-0987654321  Gone with the   Margaret Mitchell   Macmillan      1936
978-1122334455  Moby Dick       Herman Melville     Harper & Brot  1851
```
 SQL code:
```
INSERT INTO Books( ISBN, Title, Author, Publisher, YearPublished)
SELECT ISBN, Title, Author, Publisher, YearPublished
FROM Out_of_print_books; 
```

**Output:**

<img width="403" alt="image" src="https://github.com/user-attachments/assets/4d4c773e-3d2f-4846-9e4f-d9265389cea7" />


**Question 7**
```
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
For example:

Test	Result
INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (2, 99, 1, '2024-01-03');
Error: FOREIGN KEY constraint failed
```
 SQL code:
```
CREATE TABLE ProjectAssignments(
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
ProjectID INTEGER,
AssignmentDate DATE NOT NULL,
FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)

);
```

**Output:**

<img width="405" alt="image" src="https://github.com/user-attachments/assets/3250fc2b-a6a8-4a26-bd6b-6ef6948d4e0e" />


**Question 8**
```
SQL code:
INSERT INTO Employee (EmployeeID, Name, Position, Department, Salary)
VALUES
(2, 'John Smith', 'Developer', 'IT', 75000),
(3, 'Anna Bell', 'Designer', 'Marketing', 68000);
```

**Output:**

<img width="401" alt="image" src="https://github.com/user-attachments/assets/dfc9a13c-c44c-4fb6-bc00-f1e0ea13b763" />


**Question 9**
```
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.
For example:

Test	Result
INSERT INTO Products
VALUES (1, NULL,0,5);
Error: NOT NULL constraint failed: Products.ProductName
```
SQL code:
```
CREATE TABLE Products(
ProductID INTEGER PRIMARY KEY,
ProductName TEXT NOT NULL,
Price REAL CHECK (Price>0),
Stock INTEGER CHECK (Stock>=0)
);
```

**Output:**

<img width="404" alt="image" src="https://github.com/user-attachments/assets/cdadb856-f4fe-4801-9492-e1404be7ec5d" />


**Question 10**
```
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.
For example:

Test	Result
-- Attempt to insert a record with NULL FirstName
INSERT INTO Employees (EmployeeID, FirstName, LastName, Email, Salary, DepartmentID)
VALUES (1, NULL, 'Doe', 'john.doe@example.com', 50000, 1);
Error: NOT NULL constraint failed: Employees.FirstName
```
SQL code:
```
CREATE TABLE Employees(
EmployeeID INTEGER PRIMARY KEY,
FirstName VARCHAR(50) NOT NULL,
LastName VARCHAR(100) NOT NULL,
Email VARCHAR(30) UNIQUE,
Salary CHECK (Salary>0),
DepartmentID INTEGER,
FOREIGN KEY(DepartmentID) REFERENCES Departments(DepartmentID)
);
```

**Output:**

<img width="418" alt="image" src="https://github.com/user-attachments/assets/c029fba9-0087-42d4-b6c8-db1d880d666f" />

## RESULT

<img width="361" alt="image" src="https://github.com/user-attachments/assets/b4ca3d98-49ff-41fe-aa2b-a664ae61b603" />

Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
