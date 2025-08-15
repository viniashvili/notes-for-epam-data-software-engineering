# Introduction to SQL

## *Database Basics*

* A **database** is an organized collection of data that can be easily accessed, managed, and updated.
* Databases store information in structured formats and provide mechanisms to retrieve, insert, update, and delete data.

---

## **Relational Databases (RDBMS)**

* Store data in **tables** (rows = records, columns = attributes).
* Data is related using **primary keys** and **foreign keys**.
* Examples: MySQL, PostgreSQL, Oracle, Microsoft SQL Server.

### **Data Structure**

* Uses **tables** with predefined schema.

### **Schema**

* **Fixed schema** — must define table structure (columns, types) before inserting data.

### **Scalability**

* Primarily **vertical scaling** (add more CPU/RAM to one server).
* Horizontal scaling (sharding) is complex.

### **Query Language**

* **SQL** (Structured Query Language) is used for defining, manipulating, and querying data.

### **ACID Compliance**

* **Strong ACID compliance**:

  * **Atomicity** — transactions are all-or-nothing.
  * **Consistency** — database moves from one valid state to another.
  * **Isolation** — concurrent transactions don’t interfere.
  * **Durability** — committed data is saved permanently.

---

## **Non-Relational Databases (NoSQL)**

* Store data in **non-tabular formats** (key-value, document, column-family, graph).
* Designed for flexibility, scalability, and handling large volumes of unstructured/semi-structured data.
* Examples: MongoDB (document), Redis (key-value), Cassandra (column-family), Neo4j (graph).

### **Data Structure**

* **Flexible data models** — can be key-value pairs, JSON documents, wide-column stores, or graphs.

### **Schema**

* **Schema-less** or **dynamic schema** — structure can change without affecting existing data.

### **Scalability**

* Designed for **horizontal scaling** (adding more servers).
* Easily handles distributed storage and high availability.

### **Query Language**

* Varies by database type:

  * MongoDB → MQL (Mongo Query Language).
  * Cassandra → CQL (Cassandra Query Language).
  * Redis → command-based queries.

### **ACID Compliance**

* Many NoSQL databases favor **BASE** (Basically Available, Soft state, Eventual consistency) over strict ACID for performance.
* Some NoSQL systems support partial ACID compliance.

---

## *DB Components*

* **NOT NULL** – Ensures a column cannot store NULL values.
* **DEFAULT** – Assigns a default value to a column if no value is specified.
* **UNIQUE** – Ensures all values in a column are distinct.
* **KEY** – Generic term referring to columns or sets of columns used to identify records.
* **CHECK** – Ensures that all values in a column satisfy a specific condition (e.g., `CHECK (age >= 18)`).

---

## **Types of Keys**

* **Super Key** – Any set of one or more columns that can uniquely identify a record in a table (includes extra attributes beyond the minimum needed).
* **Candidate Key** – Minimal set of attributes that can uniquely identify a record (no redundant attributes).
* **Primary Key** – Chosen candidate key used to uniquely identify records in a table; cannot contain NULL values.
* **Foreign Key** – A column or set of columns in one table that refers to the primary key in another table; enforces referential integrity.
* **Alternate Key** – Candidate keys that are **not** chosen as the primary key.
* **Composite Key** – A key composed of two or more columns that together uniquely identify a record.
* **Natural Key** – A key based on real-world, meaningful data (e.g., email address, national ID).
* **Surrogate Key** – A system-generated key (e.g., auto-increment ID) with no business meaning, used purely for identification.

---

## *DB Modeling*

* **Conceptual Schema**

  * High-level description of the data and its relationships.
  * Technology-agnostic and focused on the business domain.
  * Typically represented by an **Entity-Relationship Diagram (ERD)**.
  * Example: "We have customers, each customer can place multiple orders, each order contains products."

* **Logical Schema**

  * Detailed structure of the data model, independent of physical storage.
  * Specifies tables, columns, relationships, constraints, primary/foreign keys.
  * Uses a specific database model (e.g., relational model) but not tied to a specific DBMS.
  * Example: Table `Customer(id, name, email)`, Table `Order(id, customer_id, date)`, with foreign key relationships.

