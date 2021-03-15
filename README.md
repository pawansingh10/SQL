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

- |Id |First_Name|Last_name|
  |---|----------|---------|
  |1  |Amit      | Kumar   |
  |2  |Rahul     | Jain    |
  |3  |Akhil     | Karn   |
  |4  |Rahul     | Jain   |
  |5  |Maaz      | Ahmed  |
    
- Check for Duplicate
- ```sql
   SELECT first_name,last_name,count(*) from emp GROUP BY first_name,last_name HAVING COUNT(*) > 1;
  ```

- Delete Duplicate by deleting
- ```sql
      DELETE FROM emp e1  
      INNER JOIN  emp e2
      ON e1.first_name=e2.first_name AND e1.last_name=e2.last_name
      WHERE e1.Id < e2.Id;
      
  ```

- Create another table which has no duplicate values
- ```sql
     CREATE TABLE new_emp AS 
     SELECT Id,First_Name,Last_name
     FROM emp
     GROUP BY First_Name,Last_Name;
  ```
  
 - Another way using Row_Number() function
 - ```sql
      WITH newEmp AS
      (
        SELECT *, ROW_NUMBER() OVER(PARTITION BY Id ORDER BY Id) as row_number FROM emp;
      )
      DELETE FROM emp WHERE row_number > 1;
   ```








### **Join in SQL**
***
- ***A JOIN clause is used to combine rows from two or more tables, based on a related column between them.***
- ***JOIN apply when there is something must be common atleast 1 attribute***
- ***JOIN = CROSS_Product + Condition (select)***

#### Different Types of SQL JOINs
* **INNER JOIN**
  -  Returns records that have matching values in both tables
  -  ```sql
     SELECT column_name
     FROM table1
     INNER JOIN table2
     ON table1.column_name = table2.column_name;
     ```
  
* **LEFT OUTER JOIN**
  - Returns all records from the left table, and the matched records from the right table
  
* **RIGHT OUTER JOIN**
  - Returns all records from the right table, and the matched records from the left table

* **FULL OUTER JOIN**
  - Returns all records when there is a match in either left or right table





### **Constraints in SQL**
Not NULL
Unique
Check
Default
Primary-Key
Foreign-Key

### **Aggregate Functions**
- Aggregate function is a function where the values of multiple rows are grouped together

- **count()**
  - Returns total count of records 
  - Return number of Non Null values

- **sum()**
  - Sum all Non Null values of Column salary

- **avg()**
  - Avg(salary) = Sum(salary) / count(salary) 

- **max()**
  - Maximum value in the salary 

- **min()**
  - Minimum value in the salary column except NULL 

### **SELECT Statement**
___
- The SELECT statement is used to select data from a database.

- Syntax 
```sql
     SELECT column1, column2, ...
     FROM table_name;
```

- SQL statement selects the "CustomerName" and "City" columns from the "Customers" table:
```sql
   SELECT CustomerName, City FROM Customers;
```

- SQL statement selects all the columns from the "Customers" table:
```sql
   SELECT * FROM Customers;
```

### **SELECT DISTINCT Statement**
___
- The SELECT DISTINCT statement is used to return only distinct (different) values.

- Syntax
```sql
     SELECT DISTINCT column1, column2, ...
     FROM table_name;
```

- SQL statement selects only the DISTINCT values from the "Country" column in the "Customers" table:

```sql
   SELECT DISTINCT Country FROM Customers;
```

- SQL statement lists the number of different (distinct) customer countries:
```sql
   SELECT COUNT(DISTINCT Country) FROM Customers;
```

### **WHERE Clause**
***

- The WHERE clause is used to filter records.

- Syntax
```sql
   SELECT column1, column2, ...
      FROM table_name 
   WHERE condition;
```
> ***Note : The WHERE clause is not only used in SELECT statements, it is also used in UPDATE, DELETE, etc.!***

- SQL statement selects all the customers from the country "Mexico", in the "Customers" table
```sql
   SELECT * FROM Customers
   WHERE Country='Mexico';
```

> ***Operators in The WHERE Clause***

|Operator | Discription|
|---------|------------|
| = | Equal|
| > | Greater than |
| < | Less than |
| >= | Greater the Equal to|
| <= | Less than Equal to|
| != or <> | Not Equal to |
| BETWEEN | Between Certain Range |
| LIKE    | Search for a Pattern |
| IN      | To specify multiple possible value from a column |


- ***The SQL AND, OR and NOT Operators***
  - The WHERE clause can be combined with AND, OR, and NOT operators.
  
  - AND Syntax with WHERE
  ```sql
  SELECT column1, column2, ...
    FROM table_name
  WHERE condition1 AND condition2 AND condition3 ...;
  ```
  
  - OR Syntax with WHERE
  ```sql
     SELECT column1, column2, ...
        FROM table_name
     WHERE condition1 OR condition2 OR condition3 ...;
  ```
  
  - NOT Syntax with WHERE
  ```sql
     SELECT column1, column2, ...
        FROM table_name
     WHERE NOT condition;
  ```

- SQL statement selects all fields from "Customers" where country is "Germany" AND city is "Berlin"
-

### **GROUP BY**
***
- ```sql
     SELECT column_name(s)
        FROM table_name
     WHERE condition
     GROUP BY column_name(s)
     ORDER BY column_name(s);
  ```
  
- The following SQL statement lists the number of customers in each country. Only include countries with more than 5 customers:
- ```sql
     SELECT COUNT(CustomerID), Country
        FROM Customers
     GROUP BY Country
     HAVING COUNT(CustomerID) > 5;
  ``` 
  
- 

### **Having**
- The HAVING clause was added to SQL because the WHERE keyword cannot be used with aggregate functions.

- ```sql
     SELECT column_name(s)
       FROM table_name
     WHERE condition
     GROUP BY column_name(s)
     HAVING condition
     ORDER BY column_name(s);     
  ```
  
- SQL statement lists the number of customers in each country. Only include countries with more than 5 customers:

- ```sql
     SELECT COUNT(CustomerID), Country
       FROM Customers
     GROUP BY Country
     HAVING COUNT(CustomerID) > 5;     
  ```
 
- SQL statement lists the number of customers in each country, sorted high to low (Only include countries with more than 5 customers)

- ```sql
     SELECT COUNT(CustomerID), Country
         FROM Customers
     GROUP BY Country
     HAVING COUNT(CustomerID) > 5
     ORDER BY COUNT(CustomerID) DESC;
  ```


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
