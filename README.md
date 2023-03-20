# SQL and PostgreSQL

## SQL

SQL is a standard language for accessing and manipulating databases.

- SQL stands for Structured Query Language
- SQL lets you access and manipulate databases
- SQL became a standard of the American National Standards Institute (ANSI) in 1986, and of the International Organization for Standardization (ISO) in 1987

**SQL Playground**: https://pg-sql.com/

## Basic Query

### Creating Table

```sql
CREATE TABLE cities (
    name VARCHAR(50),
    country VARCHAR(50),
    population INTEGER,
    area INTEGER
);
```

`CREATE TABLE` are keyword tell the databse that we want to do something. Always written out in capital letters.

And `cities` are identifier tell the database what thing we want to action on. ALways writter out in lower case letter.

`name`, `country`, `population` and `area` are column at the `cities` table.

`VARCHAR(50)` means a variable length character with a maximum of 50 chars.

### Inserting Table

```sql
INSERT INTO cities (name, country, populaiton, area)
VALUES ('Tokyo', 'Japan', 3834903434, 8223);
```

or use multiple insert rows

```sql
INSERT INTO cities (name, country, population, area)
VALUES ('Tokyo', 'Japan', 22323, 8226),
        ('Tokyo', 'Japan', 232323, 8224),
        ('Tokyo', 'Japan', 23233, 8225);
```

### Retrive Values of Table

Manual select column

```sql
SELECT name, country, population, area FROM cities;
```

Select column as needed

```sql
SELECT name, area FROM cities;
```

Or to retrieve all field use `*`

```sql
SELECT * FROM cities;
```

### Calculating Column

A generated column/calculating column is a special column that is always computed from other columns. Thus, it is for columns what a view is for tables. There are two kinds of generated columns: stored and virtual. A stored generated column is computed when it is written (inserted or updated) and occupies storage as if it were a normal column. A virtual generated column occupies no storage and is computed when it is read. Thus, a virtual generated column is similar to a view and a stored generated column is similar to a materialized view (except that it is always updated automatically). PostgreSQL currently implements only stored generated columns.

```sql
SELECT name, (population - area) AS calculated FROM cities;
```

In calculating column, SQL can run math operators

| Code  |  Name |
|---|---|
| `+`  |  Add |
| `-`  |  Subtract |
| `*`  |  Multiply |
| `/`  |  Divide |
| `^`  |  Exponent |
| `|/` |  Square Root |
| `@`  |  Absolute Value |
| `%`  |  Remainder |

### String Operator

| Code  |  Name |
|---|---|
| `||`  |  Join two strings |
| `CONCAT()`  |  Join two string |
| `LOWER()`  |  Give a lower case string |
| `LENGTH()`  |  Gives number of characters in a string |
| `UPPER()`  |  Gives an upper case string |

More info about string function and operator: https://www.postgresql.org/docs/9.1/functions-string.html

Example:

```sql
SELECT name || ', ' || country AS location FROM cities;
```

```sql
SELECT CONCAT(name, ', ', country) AS location FROM cities;
```

## Query

### Filter `Where`

```sql
SELECT select_list
FROM table_name
WHERE condition
ORDER BY sort_expression
```

The `WHERE` clause appears right after the FROM clause of the `SELECT` statement.  The `WHERE` clause uses the `condition` to filter the rows returned from the `SELECT` clause.

Example:

```sql
SELECT * FROM cities WHERE area > 8224;
```

Comparison Math Operator at `WHERE`

| Code  |  Name |
|---|---|
| `=`  |  Are the values equals? |
| `>`  |  Is the value on the left greater? |
| `<`  |  Is the value on the left less? |
| `>=`  |  Is the value on the left greater or equal to? |
| `IN`  |  Is the value present in a list? |
| `<=`  |  Is the value on the left lesser or equal to? |
| `<>`  |  Are the values not equal? |
| `!=`  |  Are the values not equal? |
| `BETWEEN`  |  Is the value between two other values? |
| `NOT IN`  |  Is the value not persent in a list? |

```sql
SELECT * FROM cities WHERE area BETWEEN 2000 AND 5000;
SELECT * FROM cities WHERE name IN ('Delhi', 'Shanghai');
SELECT * FROM cities WHERE name NOT IN ('Delhi', 'Shanghai');
SELECT * FROM cities WHERE area IN (2000, 5000) 
                                AND name = 'Delhi';
```

### Update

```sql
UPDATE table_name
SET column1 = value1,
    column2 = value2,
    ...
WHERE condition;
```

In this syntax:

- First, specify the name of the table that you want to update data after the UPDATE keyword.
- Second, specify columns and their new values after SET keyword. The columns that do not appear in the SET clause retain their original values.
- Third, determine which rows to update in the condition of the WHERE clause.

### Delete

```sql
DELETE FROM table_name
WHERE condition;
```
In this syntax:

- First, specify the name of the table from which you want to delete data after the DELETE FROM keywords.
- Second, use a condition in the WHERE clause to specify which rows from the table to delete

Example:

```sql
DELETE FROM cities
WHERE name = 'Tokyo';
```

## References

- https://www.udemy.com/course/sql-and-postgresql
- https://www.w3schools.com/sql/sql_intro.asp
- https://pg-sql.com/
- https://www.postgresql.org/docs/current/ddl-generated-columns.html
- https://www.postgresql.org/docs/9.1/functions-string.html
- https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-where/