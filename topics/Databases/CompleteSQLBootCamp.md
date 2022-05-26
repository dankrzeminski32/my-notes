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

#### ORDER BY

Sort rows based on a column value

can be sorted numerically or alphabetically

syntax

```
SELECT column_1, column_2
FROM table
ORDER BY column_1 ASC/DESC
```

`ORDER BY` comes after selection and happens at the bottom of the query. It is the last thing SQL does.

If you leave the `ASC/DESC` part blank, then it defaults to `ASC`

You can use `ORDER BY` on multiple columns.

It will order by your first entry first and then take all of those ordered rows and order them by your second column entry.

#### LIMIT

Allows us to limit the number of rows returned for a query

Similar to `head()` in R or Python

Allows you to get a good grasp and preview of your returned data.

Also becomes very useful when paired with ORDER BY

**Goes at the very end of a query, last command to be executed**

syntax,

```
SELECT * FROM payment
ORDER BY payment_date DESC
LIMIT 10;
```

A SQL query like that could help us answer a helpful business question like, what are the 10 most recent payments we have had?

#### BETWEEN

Used to match a value against a range of values

-   value `BETWEEN` low `AND` high

Using the `BETWEEN` operator is equal to using the >= **and** <= operators (it is inclusive).

You can also combine `BETWEEN` and the `NOT` operator to get `NOT BETWEEN`

This is the same as saying < low `OR` value > high
value `NOT BETWEEN` low `AND` high

We are **exclusive** of the actual low and high statements when using `NOT BETWEEN` unlike the regular expression

the `BETWEEN` operator can be used on dates. You need to format the dates in the **ISO 8601** standard format, which is `YYYY-MM-DD`

```
date BETWEEN '2007-01-01' AND '2007-02-01'
```

**NOTE:** datetime starts at 0:00, so pay close attention to inclusive and exclusive datetime queries

#### IN

Whenever you want to check if a value appears in some dataset

For example,

If you want to check if the name _adam_ appears `in` some first_name column or users table.

syntax,

```
value IN(option1,option2, .... option_n)
```

examples,

```
SELECT color FROM table
WHERE color IN('red','blue')
```

Can be used with the `NOT` operator

```
SELECT color FROM table
WHERE color NOT IN('red','blue')
```

#### LIKE and ILIKE

We have already found solutions for queries where we need direct matches like first_name='john'

but what about certain situations where we need to query for a general pattern? Such as, emails ending in '@gmail.com' pr all names that begin with 'A'?

The `LIKE` operator allows us to permorm pattern matching against string data with the use of **wildcard** characters

What are **wildcard** characters?

1.) the **%** percent symbol, this allows us to match **any sequence of characters**
2.) the **\_** underscore symbol, matches any **single** character

examples,

All names that begin with an 'A'

```
WHERE name LIKE 'A%'
```

Any string that starts with A and then has any sequence after that

All names that end with an 'a'

```
WHERE name LIKE '%a'
```

**NOTE:** `LIKE` is case-sensitive, we can use ILIKE which is case-insensitive.

using the underscore allows us to replace a single character

example,

image we want to get all mission impossible films

```
WHERE title LIKE 'Mission Impossible _'
```

this would give back mission impossible 1, mission impossible 2, etc...

You can use multiple underscoresm, which then leaves two character spots open,

We can combine pattern matching operators to create more complex patterns

```
WHERE name LIKE '_her%'
 - Cheryl
 - Theresa
 - Sherri

Has to be one character before 'her' but can have as many as you want after 'her'

**NOTE:** Keep in mind that PostgreSQL does support full regex capabilities.


good example,

```

SELECT \* FROM customer
WHERE first_name LIKE 'A%' AND last_name NOT LIKE 'B%'
ORDER BY last_name

```

All customers where first name starts with an 'A' and last name does not start with 'B'

```

How to check if a given word is in the column entries?

```
SELECT COUNT(*)
FROM film
WHERE title LIKE '%Truman%'
```

This returns all the films with the word Truman in them.

## GROUP BY Statements

#### Aggregate Functions

-   AVG() -> Returns average value
-   Count() -> Returns number of values
-   MAX() -> Returns max value
-   MIN() -> Returns min value
-   SUM() -> Returns the sum of all values

Aggregate functions happen only in the **SELECT** or **HAVING** clause.

```
SELECT MAX(replacement_cost) FROM film
```

Keep in mind that adding another column

```
SELECT MAX(replacement_cost), title FROM film
```

**Would not work** because our aggregate function is just returning a single value (in this case, max replacement cost)

#### Group By - Part 1

Allows us to aggregate columns per some category

Need to choose a **categorical** column to perform group by on

Categorical columns are non-continous

![gb1](img/gb1.png)

```
SELECT category_col, AGG(data_col)
FROM table
WHERE condition
GROUP BY category_col
```

The **GROUP BY** caluse has to come directly after a **FROM** statement or after a **WHERE** statement

In the **SELECT** statement, columns must either have an aggregate function or be in the **GROUP BY** call
