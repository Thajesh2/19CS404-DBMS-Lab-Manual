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
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
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
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
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

Insert all students from Archived_students table into the Student_details table.

```
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0
```

<img width="802" height="221" alt="image" src="https://github.com/user-attachments/assets/1d134479-3e33-49ab-bab4-a92e3a26f59d" />

```
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
SELECT RollNo, Name, Gender, Subject, MARKS
FROM Archived_students;
```

**Output:**

<img width="808" height="142" alt="image" src="https://github.com/user-attachments/assets/be2be22c-9e03-4eb8-a6ff-bd15268c5993" />

**Question 2**

Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.

<img width="821" height="159" alt="image" src="https://github.com/user-attachments/assets/58670dfd-01a1-401a-a702-2914a64e6d5d" />

```
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES (201, 'David Lee', 'M', 'Physics', 92);
```

**Output:**

<img width="1282" height="223" alt="image" src="https://github.com/user-attachments/assets/66e4df33-d039-4d1e-b830-67691f7bd3f3" />

**Question 3**

Write a SQL Query for inserting the below values in the table Customers

```
ID               NAME             AGE  ADDRESS     SALARY      
---------------  ---------------  ---  ----------  ----------  
1                Ramesh           32   Ahmedabad   2000
2                Khilan           25   Delhi       1500
3                Kaushik          23   Kota        2000
```

<img width="604" height="191" alt="image" src="https://github.com/user-attachments/assets/f7ea9f75-f226-47d5-b94c-e297d1118ff7" />

```
INSERT INTO Customers (ID, NAME, AGE, ADDRESS, SALARY)
VALUES 
(1, 'Ramesh', 32, 'Ahmedabad', 2000),
(2, 'Khilan', 25, 'Delhi', 1500),
(3, 'Kaushik', 23, 'Kota', 2000);
```

**Output:**

<img width="1089" height="257" alt="image" src="https://github.com/user-attachments/assets/682c065b-a341-4c99-92c8-bb3f44ea2535" />

**Question 4**

Create a table named Orders with the following constraints: OrderID as INTEGER should be the primary key. OrderDate as DATE should be not NULL. CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

<img width="1116" height="147" alt="image" src="https://github.com/user-attachments/assets/cb9e7099-b825-4e19-af0a-dd60d79b082f" />

```
CREATE TABLE Orders (
    OrderID     INTEGER PRIMARY KEY,
    OrderDate   DATE NOT NULL,
    CustomerID  INTEGER,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

**Output:**

<img width="1312" height="233" alt="image" src="https://github.com/user-attachments/assets/546d9a40-0333-4120-9983-6ba1442b4e82" />

**Question 5**

Create a table named Products with the following constraints:

ProductID should be the primary key. ProductName should be NOT NULL. Price is of real datatype and should be greater than 0. Stock is of integer datatype and should be greater than or equal to 0.

<img width="523" height="130" alt="image" src="https://github.com/user-attachments/assets/bd9e5d30-8032-4791-836d-1b71b94db533" />

```
CREATE TABLE Products (
    ProductID   INTEGER PRIMARY KEY,
    ProductName VARCHAR(100) NOT NULL,
    Price       REAL CHECK (Price > 0),
    Stock       INTEGER CHECK (Stock >= 0)
);
```

**Output:**

<img width="951" height="221" alt="image" src="https://github.com/user-attachments/assets/3afb133a-f642-4029-8eaf-60a3efc6dfd7" />

**Question 6**

Create a table named Department with the following constraints: DepartmentID as INTEGER should be the primary key. DepartmentName as TEXT should be unique and not NULL. Location as TEXT.

<img width="924" height="142" alt="image" src="https://github.com/user-attachments/assets/1dc7f45f-cd52-492e-bddf-164d5dbb11c2" />

```
CREATE TABLE Department (
    DepartmentID   INTEGER PRIMARY KEY,
    DepartmentName TEXT UNIQUE NOT NULL,
    Location       TEXT
);
```

**Output:**

<img width="1209" height="177" alt="image" src="https://github.com/user-attachments/assets/32109871-8584-4fd1-9513-f709d7fd02a3" />

**Question 7**

Create a table named Shipments with the following constraints: ShipmentID as INTEGER should be the primary key. ShipmentDate as DATE. SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID). OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

<img width="885" height="111" alt="image" src="https://github.com/user-attachments/assets/2a625ed7-9386-495e-b123-d20c595928c8" />

```
CREATE TABLE Shipments (
    ShipmentID   INTEGER PRIMARY KEY,
    ShipmentDate DATE,
    SupplierID   INTEGER,
    OrderID      INTEGER,
    FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1150" height="195" alt="image" src="https://github.com/user-attachments/assets/ce970f67-f544-47cf-8ae4-e25a609cfe6a" />

**Question 8**

Write a SQL query to Add a new ParentsNumber column as number and Adhar_Number as Number in the Student_details table.

<img width="694" height="233" alt="image" src="https://github.com/user-attachments/assets/48a30c99-1f91-4c74-b968-07a4689a3345" />

```
ALTER TABLE Student_details
ADD COLUMN ParentsNumber number;

ALTER TABLE Student_details
ADD COLUMN Adhar_Number number;
```

**Output:**

<img width="1204" height="301" alt="image" src="https://github.com/user-attachments/assets/7be65501-c600-4219-be71-8f7165ef51b2" />

**Question 9**

Write a SQL query to Add a new column Country as text in the Student_details table.

Sample table: Student_details

```
cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
```

<img width="684" height="222" alt="image" src="https://github.com/user-attachments/assets/ff6f1ce1-30ab-4a86-82b1-5cdebe9d4742" />

```
ALTER TABLE Student_details
ADD COLUMN Country TEXT;
```
**Output:**

<img width="1196" height="275" alt="image" src="https://github.com/user-attachments/assets/d6744049-45fb-4f76-86e9-f87d1f4d8695" />

**Question 10**

Create a table named Members with the following columns:

MemberID as INTEGER MemberName as TEXT JoinDate as DATE

<img width="669" height="182" alt="image" src="https://github.com/user-attachments/assets/3da241a6-15e0-441b-9346-0d1535077d80" />

```
CREATE TABLE Members (
    MemberID   INTEGER,
    MemberName TEXT,
    JoinDate   DATE
);
```
**Output:**

<img width="1304" height="287" alt="image" src="https://github.com/user-attachments/assets/cf056767-dd74-496a-8cc8-04de10c07fa8" />

## RESULT:

Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
