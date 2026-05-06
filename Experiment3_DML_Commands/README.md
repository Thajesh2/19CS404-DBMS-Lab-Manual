# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```

**Question 1**

Write a SQL statement to Increase the selling price by 15% in the products table where quantity in stock is less than 50 and supplier ID is 10.

<img width="825" height="197" alt="image" src="https://github.com/user-attachments/assets/e5a4a129-e945-416d-a48c-3a0aa805c63b" />

```
UPDATE Products
SET sell_price = sell_price * 1.15
WHERE quantity < 50 AND supplier_id = 10;
```

**Output:**

<img width="1376" height="284" alt="image" src="https://github.com/user-attachments/assets/fa0751c9-c598-45fc-9716-ae8316cbea7b" />

**Question 2**

Write a SQL statement to Double the salary for employees in department 20 who have a job_id ending with 'MAN'

<img width="688" height="126" alt="image" src="https://github.com/user-attachments/assets/fc293567-8208-4e6e-b292-4b95453eb1b9" />

```
UPDATE Employees
SET salary = salary * 2
WHERE department_id = 20
  AND job_id LIKE '%MAN';
```

**Output:**

<img width="942" height="211" alt="image" src="https://github.com/user-attachments/assets/e08a9039-dcc7-420d-918e-9674ad27003e" />

**Question 3**

Write a SQL statement to Update the product_name to 'Premium Bread' whose product ID is 5 in the products table.

<img width="227" height="155" alt="image" src="https://github.com/user-attachments/assets/6e85f8e5-4ab7-4e3b-874d-4505a0671f3c" />

```
UPDATE Products
SET product_name = 'Premium Bread'
WHERE product_id = 5;
```

**Output:**

<img width="1176" height="228" alt="image" src="https://github.com/user-attachments/assets/63c9ce64-bfcd-4f81-839a-e201f9cd3233" />

**Question 4**

Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.

<img width="221" height="161" alt="image" src="https://github.com/user-attachments/assets/e36c242c-54e2-4188-b09c-e7eee7c6e8f3" />

```
UPDATE Products
SET sell_price = sell_price * 1.10
WHERE category = 'Bakery';
```

**Output:**

<img width="1246" height="295" alt="image" src="https://github.com/user-attachments/assets/faa27db7-027a-4167-a409-62406ad480ee" />

**Question 5**

Write a SQL statement to change the EMAIL and COMMISSION_PCT column of the following EMPLOYEES table with 'not available' and 0.55 for those employees whose DEPARTMENT_ID is 110.

<img width="575" height="108" alt="image" src="https://github.com/user-attachments/assets/6cdae6bb-ace8-4511-a5ae-2dcc81246450" />

```
UPDATE Employees
SET email = 'not available',
    commission_pct = 0.55
WHERE department_id = 110;
```

**Output:**

<img width="888" height="215" alt="image" src="https://github.com/user-attachments/assets/0d4c6728-3bd2-4851-8e1d-0a4f4f2289c5" />

**Question 6**

Write a SQL query to Delete customers from 'customer' table where 'GRADE' is not equal to 3.

<img width="771" height="283" alt="image" src="https://github.com/user-attachments/assets/0766bfc8-4bdb-484a-b887-93a56aa4472d" />

```
DELETE FROM Customer
WHERE GRADE <> 3;
```

**Output:**

<img width="400" height="303" alt="image" src="https://github.com/user-attachments/assets/09606b50-664c-4ab3-9dd2-3f0d5a6abf1b" />

**Question 7**

Write a SQL query to Delete customers from 'customer' table where 'GRADE' is odd.

<img width="761" height="215" alt="image" src="https://github.com/user-attachments/assets/99616d41-dcda-45d9-b8e4-1ab24fb337cb" />

```
DELETE FROM Customer
WHERE GRADE % 2 = 1;
```

**Output:**

<img width="1058" height="165" alt="image" src="https://github.com/user-attachments/assets/409db034-4e9c-4de8-85ba-9d01f421aef5" />

**Question 8**

Write a SQL query to delete a specific doctor from Doctors table whose ID is 1.

<img width="338" height="72" alt="image" src="https://github.com/user-attachments/assets/5dc7a318-64d5-44e9-8590-bd18433e5c43" />

```
DELETE FROM Doctors
WHERE doctor_id = 1;
```

**Output:**

<img width="649" height="158" alt="image" src="https://github.com/user-attachments/assets/bed92dbd-1987-4cb8-ae5f-aa2648726d4e" />

**Question 9**

Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.

<img width="389" height="246" alt="image" src="https://github.com/user-attachments/assets/e0f27b3e-2e38-4b2f-ae1a-ddc47c07a4ee" />

```
DELETE FROM Doctors
WHERE doctor_id BETWEEN 2 AND 4;
```

**Output:**

<img width="665" height="461" alt="image" src="https://github.com/user-attachments/assets/06af7e99-66ed-48a9-a853-d53dd59528e7" />

**Question 10**

Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.

<img width="310" height="69" alt="image" src="https://github.com/user-attachments/assets/ec0dc740-fb7d-4812-91bd-da6b9b9e1bc6" />

```
DELETE FROM Doctors
WHERE specialization = 'Pediatrics'
  AND first_name = 'Michael';
```

**Output:**

<img width="649" height="217" alt="image" src="https://github.com/user-attachments/assets/5206ef44-29f8-4bc4-a67a-70febbc36a85" />

## RESULT

Thus, the SQL queries to implement DML commands have been executed successfully.
