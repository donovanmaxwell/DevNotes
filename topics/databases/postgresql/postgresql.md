# **PostgreSQL**  

## **Setup**

### **Configure Path in Environment Variables for `psql` Shell**

- Right click on Windows icon and click “System”

- Scroll down to “Advanced System Settings”

- Click Environment Variables

- In “System variables”, select "Path" and click Edit:

    - Click "New" to insert a new path variable

    - Enter location of `psql.exe` file
        - Example: `C:\Program Files\PostgreSQL\15\bin\psql.exe`
- Click Ok for each window opened during the process

### **PSQL Shell User Authentication Problem**
When first using `psql` shell, it initially is looking for a user that doesn't actually exist on the PostgreSQL server. To correct this so that the `psql` shell uses the correct username: 

- Right click on Windows icon and click “System”

- Scroll down to “Advanced System Settings”

- Click Environment Variables

- In “System variables”, click “New”:

    - Variable Name: PGUSER

    - Variable Value: postgres

If command prompt is currently running, close and reopen it. Going forward, `psql` will use postgres as the user name.


## **Fundamentals**  

### **Helpful Commands**

- `\?` Shows list of backslash commands available in `psql` shell
- `\h` Shows commands avaible in Help menu
- `\l` Lists databases on a server
- `\d` Lists all tables, views, and sequences in database
    - `\d table_name` Lists columns and their datatypes inside specified table
- `\dt` List all tables in a database
- `DROP DATABASE customer` Deletes specified database
    - This command is **dangerous**!
    - It will delete the entire databse immediately
- `DROP TABLE person` Deletes specified database
    - This command is **dangerous**!
    - It will delete the entire databse immediately


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
CREATE TABLE table_name (
    column1 datatype (length) column_constraint,
    column2 datatype (length) column_constraint,
    column3 datatype (length) column_constraint,
    table_constrants
);
```

- Specify name of table after `CREATE TABLE` keywords
- `IF NOT EXISTS` option is NOT supported by PostgreSQL
- Specify a comma-separated list of table columns. Each column consists of the column name, data type & length of data, and the column constraint.
- Specify table constraints, including primary key, foreign key, check, and unique constraints

### **EXAMPLE** 
```postgresql
CREATE TABLE accounts (
    user_id serial PRIMARY KEY,
    username VARCHAR (50) UNIQUE NOT NULL,
    password VARCHAR (50) NOT NULL,
    email VARCHAR (255) UNIQUE NOT NULL,
    created_on TIMESTAMP NOT NULL,
    last_login TIMESTAMP
);
```