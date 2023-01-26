# **Object-Relational Mapping**

**ORM:** An ORM usually describes a library/API used to make interactions with a database more robust. Java has an ORM called JPA, which allows you to persist Java objects directly to a database without having to generate your own SQL statements. You generate Java objects (often called entities) that match the columns/tables of a database, populate the Java object, then called persist(object). It knows how to store itself in the database. When you query the database for data, it will return it in the form of Java objects, instead of the nasty ResultSet that you get when you are using JDBC with SQL.