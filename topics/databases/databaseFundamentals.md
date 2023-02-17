# **Database Fundamentals**

## **Terms & Concepts**

### **Index**

 Object that allows you to find specific data in a table. Work best when searching for a specific term.

 Types:

* Balanced-Tree (B-Tree) - Works like a tree with branches and leaves. Usually have less than 5 levels. Default type of index. Index on a column is not used if the query performs a function on that column.
  
    * `CREATE INDEX index_name ON table_name (columns);`
    * `CREATE INDEX idx_emp_id ON employee (id);`

* Function-based Index - Index created on the results of a function or expression.

    * `CREATE INDEX idx_emp_monthsalary ON employee (annual_salary / 12);`

* Clustered Index - Data in the table stored in the same way as data in the index. A type of index that defines how the data is stored in the table. Specifies that data in the table is stored in the same order as data in the index. Can only be one clustered index on a table.

    * `CREATE CLUSTERED INDEX idx_cust_id ON customer (cust_id);`

* Bitmap Index (Oracle) - Looks like a 2-dimensional map or table of values. Only available in Oracle SQL. 

    * `CREATE BITMAP INDEX idx_emp_status ON employee (status);`

### **Data Transport Object**

### **Difference Between DTO & POJO**

POJO describes an approach to programming (good old fashioned OOP). 

DTO is a pattern that is used to "transfer data" using objects.

While POJOs can be treated as DTOs, you run the risk of creating an anemic domain model if you do so. Additionally, there is a mismatch in structure, since DTOs should be designed to transfer data, not to prepresent the true structure of the business domain. The result of this is that DTOs tend to be more flat than your actual domain.

In a domain of any resonable complexity, your're almost always better off creating separate domain POCOs and translating them to DTOs.

### **Domain Object**

Objects from the business specific area that represent something meaningful to the domain expert. Domain objects are mostly represented by entities and value objects. Generally speaking, most objects that live in domain layer contribute to the model and are domain objects. 

An instance of a class that is related to your domain. 

A DTO's only purpose is to transfer state and should have no behavior, except for storage and trtrieval of its own data (accessors and mutators). It is an object that carries data between processes in order to reduce the number of method calls. 


### **Entity**

An object fundamentally defined not by its attributes, but by a thread of continutity and identity. (Meaning it must have Id). They hold data and have some internal knowledge of where it came from and where it's going to be saved, updated, etc.

### **POJO**

Plain Old %Insert_Language_Of_Choice_Here% Object

A simple object without complicated logic, usually it has just a few properties and is used with ORM or as a Data Transfer Object. 

References regular objects rather than framework-y things like Entity Beans.

Generally used as DTOs to carry data between layers, and the data is then commonly used to pupulate a domain object/entity.

### **Repository**

A Class that speaks to a data storage from one side (e.g. a database, a data service, or ORM) and to the service, UI, business layer or any other requesting body. It usually hides away all the data-related stuff (like replication, connection pooling, key constraints, transactions, etc) and makes it simple to just work with data. 

### **Service**

Software that provides some functionaliy, usually via public API. Depending on the layer, it can be a RESTful self-contained container, or class that allows you to find a particular instance of needed type. Usually provides a request-response functionality.

## **Interacting With Databases**

### JDBC

### Spring Data JPA

### ORM

### DAO

### Hibernate