* **Physical Schema**

  * Actual implementation details in a specific DBMS.
  * Includes indexes, partitioning, file storage format, data types, and performance optimizations.
  * Tied to a specific database engine (e.g., MySQL, PostgreSQL, Oracle).
  * Example: `Customer.id` as `BIGINT AUTO_INCREMENT`, indexes on `email` and `customer_id`.

---

## *Normalization*

* **Definition**

  * Process of organizing data in a database to reduce redundancy and improve data integrity.
  * Achieved by dividing tables into smaller, related tables and defining relationships between them.
  * Ensures minimal duplication and avoids anomalies in insert, update, and delete operations.

---

### **1NF (First Normal Form)**

* Data is stored in **atomic** (indivisible) values — no repeating groups or arrays.
* Each record is unique (no duplicate rows).
* Each column contains only one value per row.
* **Example**:

  * ❌ `Phones = [12345, 67890]`
  * ✅ `Phone` column has one number per row.

---

### **2NF (Second Normal Form)**

* Must first be in **1NF**.
* All **non-key attributes** must depend on the **whole primary key**, not just part of it (removes **partial dependency**).
* Applies mainly to tables with **composite primary keys**.
* **Example**:

  * If a table’s primary key is `(OrderID, ProductID)`, attributes like `CustomerName` that depend only on `OrderID` should be moved to another table.

---

### **3NF (Third Normal Form)**

* Must first be in **2NF**.
* No **transitive dependencies** — non-key attributes should not depend on other non-key attributes.
* Every non-key attribute must depend **only on the primary key**.
* **Example**:

  * If `CustomerCity` depends on `CustomerZipCode` (and not directly on the primary key), it should be moved to a separate table.

---

## *DML (Data Manipulation Language)*

* Part of SQL used to **manipulate data inside database tables**.
* Common commands:

  * **INSERT** – Add new rows.
  * **UPDATE** – Modify existing rows.
  * **DELETE** – Remove rows.
  * **MERGE** – Insert, update, or delete based on a condition.
* Operates on the data stored in the database, not the structure (DDL does that).

---

## **CTE (Common Table Expression)**

* A **temporary named result set** defined within the execution scope of a single SQL statement.
* Created using the `WITH` keyword, followed by a query.
* Improves query readability and can be referenced multiple times within the same statement.
* Can be **recursive** or **non-recursive**.
* **Example**:

  ```sql
  WITH Sales_CTE AS (
      SELECT CustomerID, SUM(Amount) AS TotalSales
      FROM Sales
      GROUP BY CustomerID
  )
  SELECT * FROM Sales_CTE WHERE TotalSales > 1000;
  ```

---

## **View**

* A **virtual table** created from the result of a query.
* Does not store data physically (unless it’s a materialized view).
* Useful for simplifying complex queries, improving security (restricting columns), and ensuring consistent query logic.
* **Example**:

  ```sql
  CREATE VIEW HighValueCustomers AS
  SELECT CustomerID, Name, TotalSpent
  FROM Customers
  WHERE TotalSpent > 5000;
  ```

---

## **Subquery**

* A query nested inside another SQL query.
* Can appear in **SELECT**, **FROM**, or **WHERE** clauses.
* Types:

  * **Single-row subquery** – returns one row.
  * **Multi-row subquery** – returns multiple rows.
  * **Correlated subquery** – references columns from the outer query.
* **Example**:

  ```sql
  SELECT Name
  FROM Customers
  WHERE TotalSpent > (SELECT AVG(TotalSpent) FROM Customers);
  ```

---

## *TCL (Transaction Control Language)*

* Part of SQL used to **manage transactions** in a database.
* Works with **DML statements** to ensure data integrity.
* Common TCL commands:

  * **COMMIT** – Saves all changes made in the current transaction permanently.
  * **ROLLBACK** – Undoes all changes made in the current transaction.
  * **SAVEPOINT** – Creates a marker within a transaction to roll back to a specific point without undoing the entire transaction.

---

## **ACID Properties** (Key for transaction reliability)

