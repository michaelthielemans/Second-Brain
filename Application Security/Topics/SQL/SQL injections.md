## Types of injections

### Retrieving hidden data

### Subverting application logic
When a query should give a result in a boolean form. You can login as a admin without entering the password. 
```
in the login name field you can enter:
administrator'--
'   -> will terminate the string
--  -> everything that will follow is a comment
```

### Retrieving data from other tables
Make use of UNION statement

### Examining the database
Try to gain knowledge about the type and version of the database, this will give you a better understanding which query language you need to use.

SELECT * FROM v$version
SELECT * FROM information_schema.tables

### Blind SQL injections

In this type of injection the application will not return a result in the form of a dataset for the query. Instead the application will behave differently depending on the values inside the query.