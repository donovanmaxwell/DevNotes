# **Object-Oriented Programming**

Object-oriented programming is primarily about isolating concepts into their own entities or, in other words, creating abstractions.

## **4 Pillars of OOP**

1. Abstraction
    - Only show the necessary details to the user of the object.
    - Decouples the user from the underlying implementation.
    - Sometimes called Abstraction of Data or Hiding of Data

2. Encapsulation
    - Basically binding together fields and methods that manipulate your data which keeps both safe from outside interference and misuse.

3. Inheritance
    - Allows code reusability.
    - Classes that are derived from existing classes are either called subclass or child classes and the class from which that subclass can be derived is called superclass or parent class.
    - Enables new objects to take on the properties of existing objects.
    - There are different ways in which Inheritance can be done.
        - Single Inheritance
            - A child class inherits the behavior from parent class
        - Multi-level Inheritance
            - Relation of Grand Parent to Parent to Child is followed.
        - Multiple Inheritance
            - Relation of one child with two parents is followed.
        - Hierarchical Inheritance
            - Relation of multiple children of one parent is followed.

4. Polymorphism
    - Basically the combination of two words “Poly” which means "Many" and “Morph” which means "Forms".
    - The ability to redefine methods for derived classes.

## **Important Concepts**

### Objects
An Object refers to an independent entity that contains both data (instance variables) and behavior (methods). Generally, each object has clearly defined boundaries and behaviors and is only aware of the objects that it needs to perform its task. 

The state of an object is the value of its internal variables at any given point in time.

### Classes
A class contains the blueprint needed to create objects, and also defines the objects' variables and methods. An object is created on the basis of the class constructor.

A class defines the types of objects that can be created from it. It contains instance variables describing the object's data, a constructor or constructors used to create it, and methods that define its behavior.