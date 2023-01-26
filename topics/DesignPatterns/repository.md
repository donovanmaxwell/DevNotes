# **Repository Pattern**

> The "repository is a mechanism for encapsulating sotrage, retrieval, and serch behavior, which emulates a collection of objects."
>> Domain-Driven Design, Chris Evans

> It "mediates between the domain and data mapping layers using a collection-like interface for accessing domain objects".
>> Patterns of Enterprise Application Architecture

In other words, a repository also deals with data and hides queries similar to DAO. However, it sits at a higher level, closer to the business logic of an app. 

Consequently, a repository can use a DAO to fetch data from the database and populate a domain object. Or, it can prepare the data from a domain object and send it to a storage system using a DAO for persistence. 