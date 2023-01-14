# **SQLite**  

## **Command Line Commands**  

### List databases commands

- `.databases`
- `.tables`

### Create database

- Navigate to folder containing sqlite tools
- `C:\tools\sqlite\`
- Run `sqlite3` command and name of database to be created
- `sqlite3 fancy_app.db`

### Create table

- In folder containing desired database:
    - SYNTAX: `create table table_name (value1 datatype constraint, value2 datatype);`
    - EXAMPLE: `create table users (ID int primary key, name VarChar(20));`

### Insert data

- SYNTAX: `insert into table_name (value1, value2) VALUES (actual_value1, actual_value2));`
- EXAMPLES: 
    - `insert into users (id, name) VALUES (0, "Tessa");`
    - `insert into users (id, name) VALUES (1, "Jason");`
    - `insert into users (id, name) VALUES (2, "Raj");`
    - `insert into users (id, name) VALUES (3, "Nelly");`

### Display data

- `select * from users;` Displays entire table
- `select ID from users;` Displays values in ID column
- `select name from users;` Displays values in name column
- `select ID from users where name="Tessa";` Displays values in ID column that matches a specifc value from name column

### Delete table

- SYNTAX: `drop table table_name`
- EXAMPLE: `drop table users` 