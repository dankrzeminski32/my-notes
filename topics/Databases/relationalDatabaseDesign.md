# Relational Database Design - IT Pro TV

## Topics Covered

-   Relational database basics
-   Database Design
-   Database Models
-   Data Integrity
-   Query basics

## Relational Database Basics

### History, Terms, and Definitions

Before databases we tpically just used excel style "flat" files to store data.

#### What is the problem with these?

Having that many columns in one flat file can easily cause data corruption. Updating one column has the immediate effect on 30 other columns of data in the same sheet. Difficult to visualize and keep organized as well.

#### What makes a good database design?

A good database design means that when end users run queries against the database it returns correct and accurate results on a very consistent basis. This accuracy has a direct role in the reports and metrics that the company uses that are pulled from the database. So we are looking for ease of use as well as very accurate results.

#### Terminology

**Entity (Object)** - Something of interest that you want to track, usually a noun or collective noun. ex: Customer, salesperson, Employees.

**Attribute** - Property that describes an entity's characteristic ex: Name, phone number, hire date

**Relation** - Two-dimensional table that contains tuples and columns, just a **table** that contains relationships

> Man who created relational databases was a mathemetician so when you see the formulas behind database design the **R** in the formulas is for relation (table)

**Tuple (Row)** - Instnace of an object within a relation, row withing a table, just another word for row

**Column** - Attribute of an object within a relation, column within a table.

**Identifier** - Attribute that can be used to identify entity occurences (rows), can be unique, non-unique, or composite. Very important part of database design.

> What is a **Composite Identifier**? A: A combination of two or more columns in a database that can be used to uniquely identify each row in the table.

**Index** - Unique or non-unique identifier used to increase search speed. Rather than parsing every row in the database (slow) we have an index which allows the search to quickly jump to that section of data. We put these on our very searchable columns.

**Primary Key** - Unique Identifier used to identify rows in a table. Each row has a unique identifier It cannot be a duplicate. Never accepts nulls

**Foreign Key** - Primary Key from one table that appears as a column in another table, creating a relationship between two relations (tables)... If you have an employees salary information in one relation and his vacation time in another relation, how do you tie these two together so you can extract that employees information? A: using a Foreign Key.

**Relationship** - Exists between tables. Can be one-to-one, one-to-many, or many-to-many. Relationship from one table to another, how many occurences in **table 1** - to - **table 2**,

> You should attempt to avoid many-to-many relationships, we see these as bad and try to stay clear or fix them.

You can have many foreign keys in a table. These foreign keys lead back to the parent table which contain more information about that foreign key.

#### Composite Key Example

Employee privellages is a table which has two foreign keys, **Employee ID** (Primary Key in another table) and **Privellage ID**(Primary Key in another table) these two together make up a **composite key**

#### Why have more tables and relationships vs columns/attributes

If we have an employees table and we want to have data that represents the employees personal web page, we can have a column for webpages in that table or have another table relating back to the employee.

In this instance we want to create another table because not all employees are going to have a website, therefore if we just added a column in our employees table, we would have a lot of null values. Generally we want to stay clear of too many null values as we don't know if it is really important data missing or just not applicable data.

It is also important to note that by using a table instead we allow for organization as well as more metadata relating to more important attributes.

> Ask yourself, are a majority of entities going to have this piece of data? If no, then split it up and make another table for that piece of data, and just reference that primary key in the new table.

### Data Normalization

#### What is data normalization

-   Process of organizing a database into tables and columns
-   Normal forms, or rules, are applied to the data
-   Reduces or eliminates duplicate data, which reduces a number of issues from database modifications, or database anomalies.
-   Makes a database relational, allows for easy queries that give back **GOOD** data.
    > There are very technical mathematiical formulas that back the science behind first, second, and third normal forms.

#### What are database anomalies

Instances of weird quirks in the database that don't exactly make sense or are hard to draw conclusions from. These are most common when are databases are not in third normal form.

-   Update Anomalies

    -   When the same data exists on multiple rows
    -   Updates to some records but not others
    -   The relation is left in an inconsistent state

-   Deletion anomaly

    -   Delete certain data necessitates the deletion of other data
    -   might require null values

-   Insertion anomaly
    -   When certain facts canot be recorded
    -   Might require null values

We avoid these by using **Data normalization**!

#### Normal Forms

-   First Normal Form (1NF)

    -   The data is stored in a relational table
    -   Each column contains atomic values, breaking our data into smaller chunks, ex: First name and last name in seperate columns, not just one name column. That way we can filter by anythingre
    -   Break our data into it's smallest **Meaningful** form
    -   There are not repeating groups of columns (ex: You can't have the columns, phone_1 and phone_2 just because there are a few individuals with 2 phone numbers. We will learn how to workaround this later...)

-   Second Normal Form (2NF)

    -   Table is already in 1NF
    -   Non-key columns are dependent on the primary key (ex: if you change the pk user_id then the column phone_number should change as well )

-   Third Normal Form (3NF)
    -   Table is already in 2NF
    -   All of it's non-key columns are not transitibely dependant on the primary key.
    -   Translation: Non-key columns aren't dependent on the primary key through another key. transitively dependent means if a=b and b=c then a must equal c. WE DO NOT WANT THAT.

**MOST DATABASES ARE IN 3NF**

#### Additional Normal forms

    - Boyce-Codd normal form (BCNF)
    - Fourth Normal form (4NF)
    - Fifth Normal Form (5NF)
    - Sixth Normal Form (6NF)
