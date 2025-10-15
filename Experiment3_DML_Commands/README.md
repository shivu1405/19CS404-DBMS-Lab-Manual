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
--
Write a SQL statement to retrieve city(column name) of all customers from customers table without any repeats.

 

 

For example:

Result
city
----------
Chennai
California
Berlin
Moscow

```sql
SELECT DISTINCT city FROM customers;
```

**Output:**

<img width="1256" height="596" alt="image" src="https://github.com/user-attachments/assets/949a36ad-9801-490e-84fe-97e1eb6ce52e" />

**Question 2**
---
Write a SQL statement to Change the category to 'Household' where product name contains 'Detergent' in the products table.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT        
supplier_id    INT           
For example:

Test	Result
select changes();
changes()
----------
4

```sql
UPDATE Products
SET category = 'Household'
WHERE product_name LIKE '%Detergent%';```
```
**Output:**

<img width="1246" height="590" alt="image" src="https://github.com/user-attachments/assets/a1433378-f9a3-4023-9a2f-9ab7d04f99b2" />

**Question 3**
---
Write a SQL statement to Change the supplier name to 'A1 Suppliers' where the supplier ID is 8 in the suppliers table.

Table info

suppliers(supplier_id,supplier_name,contact_person,phone_number,email,address)

For example:

Test	Result
select changes();
changes()
----------
1
```sql
UPDATE suppliers SET supplier_name = 'A1 Suppliers' WHERE supplier_id = 8;
```

**Output:**

<img width="1232" height="484" alt="image" src="https://github.com/user-attachments/assets/28451254-bcde-4f78-9dc5-e474b566bbb7" />

**Question 4**
---
Write a SQL statement to double the availability of the product with product_id 1.

products table

---------------
product_id
product_name
category_id
availability

```sql
UPDATE products SET availability = availability * 2 WHERE product_id = 1;
```

**Output:**

<img width="1253" height="313" alt="image" src="https://github.com/user-attachments/assets/de9f9a5f-5d59-4c4a-8154-60fd488ac574" />

**Question 5**
---
Write a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in the products table.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT        
supplier_id    INT               
For example:

Test	Result
--pragma table_info('products');
select changes();
changes()
----------
2


```sql
UPDATE products
SET reorder_lvl = reorder_lvl *0.70
WHERE cost_price > 50 AND quantity < 100;
```

**Output:**

<img width="1250" height="559" alt="image" src="https://github.com/user-attachments/assets/b8747223-da48-483c-a8ad-0c1bfc8aa0db" />

**Question 6**
---
Write a SQL query to remove rows from the table 'customer' with the following condition -

1. 'cust_city' should begin with the letter 'L',

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
SELECT * FROM customer WHERE cust_country='UK';
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00013      Holmes      London      London        UK            2           6000         5000         7000         4000             BBBBBBB     A003
C00024      Cook        London      London        UK            2           4000         9000         7000         6000             FSDDSDF     A006
C00015      Stuart      London      London        UK            1           6000         8000         3000         11000            GFSGERS     A003
C00023      Karl        London      London        UK            0           4000         6000         7000         3000             AAAABAA     A006
C00010      Charles     Hampshair   Hampshair     UK            3           6000         4000         5000         5000             MMMMMMM     A009
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00010      Charles     Hampshair   Hampshair     UK            3           6000         4000            5000         5000             MMMMMMM     A009


```sql
DELETE FROM Customer
WHERE cust_city LIKE 'L%';
```

**Output:**

<img width="1225" height="900" alt="image" src="https://github.com/user-attachments/assets/863e0b01-a4f2-46b2-86c0-fc5910de75a3" />


**Question 7**
---
Write a SQL query to remove rows from the table 'customer' with the following condition -

1. 'cust_country' must be 'India',

2. 'cus_city' must not be 'Chennai',

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
SELECT * FROM customer WHERE cust_country='India';
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00025      Ravindran   Bangalore   Bangalore     India         2           5000         7000         4000         8000             AVAVAVA     A011
C00019      Yearannaid  Chennai     Chennai       India         1           8000         7000         7000         8000             ZZZZBFV     A010
C00005      Sasikant    Mumbai      Mumbai        India         1           7000         11000        7000         11000            147-258963  A002
C00007      Ramanathan  Chennai     Chennai       India         1           7000         11000        9000         9000             GHRDWSD     A010
C00022      Avinash     Mumbai      Mumbai        India         2           7000         11000        9000         9000             113-123456  A002
C00017      Srinivas    Bangalore   Bangalore     India         2           8000         4000         3000         9000             AAAAAAB     A007
C00009      Ramesh      Mumbai      Mumbai        India         3           8000         7000         3000         12000            Phone No    A002
C00014      Rangarappa  Bangalore   Bangalore     India         2           8000         11000        7000         12000            AAAATGF     A001
C00016      Venkatpati  Bangalore   Bangalore     India         2           8000         11000        7000         12000            JRTVFDD     A007
C00011      Sundariya   Chennai     Chennai       India         3           7000         11000        7000         11000            PPHGRTS     A010
CUST_CODE   CUST_NAME    CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  -----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00019      Yearannaidu  Chennai     Chennai       India         1           8000         7000         7000         8000             ZZZZBFV     A010
C00007      Ramanathan   Chennai     Chennai       India         1           7000         11000        9000         9000             GHRDWSD     A010
C00011      Sundariya    Chennai     Chennai       India         3           7000         11000        7000         11000            PPHGRTS     A010


```sql
DELETE FROM customer WHERE cust_country = 'India' AND cust_city != 'Chennai';
```

**Output:**

<img width="1244" height="908" alt="image" src="https://github.com/user-attachments/assets/76be1378-5829-4fdc-bb46-cbb23576d84a" />


**Question 8**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is odd.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
14


```sql
DELETE FROM customer WHERE GRADE % 2 = 1;
```

**Output:**

<img width="1229" height="523" alt="image" src="https://github.com/user-attachments/assets/c2b8b2f6-fe72-4048-b6b6-7bc5488e89f1" />


**Question 9**
---
Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
For example:

Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology


```sql
DELETE FROM Doctors
WHERE doctor_id BETWEEN 2 AND 4;
```

**Output:**
<img width="1237" height="892" alt="image" src="https://github.com/user-attachments/assets/007d9d6c-1fb1-4563-bb44-6dc99467eb41" />


**Question 10**
---
Write a SQL query to Delete All Doctors with a NULL Last Name

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
For example:

Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
4           Febin                   Cardiology
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics


```sql
DELETE FROM Doctors
WHERE last_name IS NULL;
```

**Output:**
<img width="1243" height="794" alt="image" src="https://github.com/user-attachments/assets/d01493ab-edb4-4085-8642-b53384428991" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
