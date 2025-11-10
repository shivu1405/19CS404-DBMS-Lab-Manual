# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER

For example:

Result
id     name             age              city             income
-----  ---------------  ---------------  ---------------  ----------
101    Peter            32               NewYork          200000
102    Mark             32               California       300000
103    Donald           25               Arizona          1000000
104    Obama            35               Florida          5000000
105    Linklon          32               Georgia          250000
107    Adam             35               California       5000000


```sql
SELECT *
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);
```

**Output:**

<img width="1302" height="606" alt="image" src="https://github.com/user-attachments/assets/8dd77a2c-7b02-4092-8f45-2211e466e82e" />


**Question 2**
---
From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
For example:

Result
grade       COUNT(*)
----------  ----------
300         2


```sql
SELECT grade, COUNT(*) 
FROM customer
WHERE grade > (
    SELECT AVG(grade)
    FROM customer
    WHERE city = 'New York'
)
GROUP BY grade;

```

**Output:**

<img width="1289" height="422" alt="image" src="https://github.com/user-attachments/assets/10771f5f-537c-4b7a-a5de-15013e99849d" />


**Question 3**
---
Write a SQL query to List departments with names longer than the average length

Departments Table (attributes: department_id, department_name)

<img width="1080" height="162" alt="image" src="https://github.com/user-attachments/assets/3e70569e-8a4a-43e6-af2f-f14df99f82c4" />


For example:

Result
depar  department_name
-----  ---------------
5      Anesthesiologis


```sql
SELECT department_id, department_name
FROM Departments
WHERE LENGTH(department_name) > (
    SELECT AVG(LENGTH(department_name))
    FROM Departments
);

```

**Output:**

<img width="1285" height="457" alt="image" src="https://github.com/user-attachments/assets/c0b255f5-4899-415c-8e21-158373ca1d51" />

**Question 4**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
2           Khilan      25          Delhi       1500


```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY = 1500;
```

**Output:**
<img width="1255" height="426" alt="image" src="https://github.com/user-attachments/assets/3fda52c7-9e5e-4669-8d28-a585b7bdc496" />


**Question 5**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
4           Chaitali    25          Mumbai      6500
5           Hardik      27          Bhopal      8500
7           Muffy       24          Indore      10000

```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY > 4500;

```

**Output:**

<img width="1274" height="515" alt="image" src="https://github.com/user-attachments/assets/73420b88-3bcb-4ea2-90b5-01885eee71af" />


**Question 6**
---
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)

<img width="932" height="208" alt="image" src="https://github.com/user-attachments/assets/dc172cd2-1318-463c-918e-e3f5db711558" />


For example:

Result
medic  medication_name  dosage
-----  ---------------  ---------------
4      Acetaminophen    600mg


```sql
SELECT medication_id, medication_name, dosage
FROM Medications
WHERE dosage = (
    SELECT MAX(dosage)
    FROM Medications
);
```

**Output:**

<img width="1293" height="492" alt="image" src="https://github.com/user-attachments/assets/bdcff453-bb21-48a0-9998-460e58d01adf" />


**Question 7**
---
From the following tables write a SQL query to find all orders generated by London-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
 

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70009       270.65      2012-09-10  3001         5005

```sql
SELECT
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    o.customer_id,
    o.salesman_id
FROM
    orders o
JOIN
    salesman s
ON
    o.salesman_id = s.salesman_id
WHERE
    s.city = 'London';
```

**Output:**

<img width="1303" height="488" alt="image" src="https://github.com/user-attachments/assets/d361e38b-3a1a-421e-9848-2634f7a06619" />


**Question 8**
---
From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
 

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70011       75.29       2012-08-17  3003         5007


```sql
SELECT
  o.ord_no,        
  o.purch_amt,    
  o.ord_date,     
  o.customer_id,   
  o.salesman_id    
FROM
  orders o        
INNER JOIN
  salesman s       
  ON o.salesman_id = s.salesman_id 
WHERE
  s.name = 'Paul Adam';
```

**Output:**

<img width="1287" height="469" alt="image" src="https://github.com/user-attachments/assets/e0426961-395f-4434-ac29-606eeb688756" />


**Question 9**
---
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
id     name             city             email            phone
-----  ---------------  ---------------  ---------------  ----------
6      Aarti Desai      Pune             aarti@gmail.com  890123456
7      Vivek Sharma     Chandigarh       vivek@gmail.com  980154021
8      Nisha Patel      Noida            nisha@gmail.com  901234567
9      Rajesh Singh     Hyderabad        rajesh@gmail.co  917654301


```sql
SELECT
    id,
    name,
    city,
    email,
    phone
FROM
    customer
WHERE
    city <> (
        SELECT
            city
        FROM
            customer
        WHERE
            id = (SELECT MAX(id) FROM customer)
    );
```

**Output:**

<img width="1284" height="590" alt="image" src="https://github.com/user-attachments/assets/53aca57e-60f7-46f5-bb87-722854027f5d" />


**Question 10**
---
Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)
<img width="755" height="294" alt="image" src="https://github.com/user-attachments/assets/7dfe78e8-f931-454f-aa5f-0cb6a918d6aa" />



For example:

Result
student_id       student_name     subject          grade
---------------  ---------------  ---------------  ---------------
2                Bob              Math             85
6                Frank            Science          85
7                John             Social           85

```sql
SELECT
    T1.*
FROM
    GRADES AS T1
INNER JOIN (
    SELECT
        subject,
        MIN(grade) AS min_grade
    FROM
        GRADES
    GROUP BY
        subject
) AS T2
ON
    T1.subject = T2.subject AND T1.grade = T2.min_grade;
```

**Output:**

<img width="1303" height="539" alt="image" src="https://github.com/user-attachments/assets/eb240da5-f5b0-4dfb-94ce-a781ecbf9eee" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