* **Atomicity** – All operations in a transaction either complete fully or have no effect.
* **Consistency** – A transaction brings the database from one valid state to another, preserving rules and constraints.
* **Isolation** – Transactions are executed independently without interfering with each other.
* **Durability** – Once committed, the changes remain permanent even in case of system failure.

---

## **COMMIT**

* Makes all changes in the transaction permanent.
* Once committed, changes **cannot be undone** (except via compensating transactions).
* **Example**:

  ```sql
  UPDATE Accounts SET Balance = Balance - 500 WHERE AccountID = 1;
  COMMIT;
  ```

---

## **ROLLBACK**

* Reverts all changes made in the current transaction to the last **COMMIT** or **SAVEPOINT**.
* Used when an error occurs or when changes need to be discarded.
* **Example**:

  ```sql
  UPDATE Accounts SET Balance = Balance - 500 WHERE AccountID = 1;
  ROLLBACK;
  ```

---

## **SAVEPOINT**

* Marks a specific point within a transaction.
* You can roll back only to that point, keeping changes before it intact.
* **Example**:

  ```sql
  SAVEPOINT BeforeUpdate;
  UPDATE Accounts SET Balance = Balance - 500 WHERE AccountID = 1;
  ROLLBACK TO BeforeUpdate;
  ```

---

## *DDL (Data Definition Language)*

* Part of SQL used to **define and manage database structures** like tables, indexes, and schemas.

* Does **not deal with data directly**, but with the **structure that holds the data**.

* Common DDL commands:

  * **CREATE** – Creates new database objects (tables, views, indexes, schemas).
  * **ALTER** – Modifies existing database objects (add/drop columns, change datatype).
  * **DROP** – Deletes database objects permanently.
  * **TRUNCATE** – Removes all data from a table **without logging individual row deletions** (faster than DELETE).

* **Example**:

  ```sql
  CREATE TABLE Employees (
      EmployeeID INT PRIMARY KEY,
      Name VARCHAR(50),
      Department VARCHAR(50)
  );

  ALTER TABLE Employees ADD COLUMN Salary DECIMAL(10,2);

  DROP TABLE Employees;
  ```

---

## *Snapshot vs View*

*Both are ways to access data, but with different behavior and purpose.*

### **View**

* A **virtual table** created by a **query**.
* Does **not store data physically**; it dynamically fetches data from underlying tables.
* Useful for **simplifying complex queries, abstraction, and security**.
* Changes in the underlying table **reflect immediately** in the view.
* **Example**:

  ```sql
  CREATE VIEW EmployeeDept AS
  SELECT Name, Department
  FROM Employees;
  ```

### **Snapshot (Materialized View)**

* A **physical copy of the data** at a certain point in time.
* Stores **actual data**, not just a query.
* Useful for **reporting, analytics, or performance optimization**.
* Can be **refreshed periodically** to stay up-to-date with the source.
* **Example**:

  ```sql
  CREATE MATERIALIZED VIEW EmployeeSnapshot AS
  SELECT Name, Department
  FROM Employees
  WITH DATA;
  ```

*Key Difference:*

| Feature           | View                          | Snapshot              |
| ----------------- | ----------------------------- | --------------------- |
| Data storage      | Virtual, no storage           | Physical, stores data |
| Real-time updates | Yes                           | Only when refreshed   |
| Use case          | Simplifying queries, security | Reporting, analytics  |

---

## *DCL (Data Control Language)*

* Part of SQL used to **control access and permissions** on database objects.

* Works with **users, roles, and privileges** to ensure security.

* Common DCL commands:

  * **GRANT** – Gives specific privileges to a user or role.
  * **REVOKE** – Removes specific privileges from a user or role.

* **Example**:

  ```sql
  -- Grant SELECT and INSERT privileges on Employees table to user John
  GRANT SELECT, INSERT ON Employees TO John;

  -- Revoke INSERT privilege
  REVOKE INSERT ON Employees FROM John;
  ```

---

## *Key Aspects of PostgreSQL Security*

