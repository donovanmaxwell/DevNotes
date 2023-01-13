# **SQL Databases**

## **Glossary**

Cells
- The points where columns and rows interact
- Where the data is shown
- Cells without data are considered NULL

CONSTRAINTS
- Primary and Foreign Keys known as constraints
- "Rules" that are set in place as far as the types of data that can be entered

DEFAULT
- Sets a default value in a column when a value isn't provided

FOREIGN KEY
- Act as link between 2 or more tables
- Not always unique

INDEXES
- Constraints athat are created on a column that speeds up data retrieval
- Compiles all of the values in a column & treats them as unique value, even if not
- Best used on columns that:
    1. Do not have a unique constraint
    2. Are not a PK
    3. Are not a FK

NOT NULL
- Ensures that no value in that column is NULL

OBJECTS
- Components or items in a database
- Can range from tables, to columns, indexes, & triggers

PRIMARY KEY
- Constraint on a column that forces every value in that column to be unique

ROWS
- Entries within the table
- One line across

SCHEMA
- Logical container for groups of tables based on the data they hold

SEQUENCE
- A user defined scheme bound object that generates a sequence of numeric values (integers)
- Sequences are grequently used in many databases because many applications require each row in a  table to contain a unique value and sequences provide and easy way to generate them.
- The sequence of numeric values is generated in an ascending **or** decending order at defined intervals and can be configurd to restart when exceeds max_value.

STORED PROCEDURES
- Pre-compiled SQL syntax that can be used over & over again by executing its name in SQL Server.
- If running a certain query that you're running frequently & writing from scratch or saving the file and then opening it to run it, then it may be time to create a stored procedure out of that query. 

TABLE
- Holds the data
- Consist of columns that are the headers of the table
- Defined by data type

TRIGGERS
- A stored procedure that will execute when a certain event happends to a table
- Typically fire off when data is added, updated, or deleted

UNIQUE
- Enforces all values in a column are different

VIEW
- Virtual table that's comprised of one or more columns from one or more tables
- Created using SQL query
- Original code used to create the view is recompiled when a user queries that table
- Updates made in the originating tables will be pulled into the view to show current data
- Allow you to pull real-time data w/o touching the origin tables 
- **BEST PRACTICE** 
    - DO NOT update data in a view
    - Perform updates to data in the originating table(s)

    Two possible use cases:
    1. To hide the raw elements of the DB from the end-user so they only see what they need to. Can also make it more cryptic for the end user
    2. An alternative to queries that are frequently run in the DB.


## **Database Normalization**

**Form**
- Each step of normalization process
- Ranges from One to Five, 5 is highest normal form
- Typically can implement up to the 3rd normal form without negatively affecting functionality

Main goal is to maintain the integrity of the data, optimize efficiency of the DB, provide a more efficient method in tracking & storing data and help avoid any data issues along the way.

3 types of anomalies that can create issues in the DB if conditions of a normal form are not met:
1. **Insert Anomaly** Occurs when unable to add a new record unless other attributes exist already
2. **Update Anomaly** Occurs when one value needs to be changed in many places, rather than being changed only in 1 place
3. **Delete Anomaly** Occurs when there's data that we'd like to remove, but it it were to be removed, we'd be forced to remove other values we'd like to keep

Forms must be satisfied in order (from One to Five) before moving on to next form

- **First Normal Form (1NF)**
    - No multiple values can be used in a single cell
    - Eliminate repeating groups/columns of data
    - Identify the primary or composite key of each table

- **Second Normal Form (2NF)**
    - 1NF must be satisfied
    - Remove any non-key colums that's not dependent on the PK
    - Implement a FK

- **Third Normal Form (3NF)**
    - 2NF must be satisfied
    - Eliminate any transitive functional dependencies

- **Boyce-Codd Normal Form (BCNF)**
    - A stricter version of 3NF, where records within a table are considered unique
    - These unique values are based upon a composite key, which is created by a combination of columns

- **Fourth Normal Form (4NF)**
    - BCNF must be satisfied
    - Deals with isolating independent multi-valued dependencies, in which 1 specifiv value in a column has multiple values dependent on it

- **Fifth Normal Form (5NF)**
    - 4NF must be satisfied
    - Deals with multi-valued repationships being associated to one another & isolating said relationships
