# Jose Portilla Udemy Course - The Complete SQL Bootcamp 2022: Go from Zero to Hero

## My collection of personal notes from the course

## Course Introduction

#### Overview

-   Course will use PostgresSQL

-   Databases and Tables Basics
-   SQL Statement Fundamentals
-   GROUP BY Clause
-   Assesment Test over these topics

-   JOIN
-   Advanced SQL
-   Commands
-   2nd Assessment test

-   Create Databases and Tables
-   Assessment Test 3

Extra lectures

-   Views
-   PostgreSQL with Python

#### Databases Overview

From Spreadsheets to Databases

**Spreadsheets**

-   One time analysis
-   quick charts
-   small datasets
-   untrained individuals

**Databases**

-   Data Integrity (cant just click a cell and change it)
-   massive data amounts
-   quick combine different datasets
-   automation
-   backend for web apps and apps

**Comparison**

-   Tabs in excel are like tables in a database
-   rows and columns are the same

**Database Platforms**

-   PostgreSQL = free & Open Source
-   MySQL & MariaSQL = Free & Open Source, widely used on internet
-   MS SQL Server Express = Free but has limitations, compatible with SQL Server (windows) only
-   Microsoft access = Cost is bad -, not easy to use just SQL
-   SQlite = Free (open source), mostly command line.

PostgreSQL is great for learning SQL

SQL (Structured Query Language) is the programming langauge used to communicate with databases

SQL is used in so much!

-   MySQL
-   PostGreSQL
-   Oracle Databases
-   MS Access
-   Amazon Redshift
-   Looker
-   MemSQL
-   Periscope Data
-   Hive (runs on top of hadoop)
-   BigQuery
-   Facebook's Presto

All of these applications use SQL in the background

Most of the commands we learn are **not** specific to PostGreSQL

**PostgreSQL** = SQl Engine

**PgAgmin** - GUI Interface for PostgreSQL

## SQL Statement Fundamentals

#### SELEcT Statement

Most common used statement

Allows us to retreive data from tables

syntax

```
SELECT column_name FROM table_name;
```

You are **not** required to capitalize SQL commands but it is **best practice** as it seperates SQL Commands from tables, column names etc..

To grab all columns from the database, use:

```
SELECT * FROM table_name;
```

**Word of caution:** Using `SELECT *` should only be used when you need to utilize every column in the database. Calling this command greatly increases traffic between the database server and the application, which can affect the speed of other queries. [AND HAS A LIST OF OTHER NEGATIVE EFFECTS](https://stackoverflow.com/questions/3639861/why-is-select-considered-harmful)

To get multiple columns,

```
SELECT column_1,column_2 FROM table_name;
```

**Quick Note:** the semicolon ; at the end of the query just signifies the end of the statement. This is **optional**, but similar to capitilazation, this makes your statements easier to read and is **best practice**

#### SELECT DISTINCT

Columns sometimes have duplicate values

Whenever you only want the distinct/unique values,

We use the `DISTINCT` keyword.

syntax,

```
SELECT DISTINCT column FROM table;
```

to clarify which column the distinct operator is being applied to,

```
SELECT DISTINCT(column) FROM table;
```

Parantheses are not necessary here but that does **not** apply to every SQL command

**Note:** when using `DISTINCT` with multiple columns and no parentheses, it gives you back distinct entries, so you may see the same value in one column more than once, but never the same entry in all columns for more than one row. It is a distinct collection of columns

```
SELECT DISTINCT column_1,column_2 FROM table_name;
```

[Here is an example](https://www.w3resource.com/sql/select-statement/queries-with-distinct-multiple-columns.php)

#### COUNT Function

Returns the number of input rows that match a specific condition of a query.

COUNT(column_name) is a function so it **should have** the parentheses.

**IMPORTANT NOTE: ** `SELECT COUNT(column_name)` and `SELECT COUNT(*)` will return the same thing, since you are just returning the number of rows in the dataset which all have that column, so use

```
SELECT COUNT(*) FROM table_name
```

**Note:** The one instance where `SELECT COUNT(column_name)` is useful is for proper documentation. Say for instance you needed to count the number of some certain rows in table to answer a specific question about **one** column. When you look back on your `COUNT` function, the column name instead of \* will help you remember the report you were trying to generate or question you were trying to answer.

`COUNT()` by itself clearly just returns the number of rows in a table, which is somewhat useful

However, when `COUNT()` is combined with other SQL commands like `DISTINCT`, it becomes much more useful.

imagine we want to know how many unique names are in a table?

```
SELECT COUNT(DISTINCT name) FROM table;
```

**Side Note:**

If we wanted to make the above query more readable, we could do:

```
SELECT COUNT(DISTINCT(name)) FROM table;
```

That is preferred IMO

#### SELECT WHERE Statement

SELECT and WHERE are the most fundamental SQL statements.

The **WHERE** statement allows us to specify certain conditions on columns for the rows that will be returned from our **SELECT** statement.

syntax

```
SELECT column_1, column_2
FROM table
WHERE conditions
```

Well what are these _conditions_?

**Comparison Operators**

Compare a Column value to something.

-   Is the price greater than $3.00?
-   Is the pet's name equal to "Sam"?

![SQL Comparison Operators](img/sql-comparison-operators.webp)

**Logical Operators**

Allow us to combine multiple comparison operators

-   AND
-   OR
-   NOT

Example,

```
SELECT name,choice
FROM table
WHERE name = 'David'
```

Now imagine multiple conditions

```
SELECT name,choice
FROM table
WHERE name='David' AND choice='Red'
```

_Note that name and choice are representing two columns in a database_
