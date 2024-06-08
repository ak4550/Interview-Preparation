#### 1. What is SQL?
SQL (Structured Query Language) is a standard language used to communicate with relational databases. It is used for querying, updating, and managing relational databases.

#### 2. What are the different types of SQL commands?
SQL commands are broadly categorized into **four** types:   
**(a). Data Definition Language (DDL):** Used to define and modify the structure of database objects. Examples include CREATE, ALTER, DROP.  
**(b). Data Manipulation Language (DML):** Used to manipulate data stored in the database. Examples include SELECT, INSERT, UPDATE, DELETE.  
**(c). Data Control Language (DCL):** Used to control access to data within the database. Examples include GRANT, REVOKE.    
**(d). Transaction Control Language (TCL):** Used to manage transactions within the database. Examples include COMMIT, ROLLBACK.  

#### 3. What is a primary key?
A primary key is a unique identifier for each record in a table. It ensures that each row in a table is uniquely identifiable and cannot have NULL values.

#### 4. What is a foreign key?
A foreign key is a column or a set of columns in a table that references the primary key or a unique key in another table. It establishes a relationship between two tables.

#### 5. What is the difference between INNER JOIN and OUTER JOIN?
**INNER JOIN** returns rows when there is at least one match in both tables being joined.   
**OUTER JOIN** returns all rows from both tables, with NULL values where there is no match.   

#### 6. What is normalization and why is it important?
Normalization is the process of organizing data in a database to reduce redundancy and dependency. It ensures that data is stored logically and efficiently. Normalization helps in improving data integrity and reducing anomalies such as insertion, update, and deletion anomalies.

#### 7. What is the difference between DELETE and TRUNCATE commands?
**(a).** DELETE command is used to remove one or more rows from a table based on specified conditions, whereas TRUNCATE command is used to remove all the rows from a table.   
**(b).** DELETE command can be rolled back using the ROLLBACK statement, but TRUNCATE command cannot be rolled back.     

#### 8. What is a subquery?
A subquery is a query nested within another query. It can be used to retrieve data from one or more tables based on specific criteria.

#### 9. What is a view?
A view is a virtual table based on the result set of a SELECT query. It does not store data physically but retrieves data from the underlying tables whenever it is queried. Views are used to simplify complex queries and restrict access to specific columns or rows of a table.

#### 10. Find 2nd Highest Score Using SQL?
```
SELECT MAX(score) AS second_highest_score
FROM scores
WHERE score < (SELECT MAX(score) FROM scores);
```

#### 11. Find nth Highest Score using SQL?
```
SELECT score
FROM scores
ORDER BY score DESC
OFFSET N-1 LIMIT 1;
```
