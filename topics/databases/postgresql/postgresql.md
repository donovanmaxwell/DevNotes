# **PostgreSQL**  

## **Fundamentals**  

### **Constraints**  
  
`NOT NULL`  

- Ensures that values in a column cannot be `NULL`

`UNIQUE`  

- Ensures the values in a column unique across the rows within the same table

`PRIMARY KEY`  

- Uniquely idendifies rows in a table
- Can only have **ONE** primary key.
- Primary key constraint allows you to define the primary key of a table

`FOREIGN KEY`  

- Ensures values in a column or a group of columns from a table exists in a column or group of columns in another table
- Tables can have multiple foreign keys

`CHECK`  

- Check constraint ensures the data must satisfy a boolean expression
  
## **CREATE TABLE Syntax**

```postgresql
CREATE TABLE [IF NOT EXISTS] table_name (
    column1 datatype (length) column_constraint,
    column2 datatype (length) column_constraint,
    column3 datatype (length) column_constraint,
    table_constrants
);
```

- Specify name of table after `CREATE TABLE` keywords
- `IF NOT EXISTS` option prevents errors due to create a table that already exists. When this option is used, PostgreSQL issues a notice instead of the error and skips creating the new table.
- Specify a comma-separated list of table columns. Each column consists of the column name, data type & length of data, and the column constraint.
- Specify table constraints, including primary key, foreign key, check, and unique constraints

### **EXAMPLE** 
```postgresql
CREATE TABLE [IF NOT EXISTS] accounts (
    user_id serial PRIMARY KEY,
    username VARCHAR (50) UNIQUE NOT NULL,
    password VARCHAR (50) NOT NULL,
    email VARCHAR (255) UNIQUE NOT NULL,
    created_on TIMESTAMP NOT NULL,
    last_login TIMESTAMP
);
```