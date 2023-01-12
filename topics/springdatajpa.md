# **Spring Data JPA**

Abstracts compexity needed to interact with databases.

An abstraction on top of JPA and Hibernate

**JPA** - Java Persistent API
- Specification for accessing persiting data and managing data between Java objects

**Hibernate** - Most popular implementation of JPA

### **application.properties**
Configuration file for basic Spring Data JPA properties, such as:
- URL, username, and password
- Hibernate dialect and format
- SQL properties

### **pom.xml**
Maven configuration file

Need to add Spring Boot, SPring Data JPA, and driver for database (PostgreSQL, SQLite, SQL, etc)

### **Tables & Classes** 
- Need to specify Table and Entity annotations in class
- Tables are configured as Java Classes
- Instance variables in class need to match table column entries
- Use @Entity from javax.persistence.Entity package, not from Hibernate
- @Entity maps the class to a table in the database
- **BEST PRACTICE** specify name of the entity, i.e., @Entity(name="Student") for Student.java (default does this automatically)
- Need to specify Primary Key with @Id annotation above ID instance variable