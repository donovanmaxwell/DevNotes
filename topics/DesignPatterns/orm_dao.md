# **ORM vs DAO**

ORM and DAO are orthogonal concepts. One has to do with how objects are mapped to database tables, the other is a design pattern for writing objects that access data. You don't choose "between" them. You can have ORM and DAO in the same application, just as you don't need ORM to use the DAO pattern. 

**Note:** they aren't opposing concepts (they actually go together quite well). It isn't uncommon for your DAO to use an ORM.

A DAO that doesn't use an ORM would have to have code that looks a lot like what is [here](https://www.tutorialspoint.com/jdbc/jdbc-insert-records.htm). You can see that they have to manually open and close a connection to the DB, manually build SQL queries, and a lot of other messy stuff.

Using JPA (an ORM for Java), the code would look more like [this](https://www.objectdb.com/java/jpa/persistence/store) (look at the first code snippet). You can see that using an ORM you have an object that represents the data you want to save, then you simply call a method with it and the ORM handles all the complex stuff.