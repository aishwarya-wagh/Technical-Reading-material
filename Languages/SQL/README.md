# SQL - Key Concepts

## NULL Values
* Represents missing or unknown data.
* Handling NULL values is crucial in SQL operations.

## String Functions
* **CONCAT()**: Concatenates two or more strings.
* **SUBSTRING()**: Extracts a substring from a string.
* **UPPER(), LOWER()**: Convert string to uppercase or lowercase.
* **TRIM()**: Removes leading and trailing spaces from a string.

## Mathematical Functions
* **ROUND(), CEIL(), FLOOR()**: Round numbers to a specified number of decimal places or to the nearest integer.
* **ABS()**: Returns the absolute value of a number.
* **POWER(), SQRT()**: Calculate the power and square root of a number.

## Date and Time Functions
* **DATEADD(), DATEDIFF()**: Add or subtract time intervals from dates.
* **GETDATE(), CURRENT_TIMESTAMP()**: Retrieve the current date and time.
* **DATEPART(), DAY(), MONTH(), YEAR()**: Extract components from date values.

## Aggregate Functions (Advanced)
* **GROUPING SETS, ROLLUP, CUBE**: Advanced grouping options for aggregating data.

## Window Functions (Advanced)
* **ROW_NUMBER()**: Assign a unique sequential integer to each row within a partition of a result set.
* **RANK()**: Assign ranks to rows within a partition, with gaps in the ranking.
* **DENSE_RANK()**: Assign ranks to rows within a partition, without gaps in the ranking.
* **LAG()**: Access data from a previous row within the same result set.
* **LEAD()**: Access data from a subsequent row within the same result set.
* **NTH_VALUE()**: Return the value of a specific row within a window frame.
* **NTILE()**: Distribute rows into a specified number of groups.
* **MOVING AVERAGE**: Calculate the average of a set of values over a specific range.

## Common Table Expressions (CTEs)
* Temporary named result set that can be referenced within a SELECT, INSERT, UPDATE, or DELETE statement.
* Improves readability and maintainability of complex queries.

## Indexing
* Indexes improve the speed of data retrieval operations on database tables.
* Types of indexes include clustered and non-clustered indexes.

## Database Transactions (Advanced)
* ACID properties (Atomicity, Consistency, Isolation, Durability).
* Transaction isolation levels (READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE).

## Database Administration Commands (Advanced)
* **GRANT, REVOKE**: Grant or revoke privileges on database objects.
* **CREATE USER, ALTER USER, DROP USER**: Manage database users.

## Stored Procedures and Functions (Advanced)
* Input and output parameters.
* Exception handling.

## Normalization Forms (Advanced)
* 1NF, 2NF, 3NF, BCNF, 4NF: Different levels of normalization to eliminate redundancy and dependency.

## Triggers (Advanced)
* Database objects that automatically execute in response to certain events on a particular table or view.

## Composite Key
* A key that consists of more than one attribute to uniquely identify a record in a table.

## Surrogate Key
* A system-generated unique identifier used as the primary key instead of natural keys.

## Data Warehouse
* A centralized repository for storing large volumes of structured and unstructured data from various sources for analytical reporting and data analysis.

## Dimensional Modeling
* A design technique used in data warehousing to organize and represent data for easy querying and analysis.

## Fact Table
* A central table in a dimensional model that contains quantitative data (facts) about a business process.

## Dimension Table
* A table in a dimensional model that contains descriptive attributes about the entities in a fact table.

## Star Schema
* A dimensional modeling schema consisting of one or more fact tables connected to multiple dimension tables in a star-like structure.

## Snowflake Schema
* A dimensional modeling schema where dimension tables are normalized into multiple related tables, resembling a snowflake shape.

## OLTP (Online Transaction Processing)
* A database design optimized for transactional processing, characterized by many short transactions.

## OLAP (Online Analytical Processing)
* A database design optimized for analytical processing, supporting complex queries and aggregations for data analysis.

## Data Mart
* A subset of a data warehouse that focuses on a specific department, function, or business unit within an organization.

## Data Modeling Tools
* Software tools used to design, visualize, and document database schemas and relationships (e.g., ERwin, Oracle SQL Developer Data Modeler).

## Database Normalization Forms (Advanced)
* Beyond the basic normalization forms (1NF, 2NF, 3NF), additional forms like Boyce-Codd Normal Form (BCNF) and Fourth Normal Form (4NF) are also important to understand.

## Temporal Database Design (Advanced)
* Designing databases to manage historical data and changes over time.

## Graph Database Design (Advanced)
* Designing databases to represent and query highly connected data using graph structures.

## Data Federation
* Integrating data from multiple sources in real-time or near-real-time without physically consolidating it into a single repository.

## Common Syntax for Window Functions

### ROW_NUMBER()
```sql
SELECT
    column,
    ROW_NUMBER() OVER (PARTITION BY partition_column ORDER BY order_column) AS row_num
FROM
    table;
```

### RANK()
```sql
SELECT
    column,
    RANK() OVER (PARTITION BY partition_column ORDER BY order_column) AS rank
FROM
    table;
```

### DENSE_RANK()
```sql
SELECT
    column,
    DENSE_RANK() OVER (PARTITION BY partition_column ORDER BY order_column) AS dense_rank
FROM
    table;
```

### LAG()
```sql
SELECT
    column,
    LAG(column, offset, default_value) OVER (PARTITION BY partition_column ORDER BY order_column) AS previous_value
FROM
    table;
```

### LEAD()
```sql
SELECT
    column,
    LEAD(column, offset, default_value) OVER (PARTITION BY partition_column ORDER BY order_column) AS next_value
FROM
    table;
```

### NTH_VALUE()
```sql
SELECT
    column,
    NTH_VALUE(column, n) OVER (PARTITION BY partition_column ORDER BY order_column) AS nth_value
FROM
    table;
```

### NTILE()
```sql
SELECT
    column,
    NTILE(num_buckets) OVER (PARTITION BY partition_column ORDER BY order_column) AS tile
FROM
    table;
```

### MOVING AVERAGE (Using AVG with Window Functions)
```sql
SELECT
    column,
    AVG(column) OVER (PARTITION BY partition_column ORDER BY order_column ROWS BETWEEN n PRECEDING AND CURRENT ROW) AS moving_avg
FROM
    table;
```
