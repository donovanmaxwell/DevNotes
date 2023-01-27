# **Data Access Object**

**DAO:** A Data Access Object is a *pattern* that is often followed when an application needs to interact with some persistent data store (often a database). The DAO provides a series of operations to the rest of the application without the application needing to know the details of the data store. For example, there might be operations to retrieve a subset of data, update the data, or remove the data. It is much more generic than ORM - it simply is an object an application uses to retrieve data.

A DAO is an object that abstracts the implementation of a persistent data store away from the application and allows for simple interaction with it. A ORM is a robust library/API that provides a bunch of tools to save/retrieve an object directly to/from the database without having to write your own SQL statements.

The pattern lends itself to modularized code. You keep all the persistence logic in one place (separation of concerns, fight leaky abstractions). Allows testing of data access separately from the rest of the application.

DAOs are often table-centric. In many cases, DAOs match database tables

### **Separation of Concerns**

All persistence code is in one place, separated from the rest of the application. This makes the code more testable and maintainable. It also makes it easier to switch implementations later. If the code currently uses Hibernate-based DAOs, you can manipulate the session in the DAO. 

The anti-pattern to this is when persistence-related code happends outside of the persistence layer (see Law of Leaky Abstractions). 

### **Transactions**

Transactions are a bit trickier. At 1st glance, transactions might seem to be a concern of persistence, and they are. But they are not *only* a concern of persistence. Transactions are also a concern of your services, in that your service methods should define a 'unit of work', which means everything that happends in a service method should be atomic. If you use Hibernate transactions, then you are going to have to write Hibernate transactions code outside of the DAOs to define transaction boundaries around services that use many DAO methods.

NOTE: The transactions can be independent of your implementation. You need transactions whether or not you use Hibernate. Also note: You don't need to use the Hibernate transaction machinery. You can use container-based transactions, JTA transactions, etc. 

Transactions can be a pain. Spring makes these easier. The EJB spec also allows defining transactions around services with annotations. 

If using a service-based application approach you might see the services as the DAO. If there is no need for another level of abstraction, the DAOs in between are not needed. In bigger applications, let the services handle session and transaction management and redirect the actual work to the DAOs.

### **DAOs vs Repository Patterns**

- DAO is an abstranction of data persistence. A repository is an abstraction of a collection of objects.
- DAO is a lower-level concept, closer to the storage systems. Repository is a higher-level concept, closer to the Domain objects.
- DAO works as a data mapping/access layer, hiding the queries. A repository is a layer between domains and data access layers, hiding the complexity of collating data and preparing a domain object.
- DEO can't be implemented using a repository. However, a repository can use a DAO for accessing underlying storage. 

The repository pattern encourances a domain-driven design, providing an easy understanding of the data structure. 

## **DAO Pattern Sample**

Here, the JPA EntityManager interface is used to interact with underlying storage and provide a data access mechanism for the User domain.

1. Create domain class:
```Java
public class User {
    private Long id;
    private String userName;
    private String firstName;
    private String email;

    // getters & setters, etc.
}
```

2. Create the `UserDao` interface that privides simple CRUD operations for the `User` domain.
```Java
public interface UserDao {
    void create (User user);
    User read(Long id);
    void update(User user);
    void delete(String userName);
}
```

3. Create the `UserDaoImpl` class that implements the `UserDao` interface:
```Java
public class UserDaoImpl implements UserDao {
    private final EntityManager entityManager;

    @Override
    public void create(User user) {
        entityManager.persist(User);
    }

    @Override
    public User read(long id) {
        return entityManager.find(User.class, id);
    }

    // ...
}
```


