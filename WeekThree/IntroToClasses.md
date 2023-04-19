# Introduction to Object-Orientated Programming with Classes.

When C++ was designed by Bjarne Stroustrup in 1985 at Bells Labs as a _superset_ of the C programming language.
By being a _subset_ of C, it means that while not all C++ code is valid C code, all C code is valid C++ code.
An example of this difference is _classes_, which are **abstract data types** (ADT) that are similar to the
structures that we learned about in week two. This is by design so that C++ could support the design pattern called
*OOP* or **Object Orientated Programming** which uses classes and objects to organize code to increase readability
and ability to be reused in other programs.

## What is a Class?
A class is an **abstract data type** that contains attributes and methods, which serves as a 'blueprint' for 
creating data objects.

For example, if I wanted to make a program that managed the distribution network of an online book store,
we could use the following code blocks.

```cpp
class Product {
    public:
        int priceInCents;
        int qtyInStock;
        string name;
};
```

Breaking down the above code line by line, we can see how a class is constructed.

Here we initalize a `class` object with the name of `Product`.
```cpp
class Product {
//    ...
};
```
Next we declare our **access specifier**, which defines how the attributes and methods of a class can be accessed
by the users of our program. In context of our above code, we're stating that we want _public_ access to `priceInCents`,
`qtyInStock`, and `name` attributes.
```cpp
    public:
        int priceInCents;
        int qtyInStock;
        string name;
```
There are in total three different access specifiers that we can utilize in our classes.
1. `public` - able to access from outside the class.
2. `private` - not able to access from outside the class.
3. `protected` - not available to outside the class, but can be interacted with when __inherited__ to a child class.

An example of the use case for a `private` access specifier would be something such as `creditCardNumber` for 
a `Customer` class.

#### Important Note: Private members of a class can be accessed from a public method inside the same class.

### Abstraction
Simplifying real world concepts into its essential elements.

### Encapsulation
Protecting data values by controlling with methods, separating the data from procedure.

### Inheritance
Layering of data fields and methods to make a group of classes flexible and efficient.

### Polymorphism
Ability of a method or data to be processed in multiple classes.

## Syntax

```cpp
// The below code is used to distinguish the implementation of a specific class as different from another
// person's implementation of a class.
#ifndef CAR_H
#define CAR_H

class Car {
    public:
        string make;
        string model;
        string color;
        int odometer;
        int year;
        // Constructor Method.
        Car(string make, string model, string color, int odometer, int year){
            make = make;
            model = model;
            color = color;
            odometer = odometer;
            year = year;
        }
    private:
        bool activeRental;
};

#endif
```

## Implementation


## Testing Classes


MORE INFO CAN BE FOUND ON PAGE 586 OF THE TEXTBOOK