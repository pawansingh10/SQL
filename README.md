# SQL
Understanding of SQL


## **SQL Interview Questions**
***

### **SQL Query to find the Nth highest Salary**
- **EMP**
- |Id|Salary|
  |----|------|
  |1  | 10000|
  |2  | 20000|
  |3  | 20000|
  |4  | 30000|
  |5  | 40000|
  |6  | 50000|

- Find Highest Salary from table EMP
  
- ```sql
     SELECT MAX(Salary) FROM EMP;  // 50000
   ```
 
- Find Second Highest Salary from this table EMP
- ```sql
    SELECT MAX(Salary) FROM EMP WHERE Salary NOT IN (SELECT MAX(SALARY) FROM EMP);   // 40000
  ```

- Find the nth Highest salary from the table EMP
- ```sql
     SELECT Id,Salary from EMP e1 WHERE N-1=(SELECT COUNT(DISTINCT Salary) FROM e2 WHERE e2.Salary > e1.Salary)
  ``` 

> ***Co-related nested Query, recognizes by where the outer query's value used in inner***

-    e1          and           e2

- |Id|Salary|     |        |Id|Salary|
  |----|------|-----|----- |----|------|
  |1  | 10000|      |      |1  | 10000|
  |2  | 20000|      |      |2  | 20000|
  |3  | 20000|      |      |3  | 20000|
  |4  | 30000|      |      |4  | 30000|
  |5  | 40000|      |      |5  | 40000|
  |6  | 50000|      |      |6  | 50000|
 
- Here e2.salary is compare by all e1.salary
- For duplicate value we use DISTINCT otherwise without distinct it works fine!
- For Example we have to find 4th Highest salary then put N=4
- ```sql 
     SELECT Id,Salary from EMP e1 WHERE 4-1=(SELECT COUNT(DISTINCT Salary) FROM e2 WHERE e2.Salary > e1.Salary)
  ```
- compare 3=count given by sub-query
  
   
  
  






### **SQL Query to delete duplicate rows from a Table**

### **Join in SQL**

### **Constraints in SQL**
Not NULL
Unique
Check
Default
Primary-Key
Foreign-Key

### **Aggregate Functions**
count()
sum()
avg()
max()
min()

### **Keys in DBMS**
* **Primary-Key**
* **Foreign-Key**
* **Composite-Key**
* **Super-Key**
* **Candidate Key**
* **Secondary-Key**


### **What is Normalization? Why is it used?**


### **Differents types of SQL Commands**

* **DDL - Data Definition Language**
  - **Create**
  - **Alter**
  - **Rename**
  - **Drop**
  - **Truncate**

* **DML - Data Manipulation Language**
  - **Insert**
  - **Delete**
  - **Update**

* **DCL - Data Control Language**
  - **Grant**
  - **Revoke**

* **TCL - Transaction Control Language**
  - **Commit**
  - **RollBack**
  - **SavePoint**
 
 
### **Difference between delete, truncate and drop**


### **Different between Char and VarChar**

### **Difference between Union and Join**

### **Difference between In and Exists**

### **How to create empty table with the same structure as another table?**
- SELECT * INTO students_copy FROM students WHERE 1==2;

### **What is pattern matching in SQL?**
- % Wildcard + LIKE operator
- SELECT * FROM students WHERE name LIKE '-K%'; 

### **What is Union, Minus and Intersect**
- SELECT name FROM students    UNION   SELECT name FROM contacts;

### **Difference between Union and Union All**
