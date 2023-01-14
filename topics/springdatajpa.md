# **Spring Data JPA**

Abstracts compexity needed to interact with databases.

An abstraction on top of JPA and Hibernate

**JPA** 

- Java Persistent API
- Specification for accessing persiting data and managing data between Java objects

**Hibernate** 

- Most popular implementation of JPA
- Persistence provider for JPA

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

### **Configuration**  

- Spring Boot configures Hibernate as the default JPA provider, so it's no longer necessary to define the entityManagerFactory bean unless we want to customize it.
- Spring Boot can also auto-configure the dataSource bean, depending on the database we're using. In the case of an in-memory database of type H2, HSQLDB and Apache Derby, Boot automatically configures the DataSource if the corresponding database dependency is present on the classpath.
- If we want to use JPA with MySQL database, we need the mysql-connector-java dependency. We'll also need to define the DataSource configuration.
- We can do this in a @Configuration class or by using standard Spring Boot properties.
- The Java configuration looks the same as it does in a standard Spring project:

```java
@Bean
public DataSource dataSource() {
    DriverManagerDataSource dataSource = new DriverManagerDataSource();

    dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
    dataSource.setUsername("mysqluser");
    dataSource.setPassword("mysqlpass");
    dataSource.setUrl(
      "jdbc:mysql://localhost:3306/myDb?createDatabaseIfNotExist=true"); 
    
    return dataSource;
}
```

To configure the data source using a properties file, we have to set properties prefixed with spring.datasource:

```java
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.username=mysqluser
spring.datasource.password=mysqlpass
spring.datasource.url=
  jdbc:mysql://localhost:3306/myDb?createDatabaseIfNotExist=true
```

Spring Boot will automatically configure a data source based on these properties.

In addition to the Spring Core and persistence dependencies we also need to define JPA and Hibernate in the project as well as a MySQL connector:

```xml
<dependency>
   <groupId>org.hibernate</groupId>
   <artifactId>hibernate-core</artifactId>
   <version>5.2.17.Final</version>
   <scope>runtime</scope>
</dependency>

<dependency>
   <groupId>mysql</groupId>
   <artifactId>mysql-connector-java</artifactId>
   <version>8.0.19</version>
   <scope>runtime</scope>
</dependency>
```

Note that the MySQL dependency is included here as an example. We need a driver to configure the data source, but any Hibernate-supported database will do.