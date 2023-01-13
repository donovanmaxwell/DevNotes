# **PostgreSQL - Insert Statements**

## **INSERT Fundamentals**
Allows a new row to be inserted into an existing table.

### Example:  
(most basic syntax)  
```postgresql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

In this syntax: 
  
- Specify the name of the table `(table_name)` and a list of comma-separated columns `(column1, column2, ...)`
- Supply list of comma-separated values in parentheses `(value1, value2, ...)`. 
- The columns and values in both lists must be in the same order. 

The `INSERT` statement returns a command tag: 

```
INSERT oid count
```

`OID` is an object identifier. Typically, the `INSERT` statement returns `OID` with value 0. The `count` is the number of rows that the `INSERT` statement inserted successfully.

### RETURNING Clause

Optional clause that returns the info of the inserted row. 

If you want to return the entire inserted row, use an asterisk after the `RETURNING` keyword.

```postgresql
INSERT INTO table_name(column1, column2)
VALUES (value1, value2)
RETURNING *;
```

If you want to retutrn just some info of the inserted row, you can specify one or more columns after the `RETURNING` clause.

For example, the following statement returns the `id` of the inserted row:

```postgresql
INSERT INTO table_name(column1, column2)
VALUES (value1, value2)
RETURNING id;
```

## **INSERT Statement Examples**

### Inserting a single row into a table

```postgres
INSERT INTO links (url, name)
VALUES('https://fancy.website.io','Fancy Website');
```

### Inserting a date value

To insert a date value into a column with the `DATE` type, use the date in the format `YYYY-MM-DD`.

```postgres
INSERT INTO links (url, name, last_update)
VALUES('https://fancy.website.io','Fancy Website', '2022-12-03');
```

## Getting the last insert id

```postgres
INSERT INTO links (url, name)
VALUES('https://fancy.website.io','Fancy Website')
RETURNING id;
```