* **Authentication** – Verifies the identity of users (passwords, certificates, LDAP, etc.).
* **Authorization** – Controls what users/roles can do (via privileges and grants).
* **Roles and Privileges** – Fine-grained access control for tables, schemas, functions, and more.
* **SSL/TLS** – Encrypts client-server communication.
* **Row-Level Security (RLS)** – Allows policies to filter rows a user can access.
* **Auditing & Logging** – Tracks user activity for compliance and troubleshooting.

---

## *Roles in PostgreSQL*

* PostgreSQL uses **roles** instead of separate users and groups.

* A **role can act as a user, a group, or both**.

* Roles can **own objects** and have **privileges granted to them**.

* **Role Types**:

  * **Login Role** – Can log in and act as a database user.
  * **Group Role** – Acts as a container for privileges, can have multiple members.
  * **Superuser Role** – Has unrestricted access to all objects and operations.

* **Creating Roles Example**:

  ```sql
  -- Create a role with login
  CREATE ROLE John LOGIN PASSWORD 'secret123';

  -- Create a group role
  CREATE ROLE Managers;

  -- Grant John to Managers group
  GRANT Managers TO John;

  -- Grant privileges to Managers
  GRANT SELECT, INSERT ON Employees TO Managers;
  ```

---

## *OLTP vs OLAP*

* **OLTP (Online Transaction Processing)** and **OLAP (Online Analytical Processing)** are two types of database systems used for **different purposes**.

---

### **OLTP (Online Transaction Processing)**

* Focused on **managing day-to-day transactional data**.
* Optimized for **fast inserts, updates, and deletes**.
* Handles **large numbers of short, atomic transactions**.
* Data is **highly normalized** to reduce redundancy.
* **Use case:** Banking systems, e-commerce orders, ticket bookings.
* **Characteristics:**

  * Many users performing concurrent operations.
  * Real-time data processing.
  * Short response time required.
* **Example:**

  ```sql
  INSERT INTO Orders (OrderID, CustomerID, OrderDate) VALUES (101, 1, CURRENT_DATE);
  ```

---

### **OLAP (Online Analytical Processing)**

* Focused on **analyzing large volumes of historical data**.
* Optimized for **complex queries, aggregations, and reporting**.
* Data is often **denormalized** into star or snowflake schemas.
* **Use case:** Business intelligence, data warehouses, trend analysis.
* **Characteristics:**

  * Few users, performing complex queries.
  * Large amounts of historical data.
  * Response time can be longer due to complex computations.
* **Example:**

  ```sql
  SELECT Region, SUM(Sales) 
  FROM Sales_Fact
  GROUP BY Region;
  ```

---

### **Key Differences**

| Feature        | OLTP                   | OLAP                      |
| -------------- | ---------------------- | ------------------------- |
| Purpose        | Transaction processing | Data analysis & reporting |
| Data Volume    | Small per transaction  | Large, historical         |
| Data Structure | Normalized             | Denormalized              |
| Queries        | Simple, short          | Complex, aggregations     |
| Users          | Many                   | Few                       |
| Updates        | Frequent               | Rare                      |
| Response Time  | Fast                   | Can be slower             |

---

## *Window Functions*

* SQL functions that perform calculations **across a set of table rows related to the current row**.
* Unlike aggregate functions, **window functions do not collapse rows**; they return a value for **each row**.
* Useful for **ranking, running totals, moving averages, and analytics**.

---

## **OVER Clause**

* Defines the **window (set of rows)** for the function.

* Can include:

  * **PARTITION BY** – Groups rows for independent calculations.
  * **ORDER BY** – Defines the order of rows within the partition.
  * **ROWS / RANGE** – Specifies a frame of rows relative to the current row.

* **Basic Syntax:**

  ```sql
  <window_function>() OVER (
      [PARTITION BY column1, column2, ...]
      [ORDER BY column3, ...]
      [ROWS BETWEEN ...]
  )
  ```

---

## **Ranking Functions**

* Used to **assign a rank or number to each row** in a partition based on order.

### **ROW\_NUMBER()**

* Assigns a **unique sequential number** to rows within a partition.
* **Ties get separate numbers** (no duplicates).
* **Example:**

  ```sql
  SELECT Name, Department,
         ROW_NUMBER() OVER (PARTITION BY Department ORDER BY Salary DESC) AS RowNum
  FROM Employees;
  ```

