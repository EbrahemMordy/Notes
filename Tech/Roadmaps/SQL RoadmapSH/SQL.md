# What's a database?
A database is an organized collection of data.

# SQL SELECT
```SQL
SELECT year,
       month,
       west
  FROM tutorial.us_housing_units
```

Rename columns

```SQL
SELECT west AS "West Region"
  FROM tutorial.us_housing_units
```

# SQL LIMIT
```SQL
SELECT *
  FROM tutorial.us_housing_units
 LIMIT 100
```

# SQL WHERE
```SQL
SELECT *
  FROM tutorial.us_housing_units
 WHERE month = 1
```

# SQL Comparison Operators

| Equal to                 | `=`          |
| ------------------------ | ------------ |
| Not equal to             | `<>` or `!=` |
| Greater than             | `>`          |
| Less than                | `<`          |
| Greater than or equal to | `>=`         |
| Less than or equal to    | `<=`         |
# SQL Logical Operators
- [`LIKE`](https://mode.com/sql-tutorial/sql-like) allows you to match similar values, instead of exact values.
- [`IN`](https://mode.com/sql-tutorial/sql-in-operator) allows you to specify a list of values you'd like to include.
- [`BETWEEN`](https://mode.com/sql-tutorial/sql-between) allows you to select only rows within a certain range.
- [`IS NULL`](https://mode.com/sql-tutorial/sql-is-null) allows you to select rows that contain no data in a given column.
- [`AND`](https://mode.com/sql-tutorial/sql-and-operator) allows you to select only rows that satisfy two conditions.
- [`OR`](https://mode.com/sql-tutorial/sql-or-operator) allows you to select rows that satisfy either of two conditions.
- [`NOT`](https://mode.com/sql-tutorial/sql-not-operator) allows you to select rows that do not match a certain condition.

# SQL LIKE
```sql
SELECT *
  FROM tutorial.billboard_top_100_year_end
 WHERE "group_name" LIKE 'Snoop%'
```

`ILIKE`  ignore case when you're matching values

```sql
SELECT *
  FROM tutorial.billboard_top_100_year_end
 WHERE "group_name" ILIKE 'snoop%'
```

# SQL IN
```sql
SELECT *
  FROM tutorial.billboard_top_100_year_end
 WHERE year_rank IN (1, 2, 3)
```

# SQL BETWEEN
```sql
SELECT *
  FROM tutorial.billboard_top_100_year_end
 WHERE year_rank >= 5 AND year_rank <= 10
```

# SQL IS NULL
```sql
SELECT *
  FROM tutorial.billboard_top_100_year_end
 WHERE artist IS NULL
```

# SQL AND
```sql
SELECT *
  FROM tutorial.billboard_top_100_year_end
 WHERE year = 2012
   AND year_rank <= 10
   AND "group_name" ILIKE '%feat%'
```

# SQL OR
```sql
SELECT *
  FROM tutorial.billboard_top_100_year_end
 WHERE year = 2013
   AND ("group_name" ILIKE '%macklemore%' OR "group_name" ILIKE '%timberlake%')
```

# SQL NOT
```sql
SELECT *
  FROM tutorial.billboard_top_100_year_end
 WHERE year = 2013
   AND artist IS NOT NULL
```

# SQL ORDER BY
```sql
SELECT *
  FROM tutorial.billboard_top_100_year_end
 WHERE year = 2013
 ORDER BY year_rank DESC
```

---
# SQL Aggregate Functions
- [`COUNT`](https://mode.com/sql-tutorial/sql-count) counts how many rows are in a particular column.
- [`SUM`](https://mode.com/sql-tutorial/sql-sum) adds together all the values in a particular column.
- [`MIN`](https://mode.com/sql-tutorial/sql-min-max) and [`MAX`](https://mode.com/sql-tutorial/sql-min-max) return the lowest and highest values in a particular column, respectively.
- [`AVG`](https://mode.com/sql-tutorial/sql-avg) calculates the average of a group of selected values.

# SQL COUNT
```sql
SELECT COUNT(high)
  FROM tutorial.aapl_historical_stock_price
```

```sql
SELECT COUNT(date) AS count_of_date
  FROM tutorial.aapl_historical_stock_price
```

```sql
SELECT
    COUNT(CASE WHEN list_price >= 500 THEN product_id END) AS expensive_product_count,
   COUNT(CASE WHEN list_price < 500 THEN product_id END) AS cheap_product_count
FROM products
```


If you must use spaces, you will need to use double quotes.

```sql
SELECT COUNT(date) AS "Count Of Date"
  FROM tutorial.aapl_historical_stock_price
```

# SQL SUM
```sql
SELECT SUM(volume)
  FROM tutorial.aapl_historical_stock_price
```

# SQL MIN/MAX
```sql
SELECT MIN(volume) AS min_volume,
       MAX(volume) AS max_volume
  FROM tutorial.aapl_historical_stock_price
```

# SQL AVG
```sql
SELECT AVG(high)
  FROM tutorial.aapl_historical_stock_price
```

# SQL GROUP BY
You can group by multiple columns, but you have to separate column names with commas—just as with [`ORDER BY`](https://mode.com/sql-tutorial/sql-order-by)):

```sql
SELECT year,
       month,
       COUNT(*) AS count
  FROM tutorial.aapl_historical_stock_price
 GROUP BY year, month
```

Group by number of column
```sql
SELECT year,
       month,
       COUNT(*) AS count
  FROM tutorial.aapl_historical_stock_price
 GROUP BY 1, 2
```

# SQL HAVING
```sql
SELECT year,
       month,
       MAX(high) AS month_high
  FROM tutorial.aapl_historical_stock_price
 GROUP BY year, month
HAVING MAX(high) > 400
 ORDER BY year, month
```

As mentioned in prior lessons, the order in which you write the clauses is important. Here's the order for everything you've learned so far:

1. `SELECT`
2. `FROM`
3. `WHERE`
4. `GROUP BY`
5. `HAVING`
6. `ORDER BY`

# SQL CASE
```sql
SELECT player_name,
       year,
       CASE WHEN year = 'SR' THEN 'yes'
            ELSE NULL END AS is_a_senior
  FROM benn.college_football_players
```

But what if you don't want null values in the `is_a_senior` column? The following query replaces those nulls with "no":

```sql
SELECT player_name,
       year,
       CASE WHEN year = 'SR' THEN 'yes'
            ELSE 'no' END AS is_a_senior
  FROM benn.college_football_players
```
You can also define a number of outcomes in a `CASE` statement by including as many `WHEN`/`THEN` statements as you'd like:

```sql
SELECT player_name,
       weight,
       CASE WHEN weight > 250 THEN 'over 250'
            WHEN weight > 200 THEN '201-250'
            WHEN weight > 175 THEN '176-200'
            ELSE '175 or under' END AS weight_group
  FROM benn.college_football_players
```

`CASE`'s slightly more complicated and substantially more useful functionality comes from pairing it with [aggregate functions](https://mode.com/sql-tutorial/sql-aggregate-functions). For example, let's say you want to only count rows that fulfill a certain condition. Since [`COUNT`](https://mode.com/sql-tutorial/sql-count) ignores nulls, you could use a `CASE` statement to evaluate the condition and produce null or non-null values depending on the outcome:

```sql
SELECT CASE WHEN year = 'FR' THEN 'FR'
            ELSE 'Not FR' END AS year_group,
            COUNT(1) AS count
  FROM benn.college_football_players
 GROUP BY CASE WHEN year = 'FR' THEN 'FR'
               ELSE 'Not FR' END
```

Now, you might be thinking "why wouldn't I just use a `WHERE` clause to filter out the rows I don't want to count?" You could do that—it would look like this:

```sql
SELECT COUNT(1) AS fr_count
  FROM benn.college_football_players
 WHERE year = 'FR'
```

But what if you also wanted to count a couple other conditions? Using the `WHERE` clause only allows you to count one condition. Here's an example of counting multiple conditions in one query:

```sql
SELECT CASE WHEN year = 'FR' THEN 'FR'
            WHEN year = 'SO' THEN 'SO'
            WHEN year = 'JR' THEN 'JR'
            WHEN year = 'SR' THEN 'SR'
            ELSE 'No Year Data' END AS year_group,
            COUNT(1) AS count
  FROM benn.college_football_players
 GROUP BY 1
```

```sql
SELECT COUNT(CASE WHEN year = 'FR' THEN 1 ELSE NULL END) AS fr_count,
       COUNT(CASE WHEN year = 'SO' THEN 1 ELSE NULL END) AS so_count,
       COUNT(CASE WHEN year = 'JR' THEN 1 ELSE NULL END) AS jr_count,
       COUNT(CASE WHEN year = 'SR' THEN 1 ELSE NULL END) AS sr_count
  FROM benn.college_football_players
```

# SQL DISTINCT
```sql
SELECT DISTINCT year, month
  FROM tutorial.aapl_historical_stock_price
```

```sql
SELECT COUNT(DISTINCT month) AS unique_months
  FROM tutorial.aapl_historical_stock_price
```

# SQL Joins
Check this again [Cheat Sheet](https://www.datacamp.com/cheat-sheet/sql-joins-cheat-sheet) 
```sql
SELECT teams.conference AS conference,
       AVG(players.weight) AS average_weight
  FROM benn.college_football_players players
  JOIN benn.college_football_teams teams
    ON teams.school_name = players.school_name
 GROUP BY teams.conference
 ORDER BY AVG(players.weight) DESC
```

# SQL INNER JOIN
![](Pasted%20image%2020250427192527.png)

# SQL Outer Joins
Outer joins are joins that return matched values **and** unmatched values from either or both tables. There are a few types of outer joins:

- [`LEFT JOIN` returns only unmatched rows from the left table](https://mode.com/sql-tutorial/sql-left-join), as well as matched rows in both tables.
- [`RIGHT JOIN` returns only unmatched rows from the right table](https://mode.com/sql-tutorial/sql-right-join) , as well as matched rows in both tables.
- [`FULL OUTER JOIN` returns unmatched rows from both tables,](https://mode.com/sql-tutorial/sql-full-outer-join)as well as matched rows in both tables.
![](Pasted%20image%2020250427201741.png)
# SQL LEFT JOIN
```sql
SELECT companies.permalink AS companies_permalink,
       companies.name AS companies_name,
       acquisitions.company_permalink AS acquisitions_permalink,
       acquisitions.acquired_at AS acquired_date
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_acquisitions acquisitions
    ON companies.permalink = acquisitions.company_permalink
```

# SQL RIGHT JOIN
```sql
SELECT companies.permalink AS companies_permalink,
       companies.name AS companies_name,
       acquisitions.company_permalink AS acquisitions_permalink,
       acquisitions.acquired_at AS acquired_date
  FROM tutorial.crunchbase_acquisitions acquisitions
 RIGHT JOIN tutorial.crunchbase_companies companies
    ON companies.permalink = acquisitions.company_permalink
```

# SQL Joins Using WHERE or ON
```sql
SELECT companies.permalink AS companies_permalink,
       companies.name AS companies_name,
       acquisitions.company_permalink AS acquisitions_permalink,
       acquisitions.acquired_at AS acquired_date
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_acquisitions acquisitions
    ON companies.permalink = acquisitions.company_permalink
 WHERE acquisitions.company_permalink != '/company/1000memories'
    OR acquisitions.company_permalink IS NULL
 ORDER BY 1
```

# SQL FULL OUTER JOIN
```SELECT COUNT(CASE WHEN companies.permalink IS NOT NULL AND acquisitions.company_permalink IS NULL
                  THEN companies.permalink ELSE NULL END) AS companies_only,
       COUNT(CASE WHEN companies.permalink IS NOT NULL AND acquisitions.company_permalink IS NOT NULL
                  THEN companies.permalink ELSE NULL END) AS both_tables,
       COUNT(CASE WHEN companies.permalink IS NULL AND acquisitions.company_permalink IS NOT NULL
                  THEN acquisitions.company_permalink ELSE NULL END) AS acquisitions_only
  FROM tutorial.crunchbase_companies companies
  FULL JOIN tutorial.crunchbase_acquisitions acquisitions
    ON companies.permalink = acquisitions.company_permalink
```

# Self Join
```MYSQL
WITH RECURSIVE EmployeeHierarchy AS (
  SELECT employee_id, employee_name, manager_id, 0 AS level
  FROM companyemployees
  WHERE manager_id IS NULL  
  UNION ALL
  SELECT emp.employee_id, emp.employee_name, emp.manager_id, eh.level + 1
  FROM companyemployees emp
  JOIN EmployeeHierarchy eh ON emp.manager_id = eh.employee_id
)
SELECT employee_id, employee_name, level
FROM EmployeeHierarchy;
```

# Cross Join
```MYSQL
CREATE TABLE Meals(MealName VARCHAR(100))
CREATE TABLE Drinks(DrinkName VARCHAR(100))
INSERT INTO Drinks
VALUES('Orange Juice'), ('Tea'), ('Cofee')
INSERT INTO Meals
VALUES('Omlet'), ('Fried Egg'), ('Sausage')
SELECT *
FROM Meals;
SELECT *
FROM Drinks
```
![](Pasted%20image%2020250428175613.png)

# SQL UNION
```sql
SELECT *
  FROM tutorial.crunchbase_investments_part1

 UNION

 SELECT *
   FROM tutorial.crunchbase_investments_part2
```

SQL has strict rules for appending data:

1. Both tables must have the same number of columns
2. The columns must have the same data types in the same order as the first table

# SQL Joins with Comparison Operators
```sql
SELECT companies.permalink,
       companies.name,
       companies.status,
       COUNT(investments.investor_permalink) AS investors
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_investments_part1 investments
    ON companies.permalink = investments.company_permalink
   AND investments.funded_year > companies.founded_year + 5
 GROUP BY 1,2, 3
```

# SQL Joins on Multiple Keys
```sql
SELECT companies.permalink,
       companies.name,
       investments.company_name,
       investments.company_permalink
  FROM tutorial.crunchbase_companies companies
  LEFT JOIN tutorial.crunchbase_investments_part1 investments
    ON companies.permalink = investments.company_permalink
   AND companies.name = investments.company_name
```

# SQL Self Joins


# Data Definition Language
The DDL commands in SQL are:

- **`CREATE`**: To add a new object to the database.
- **`ALTER`:** To change the structure of the database.
- **`DROP`**: To remove an existing object from the database. Check out our guide on [how to delete a column in SQL](https://www.dbvis.com/thetable/deleting-a-column-in-sql/).
- **`TRUNCATE`:** To remove all records from a table, including the space allocated to store this data.

```MYSQL
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    hire_date DATE
);
ALTER TABLE employees
ADD department_id INT;
DROP TABLE employees;
TRUNCATE TABLE employees;
```

# Data Manipulation Language
DML statements include:

- **SELECT**: This statement is used to retrieve data from one or more tables in a database. As an example, the following SQL query retrieves all records from the "customers" table: ``SELECT * FROM customers;``  

- **INSERT**: This statement is used to insert new data into a table. As an illustration, the following SQL statement inserts a new row into the "customers" table:
  ``INSERT INTO customers (id, name, address) VALUES (1, 'John Smith,' '123 Main St');``  

- **UPDATE**: This statement is used to modify existing data in a table. For example, the following SQL statement updates the address of the customer with an ID of 1 in the "customers" table: 
  ``UPDATE customers SET address = '456 Park Ave' WHERE id = 1;``  

- **DELETE**: This statement is used to delete data from a table. For example, the following SQL statement deletes the customer with an ID of 1 from the "customers" table:
  ``DELETE FROM customers WHERE id = 1;``


# Data Constraints
- [NOT NULL](https://www.w3schools.com/sql/sql_notnull.asp) - Ensures that a column cannot have a NULL value
- [UNIQUE](https://www.w3schools.com/sql/sql_unique.asp) - Ensures that all values in a column are different
- [PRIMARY KEY](https://www.w3schools.com/sql/sql_primarykey.asp) - A combination of a `NOT NULL` and `UNIQUE`. Uniquely identifies each row in a table
- [FOREIGN KEY](https://www.w3schools.com/sql/sql_foreignkey.asp) - Prevents actions that would destroy links between tables
- [CHECK](https://www.w3schools.com/sql/sql_check.asp) - Ensures that the values in a column satisfies a specific condition

# Subqueries 
```SQL
SELECT * FROM CUSTOMERS 
WHERE ID IN (SELECT ID FROM CUSTOMERS WHERE SALARY > 4500);
```

# Correlated Subqueries
A _correlated subquery_ is a subquery that contains a reference to a table that also appears in the outer query. For example:

```mysql
SELECT * FROM t1
  WHERE column1 = ANY (SELECT column1 FROM t2
                       WHERE t2.column2 = t1.column2);
```

# String Functions
- CONCAT `CONCAT ( string_value1, string_value2 [, string_valueN ] )` 
- LENGTH `LENGTH(string)`
- SUBSTRING `SUBSTRING(string, start, length)` 
- REPLACE `REPLACE(string, old_string, new_string)` 
- UPPER `UPPER(text)` 
- LOWER `LOWER(text)` 

# Date and Time
- `DATE` - format YYYY-MM-DD
- `DATETIME` - format: YYYY-MM-DD HH:MI:SS
- `TIMESTAMP` - format: YYYY-MM-DD HH:MI:SS
- `YEAR` - format YYYY or YY

# Date and Time Functions
- TIMESTAMP `TIMESTAMP(expression, time)` 
- DATEPART `DATEPART(interval, date)` 
- DATEADD `DATEADD(datepart, numberToAdd, date)` 

# Numeric Functions
- FLOOR `FLOOR(number)` 
- ABS `ABS(number)` 
- MOD `MOD(x, y)` 
- ROUND `ROUND(number, decimals)`
- CEILING `CEILING(number)`

# Conditional 
- NULLIF `NULLIF(expr1, expr2)` 
- COALESCE `COALESCE(col,value)` replace null with value

# Views
- A view is a virtual table defined by a query.
- Say we wrote a query to join three tables, as in the previous example, and then select the relevant columns. The new table created by this query can be saved as a view, to be further queried later on.
- Views are useful for:
    - **simplifying**: putting together data from different tables to be queried more simply,
    - **aggregating**: running aggregate functions, like finding the sum, and storing the results,
    - **partitioning**: dividing data into logical pieces,
    - **securing**: hiding columns that should be kept secure. While there are other ways in which views can be useful, in this lecture we will focus on the above four.
```sqlite
CREATE VIEW "longlist" AS
SELECT "name", "title" FROM "authors"
JOIN "authored" ON "authors"."id" = "authored"."author_id"
JOIN "books" ON "books"."id" = "authored"."book_id";
```

```sqlite
CREATE TEMPORARY VIEW "average_ratings_by_year" AS
SELECT "year", ROUND(AVG("rating"), 2) AS "rating" FROM "average_book_ratings" 
GROUP BY "year";
```

# Common Table Expression (CTE)
A regular view exists forever in our database schema. A temporary view exists for the duration of our connection with the database. A CTE is a view that exists for a single query alone.
```sqlite
WITH "average_book_ratings" AS (
    SELECT "book_id", "title", "year", ROUND(AVG("rating"), 2) AS "rating" FROM "ratings"
    JOIN "books" ON "ratings"."book_id" = "books"."id"
    GROUP BY "book_id"
)
SELECT "year" ROUND(AVG("rating"), 2) AS "rating" FROM "average_book_ratings"
GROUP BY "year";
```

# Soft Deletions
mark row as deleted without delete it from database

# Index
```mysql
CREATE INDEX "title_index" ON "movies" ("title");
```

```mysql
DROP INDEX "title_index";
```

# COVERING INDEX
A covering index means that all the information needed for the query can be found within the index itself. Instead of two steps:

1. looking up relevant information in the index,
2. using the index to then search the table, a covering index means that we do our search in one step (just the first one).

# Partial Index
- This is an index that includes only a subset of rows from a table, allowing us to save some space that a full index would occupy.
- This is especially useful when we know that users query only a subset of rows from the table. In the case of IMDb, it may be that the users are more likely to query a movie that was just released as opposed to a movie that is 15 years old. Let's try to create a partial index that stores the titles of movies released in 2023.
    ```mysql
    CREATE INDEX "recents" ON "movies" ("titles")
    WHERE "year" = 2023;
    ```
- We can check that searching for movies released in 2023 uses the new index.
    ```mysql
    EXPLAIN QUERY PLAN
    SELECT "title" FROM "movies"
    WHERE "year" = 2023;
    ```

# Concurrency
Concurrency is the simultaneous handling of multiple queries or interactions by the database. Imagine a database for a website, or a financial service, that gets a lot of traffic at the same time. Concurrency is particularly important in these cases.

# Transactions
Transactions have some properties, which can be remembered using the acronym ACID:
-  **atomicity**: can't be broken down into smaller pieces,
- **consistency**: should not violate a database constraint,
- **isolation**: if multiple users access a database, their transactions cannot interfere with each other,
- **durability**: in case of any failure within the database, all data changed by transactions will remain.
```mysql
BEGIN TRANSACTION;
UPDATE "accounts" SET "balance" = "balance" + 10 WHERE "id" = 2;
UPDATE "accounts" SET "balance" = "balance" - 10 WHERE "id" = 1;
COMMIT;
```

```mysql
BEGIN TRANSACTION;
UPDATE "accounts" SET "balance" = "balance" + 10 WHERE "id" = 2;
UPDATE "accounts" SET "balance" = "balance" - 10 WHERE "id" = 1; -- Invokes constraint error
ROLLBACK;
```

# Race Conditions
- A race condition occurs when multiple entities simultaneously access and make decisions based on a shared value, potentially causing inconsistencies in the database. Unresolved race conditions can be exploited by hackers to manipulate the database.
- transactions are processed in **isolation** to avoid the inconsistencies in the first place. Each transaction dealing with similar data from our database will be processed sequentially. This helps prevent the inconsistencies that an adversarial attack can exploit.
- To make transactions sequential, SQLite and other database management systems use **locks** on databases. A table in a database could be in a few different states:
    - **UNLOCKED**: this is the default state when no user is accessing the database,
    - **SHARED**: when a transaction is reading data from the database, it obtains shared lock that allows other transactions to read simultaneously from the database,
    - **EXCLUSIVE**: if a transaction needs to write or update data, it obtains an exclusive lock on the database that does not allow other transactions to occur at the same time (not even a read)
