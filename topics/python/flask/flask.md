# Python Flask

## Flask Environment variables

avoid the inconvenience and stay consistent

so instead of using

```
export FLASK_APP=demo
```

we will just throw all of our necessary environment variables in a `.env` file

#### are environment variables specific to your venv?

They only exist for that process block

-   REST API must return JSON Serializable data

## REST API Response Codes

200 OK – the API request succeeded (general purpose)
201 Created – request to create a new record succeeded
204 No Content – the API request succeeded, but there is no response payload to return
400 Bad Request – the API request is bad or malformed and could not be processed by the server
404 Not Found – couldn’t find a record by ID

## REST API Security

Validate required fields, field types (e.g. string, integer, boolean, etc), and format requirements
Return 400 Bad Request with details about any errors from bad or missing data
Escape parameters that will become part of the SQL statement to protect from SQL injection attacks
Never allow SQL to be passed in the URL

## Databases Interaction in Flask

#### How to delete all tables and create new ones?

```
db.drop_all() #Deletes all existing tables
db.create_all() #Creates new databases
```

#### How to update or add flask models w/sqlalchemy

We need a migration tool

```
pip install flask-migrate
```

then if it is the first time initializing the database,

```
flask db init
```

If not and you just need to update an existing table then 

```
flask db migrate
```
and 

```
flask db upgrade
```

But if you need to add a new table you created,

**NOTE:** Make sure you have the model imported in the same file as this code: 

```
db.create_all()
```

That is just a method for creating all new databases with your SQLAlchemy object