---

### **RANK()**

* Assigns a **rank based on order**, but **ties get the same rank**.
* **Gaps occur** in ranking after ties.
* **Example:**

  ```sql
  SELECT Name, Department,
         RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS RankNum
  FROM Employees;
  ```

---

### **DENSE\_RANK()**

* Similar to RANK(), but **no gaps in ranking** after ties.
* **Example:**

  ```sql
  SELECT Name, Department,
         DENSE_RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS DenseRankNum
  FROM Employees;
  ```

---

## **Offset Functions (LEAD, LAG)**

* Access **previous or next row values** without a self-join.

* Useful for **comparing rows, calculating differences, or trends**.

* **LAG()** – Gets a value from a **previous row**.

* **LEAD()** – Gets a value from a **next row**.

* **Example:**

  ```sql
  SELECT Name, Salary,
         LAG(Salary, 1) OVER (ORDER BY Salary) AS PrevSalary,
         LEAD(Salary, 1) OVER (ORDER BY Salary) AS NextSalary
  FROM Employees;
  ```

---

## **Use Cases of Window Functions**

* Ranking employees or products by sales or performance.
* Calculating **running totals, moving averages**, or cumulative sums.
* Comparing **current row with previous/next row** for trends.
* Generating **row numbers or percentiles** for reporting and analytics.
* Avoiding **complex self-joins** for relative calculations.

---

Here’s your notes updated with **window frames, rows vs range frames, and enhanced use cases** in the same structured style:

---

## *Window Functions*

* SQL functions that perform calculations **across a set of table rows related to the current row**.
* Return a value for **each row**, unlike aggregate functions.
* Useful for **ranking, running totals, moving averages, trend analysis, and analytics**.

---

## **OVER Clause**

* Defines the **window (set of rows)** for the function.

* Components:

  * **PARTITION BY** – Groups rows independently.
  * **ORDER BY** – Defines row order within the partition.
  * **ROWS / RANGE** – Defines the **frame** relative to the current row.

* **Basic Syntax:**

  ```sql
  <window_function>() OVER (
      [PARTITION BY column1, column2, ...]
      [ORDER BY column3, ...]
      [ROWS BETWEEN ... | RANGE BETWEEN ...]
  )
  ```

---

## *Window Frames*

* **Window frame** specifies **which rows the window function should operate on**, relative to the current row.

### **1. ROWS Frame**

* Defines the frame in **physical number of rows**.
* Example:

  ```sql
  SUM(Salary) OVER (
      ORDER BY HireDate
      ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
  ) AS SalarySum
  ```

*Meaning:* Sum of current row + 2 previous rows.

---

### **2. RANGE Frame**

* Defines the frame in terms of **logical value range**, not row count.
* Example:

  ```sql
  SUM(Salary) OVER (
      ORDER BY HireDate
      RANGE BETWEEN INTERVAL '1 year' PRECEDING AND CURRENT ROW
  ) AS SalarySum
  ```

*Meaning:* Sum of salaries for employees hired in the last year relative to current row.

---

### **3. GROUPS Frame** *(PostgreSQL-specific)*

* Frames based on **groups of tied values** in ORDER BY.
* Useful for **percentiles or cumulative aggregates where multiple rows share same order value**.
* Example:

  ```sql
  SUM(Salary) OVER (
      ORDER BY Salary
      GROUPS BETWEEN 1 PRECEDING AND CURRENT ROW
  ) AS SalarySum
  ```

---

## **Use Cases of Window Functions**

* **Ranking & ordering:** ROW\_NUMBER(), RANK(), DENSE\_RANK() for top-N queries or leaderboards.
* **Running totals / cumulative sums:** SUM() OVER(...) for financial reporting.
* **Moving averages & trends:** AVG() OVER(...) with ROWS or RANGE frames.
* **Comparisons between rows:** LAG() / LEAD() for month-over-month or day-over-day analysis.
* **Percentiles / analytics:** NTILE(), CUME\_DIST() for segmentation or scoring.
* **Avoiding complex joins:** Relative calculations without self-joins.
