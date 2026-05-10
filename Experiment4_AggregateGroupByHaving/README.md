# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
How many appointments are scheduled for each patient?

Sample table: Appointments Table

name                  type
--------------------  ----------
AppointmentID         INTEGER
PatientID             INTEGER
DoctorID              INTEGER
AppointmentDateTime   DATETIME
Purpose               TEXT
Status                TEXT
For example:

Result
PatientID   TotalAppointments
----------  -----------------
3           3
5           2
6           1
7           1
10          3


```
SELECT PatientID, COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY PatientID;
```

**Output:**

<img width="782" height="682" alt="image" src="https://github.com/user-attachments/assets/03d0b28b-7d3d-4425-9a68-6b18e9d38a8a" />

**Question 2**
Write SQL query to extract the email domain from each patient's email address and count the number of patients with the same email domain.

Sample table: Patients Table



For example:

Result
EmailDomain  TotalPatients
-----------  -------------
example.com  10
```
SELECT 
    substr(email, instr(email, '@') + 1) AS EmailDomain,
    COUNT(*) AS TotalPatients
FROM Patients
GROUP BY EmailDomain;
```

**Output:**

<img width="712" height="436" alt="image" src="https://github.com/user-attachments/assets/58e85158-fc5b-4743-8b8f-4ac069e6e7fa" />

**Question 3**
How many prescriptions were written by each doctor?

Sample tablePrescriptions Table



For example:

Result
DoctorID    TotalPrescriptions
----------  ------------------
1           1
2           1
3           1
4           1
5           1
6           1
7           1
8           1
9           1
10          1
```
SELECT DoctorID, COUNT(*) AS TotalPrescriptions
FROM Prescriptions
GROUP BY DoctorID;
```

**Output:**

<img width="768" height="830" alt="image" src="https://github.com/user-attachments/assets/f0fc2a10-c318-4756-bab2-8a492d71de02" />

**Question 4**
Write a SQL query to calculate the average purchase amount of all orders. Return average purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
AVERAGE
----------
1461.765
```
SELECT AVG(purch_amt) AS AVERAGE
FROM orders;
```
**Output:**

<img width="406" height="385" alt="image" src="https://github.com/user-attachments/assets/f2a39fe1-b2a0-4d24-8773-13af817ee526" />

**Question 5**
Write a SQL query to find the average length of names for people living in Chennai?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
avg_name_length
---------------
10.0
```
SELECT AVG(LENGTH(name)) AS avg_name_length
FROM customer
WHERE city = 'Chennai';
```

**Output:**

<img width="468" height="387" alt="image" src="https://github.com/user-attachments/assets/64787b13-8139-4a7a-afd0-c23e493379db" />


**Question 6**
Write a SQL query to count the number of customers. Return number of customers.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

 

For example:

Result
COUNT
----------
8
```
SELECT COUNT(*) AS COUNT
FROM customer;
```

**Output:**

<img width="392" height="387" alt="image" src="https://github.com/user-attachments/assets/402a1489-659c-4722-a731-d6176aba2217" />

**Question 7**
Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
avg_income
----------
5000000.0
```
SELECT AVG(income) AS avg_income
FROM employee
WHERE name LIKE 'A%';
```

**Output:**

<img width="393" height="397" alt="image" src="https://github.com/user-attachments/assets/fb461401-874a-476f-9afb-9888f0d8c661" />

**Question 8**
Write the SQL query that achieves the grouping of data by city, calculates the total income for each city, and includes only those cities where the total income sum is greater than 200,000.

Sample table: employee



For example:

Result
city        Income
----------  ----------
Alaska      450000
Arizona     1000000
California  5300000
Florida     5350000
Georgia     250000
```
SELECT city, SUM(income) AS Income
FROM employee
GROUP BY city
HAVING SUM(income) > 200000;
```

**Output:**

<img width="610" height="610" alt="image" src="https://github.com/user-attachments/assets/6bfaf1c4-4803-4c30-bd1b-edbe9f1a57cd" />

**Question 9**
Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

Sample table: customer1



For example:

Result
address     SUM(salary)
----------  -----------
Bhopal      8500
Hyderabad   4500
Indore      10000
Mumbai      6500
```
SELECT address, SUM(salary) AS "SUM(salary)"
FROM customer1
GROUP BY address
HAVING SUM(salary) > 2000;
```

**Output:**

<img width="610" height="558" alt="image" src="https://github.com/user-attachments/assets/0966d716-d55a-45b2-b578-cd4c0c18ed1e" />

**Question 10**
Write a SQL query to identify the cities (addresses) where the average salary is greater than Rs. 5000, as per the "customer1" table.

Sample table: customer1



For example:

Result
address     AVG(salary)
----------  -----------
Bhopal      8500.0
Indore      10000.0
Mumbai      6500.0
```
SELECT address, AVG(salary) AS "AVG(salary)"
FROM customer1
GROUP BY address
HAVING AVG(salary) > 5000;
```

**Output:**

<img width="647" height="508" alt="image" src="https://github.com/user-attachments/assets/5cfc4320-8bd0-46c9-ae92-89ba5820a65c" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
