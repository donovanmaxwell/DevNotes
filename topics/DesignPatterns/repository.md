# **Repository Pattern**

> The "repository is a mechanism for encapsulating sotrage, retrieval, and serch behavior, which emulates a collection of objects."
>> Domain-Driven Design, Chris Evans

> It "mediates between the domain and data mapping layers using a collection-like interface for accessing domain objects".
>> Patterns of Enterprise Application Architecture

In other words, a repository also deals with data and hides queries similar to DAO. However, it sits at a higher level, closer to the business logic of an app. 

Consequently, a repository can use a DAO to fetch data from the database and populate a domain object. Or, it can prepare the data from a domain object and send it to a storage system using a DAO for persistence. 

## **Repository Pattern Sample**

1. Create the interface:
```Java
public interface UserRepository {
    User get(Long id);
    void add(User user);
    void update(User user);
    void remove(User user);
}
```

2. Create the class providing an implementation of the interface:
```Java
public class UserRepositoryImpl implements UserRepository {
    private UserDaoImpl userDaoImpl;

    @Override
    public User get(Long id) {
        User user = userDaoImpl.read(id);
        return user;
    }

    @Override
    public void add(User user) {
        userDaoImpl.createUser(user);
    }

    // ...
}
```

Here, we've used the `UserDaoImpl` to send/retrieve data from the database. So far, we can say that the implementations of DAO and Repository look very similar because the User class is an anemic domain. Repository is just another layer over the data-access layer (DAO). 

However, DAO seems a perfect candidate to access the data, and a repository is an ideal way to implement a use-case.

## **Repository Sample Pattern with Multiple DAOs**

Sample imagines preparing a social media profile of a user by aggregating Twitter tweets, Facebook posts, and more.

1. Tweet

Create the Tweet class with a few properties that hold the tweet info:
```Java 
public class Tweet {
    private String email;
    private String tweetText;
    private Data dateCreated;

    // ... getters & setters
}
```

2. `TweetDao` and `TweetDaoImpl`

Similar to the `UserDao`, create the `TweetDao` interface that allows fetching tweets:
```Java
public interface TweetDao {
    List<Tweet> fetchTweets(String email);
}
```

Also, create the `TweetDaoImpl` class that provides the implementation of the `fetchTweets` method:

```Java
public class TweetDaoImpl implements TweetDao {
    @Override
    public List<Tweet> fetchTweets(String email) {
        List<Tweet> tweets = new ArrayList<Tweet>();

        // call Twitter API and prepare Tweet object

        return tweets;
    }
}
```

3. Enhance `User` Domain

Create the `UserSocialMedia` subclass of our `User` class to keep a list of the `Tweet` objects:

```Java
public class UserSocialMedia extends User {
    private UserDaoImpl userDaoImpl;
    private TweetDaoImpl tweetDaoImpl;

    @Override
    public user get(Long id) {
        UserSocialMedia user = (UserSocialMedia) userDaoImpl.read(id);

        List<Tweet> tweets = tweetDaoImpl.fetchTweets(user.getEmail());
        user.setTweets(tweets);

        return user;
    }
}
```

Here, the `UserRepositoryImpl` extracts user data using the `UserDaoImpl` and user's tweets using the `TweetDaoImpl`.

Then, it aggregates both sets of info and provides a domain object of the `UserSocialMedia` class that is handy for the business use-case. Therefore, a repository replies on DAOs for accessing data from various sources. 

The `User` domain can also be enhanced to keep a list of Facebook posts.