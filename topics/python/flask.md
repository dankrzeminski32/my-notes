# Python Flask

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



