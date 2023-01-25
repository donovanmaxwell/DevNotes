# Builder Design Pattern

What does the Builder Pattern do?
- It allows use to separate the construction of a more complex class, from the representation of the class.
- Creates a class who's sole purpose is to create the class we want.
- It takes certain specifications and returns a class based on these specs.

Builder pattern was introduced to sole some of the problems with Factory and Abstract Factory design patterns when the object contains a lot of attributes. There are 3 major issues with actory and Abstract Factory design patterns when the object contains a lot of attribute:

1. Too many arguments to pass from client program to the Factory class that can be error prone because most of the time, the type of arguments are same and grom client side its hard to maintain the order of the argument.
2. Some of the parameters might be optional but in Factory pattern, we are forced to send all the parameters and optional parameters need to send as NULL.
3. If the object is heavy and its creation is complex, then all that complexity  will be part of Factory classes, which creates confusion.

We create a class that contains all the state variables we need to set to create a functioning object. We have a setter for each of these values with "set" removed from the method name.

To implement builder design pattern:  
1. Create a static nested class and copy all the argyments from the outer class to the Builder class. Follow the naming convention. If the class name is `Computer` then the builder class should be named `ComputerBuilder`.
2. Builder class should have a public constructor with all the required attributes as parameters.
3. Builder class should have methods to set the optional parameters and it should return the same Builder object after setting the optional attribute(s).
4. Provide a `build()` method in the builder class that will return the object needed by client program. For this we need to have a private contructor in the class with Builder class as argument.

Builder uses the Fluent Interface idiom, which makes the code more readable when using the class.

The setter returns a builder object holding the value, and any other previously set values. This allows calls to be chained together, returning an instance of the object with everything configured.

| Game Builder |
|---|
| - awayTeam : String |
| - homeTeam : String |
| - currentYardLine : String |
| - stadium : String |
| - weather : String |
| awayTeam(String name) |
| homeTeam(String name) |
| currentYardLine(int position) |
| stadium(String name) |
| weather(String type) |

```Java
String homeTeam;

public GameBuilder homeTeam(String name) {
    homeTeam = name;
    return this;
}

public Game build() {
    if (homeTeam == null) {
        throw new IllegalStateException("Missing home team");
    }
    homeTeam = name;
    return this;
}

GameBuilder builder = new GameBuilder().homeTeam("Dallas");
Game game = builder.build();
```

If the builder can't build the instance, it should error out and not create the instance. In Java, the standard way to do this is throw an exception. `IllegalStateException` is the exception we throw when someone is trying to create the class in an illegal state.

```Java
Game footballGame = new GameBuilder()
    .homeTeam("Dallas")
    .awayTeam("San Francisco")
    .currentYardLine(35)
    .weather("Rain")
    .build();
```

Attributes can be specified in any order.

We use this pattern over chaining constructors because we can mix around the order of our state. It also allows us to prevent object creation in an inconsistent state. In the above example, a game instance can't be created where only one team is specified.

The builder will not return an instance until it has all the information needed to create the instance in a usable state. 

The builder pattern is overkill is only a few attributes need to be set. Chaining is a more simple solution for simple classes of only a few attributes. The builder patter is for larger, more complex class construction.

The builder is a nested static class inside the class to be built.

```Java

/*
Create the class with all the parameters needed.
Default values are set in the builder.
*/

public class Computer {

    // required parameters
    private String HDD;
    private String RAM;

    //optional parameters
    private boolean hasGraphicsCard;
    private boolean hasBluetooth;

    public String getHDD() {
        return HDD;
    }

    public String getRAM() {
        return RAM;
    }

    public boolean hasGraphicsCard() {
        return hasGraphicsCard;
    }

    public boolean hasBlueTooth() {
        return hasBlueTooth;
    }

    private Computer(ComputerBuilder builder) {
        this.HDD=builder.HDD;
        this.RAM=builder.RAM;
        this.hasGraphicsCard=builder.hasGraphicsCard;
        this.hasBluetooth=builder.hasBluetooth;
    }

    // Builder class
    public static class ComputerBuilder{
        // required parameters
        private String HDD;
        private String RAM;

        //optional parameters
        private boolean hasGraphicsCard;
        private boolean hasBluetooth;

        public ComputerBuilder(String hdd, String ram) {
            this.HDD=hdd;
            this.RAM=ram;
        }

        public ComputerBuilder setGraphicsCard(boolean hasGraphicsCard) {
            this.hasGraphicsCard=hasGraphicsCard;
            return this;
        }

        public ComputerBuilder setBluetooth(boolean hasBluetooth) {
            this.hasBluetooth=hasBluetooth;
            return this;
        }

        public Computer build() {
            return new Computer(this);
        }

    }
}
```

Note that Computer class has only getter methods and no public constructor. So the only way to get a Computer object is through the ComputerBuilder class.

Here is a builder pattern example test program showing how to use Builder class to get the object:
```Java
import com.computerapp.Computer;

public class TestBuilderPattern {
    public static void main(Args[] args) {
        /*
        Using builder to get the object in a single line of code and 
        without any inconsistent state or arguments management issues
        */
        Computer comp = new Computer.ComputerBuilder("1 TB", "32 GB").setGraphicsCard(true).setBluetoth(true).build();
    }
}
```


