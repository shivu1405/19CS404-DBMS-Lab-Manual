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
--
ow many prescriptions were written in each frequency category (e.g., once daily, twice daily)?

Sample tablePrescriptions Table
<img width="944" height="129" alt="image" src="https://github.com/user-attachments/assets/21a38d85-fd4c-4c8a-ae73-47538d4a732b" />




For example:

Result
Frequency      TotalPrescriptions
-------------  ------------------
Every 3 weeks  1
Every 6 hours  1
Once           1
Once daily     4
Once daily at  1
Pending        1
Twice daily    1


```sql
SELECT
    Frequency,
    COUNT(*) AS TotalPrescriptions
FROM
    Prescriptions
GROUP BY
    Frequency;
```

**Output:**
<img width="1245" height="623" alt="image" src="https://github.com/user-attachments/assets/53d7a55a-d952-4763-b896-fee4b7321dba" />


**Question 2**
---
What is the most common diagnosis among patients?

Sample table:MedicalRecords Table
<img width="955" height="145" alt="image" src="https://github.com/user-attachments/assets/0fc1484c-25e6-43c2-b163-e0c9aa4d44d1" />



For example:

Result
Diagnosis              DiagnosisCount
---------------------  --------------
Childhood vaccination  3


```sql
SELECT Diagnosis, COUNT(*) AS DiagnosisCount
FROM MedicalRecords
GROUP BY Diagnosis
ORDER BY DiagnosisCount DESC
LIMIT 1;
```

**Output:**

<img width="1245" height="404" alt="image" src="https://github.com/user-attachments/assets/4845d270-b292-4618-8fd2-4bcef2d53609" />


**Question 3**
---
How many medical records does each doctor have?

Sample table:MedicalRecords Table
<img width="963" height="140" alt="image" src="https://github.com/user-attachments/assets/6e51a811-1940-46d9-91c9-f3e19e5f1427" />



For example:

Result
DoctorID    TotalRecords
----------  ------------
3           4
5           1
6           1
7           1
8           3


```sql
SELECT DoctorID, COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY DoctorID;
```

**Output:**

<img width="1233" height="701" alt="image" src="https://github.com/user-attachments/assets/58b016e3-bff7-4557-9095-d8ce34609cd9" />


**Question 4**
---
Write a SQL query to find the customer with longest name?

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
name          length
------------  ----------
Preeti Patel  12


```sql
SELECT name, LENGTH(name) AS length
FROM customer
ORDER BY length DESC
LIMIT 1;
```

**Output:**

<img width="1243" height="396" alt="image" src="https://github.com/user-attachments/assets/8976d26d-30dc-4d8a-ad26-9b4ade0268a7" />


**Question 5**
---
Write a SQL query to find Who has the highest income among employee living in California?

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
name        max(income)
----------  -----------
Adam        5000000


```sql
SELECT name,max(income)
FROM employee
WHERE city = 'California';
```

**Output:**

<img width="1235" height="407" alt="image" src="https://github.com/user-attachments/assets/fe6e92bc-fc5f-4a56-b30f-384403fa3a9e" />


**Question 6**
---
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



```sql
SELECT AVG(LENGTH(name)) AS avg_name_length
FROM customer
WHERE city = 'Chennai';
```

**Output:**

<img width="1251" height="413" alt="image" src="https://github.com/user-attachments/assets/16e12001-ffe9-49b3-bd82-f2a8023233b6" />


**Question 7**
---
Write a SQL query to calculate the total number of working hours of all employees

Sample table: employee1
<img width="853" height="163" alt="image" src="https://github.com/user-attachments/assets/27cd4f7a-c215-4a3b-bd58-17c83256cc13" />



 

For example:

Result
Total working hours
-------------------
111


```sql
SELECT SUM(workhour) AS "Total working hours"
FROM employee1;
```

**Output:**

<img width="1241" height="406" alt="image" src="https://github.com/user-attachments/assets/868da490-c721-470e-84fb-adaf3326a022" />


**Question 8**
---
Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

Sample table: customer1
<img width="779" height="129" alt="image" src="https://github.com/user-attachments/assets/d9b86a7e-c850-41b0-a21a-ba8081b8bfc8" />



For example:

Result
address     SUM(salary)
----------  -----------
Bhopal      8500
Hyderabad   4500
Indore      10000
Mumbai      6500


```sql
SELECT address, SUM(salary)
FROM customer1
GROUP BY address
HAVING SUM(salary)>2000;
```

**Output:**



**Question 9**
---
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 400,000.

Sample table: employee
<img width="779" height="163" alt="image" src="https://github.com/user-attachments/assets/13abaf2a-3f69-47c7-9815-b176b92855ae" />



For example:

Result
age         MIN(income)
----------  -----------
32          200000
40          350000


```sql
SELECT age,MIN(income)
FROM employee
GROUP BY age
HAVING MIN(income) < 400000 ;
```

**Output:**


**Question 10**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the minimum work hours for each date, and excludes dates where the minimum work hour is not less than 10.

Sample table: employee1
<img width="780" height="148" alt="image" src="https://github.com/user-attachments/assets/e2433331-e38e-4fda-bfea-51de375a693a" />



For example:

Result
jdate       MIN(workhour)
----------  -------------
2002.0      9
2004.0      9
2006.0      9


```sql
SELECT jdate,MIN(workhour)
FROM employee1
GROUP BY jdate
HAVING MIN(workhour) < 10;
```

**Output:**

<img width="1227" height="524" alt="image" src="https://github.com/user-attachments/assets/9f31f954-600a-4a93-99af-ba42716d9ed3" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
