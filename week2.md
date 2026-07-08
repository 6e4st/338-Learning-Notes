# Week 2 Notes

## Overview

Week 2 focused on deeper Java object-oriented programming concepts. The main topics were static variables, static methods, wrapper classes, boxing and unboxing, the `Math` class, the `var` keyword, object comparison, `equals`, `hashCode`, `toString`, `@Override`, inheritance, interfaces, and `HashMap`.

---

## Static Variables

A static variable belongs to the class, not to a specific object.

This is different from an instance variable. An instance variable belongs to each object created from a class. A static variable is shared by all objects of that class.

### Example

```java
public class CarMade {
    private static int numOfCars = 0;

    public void demoMethod() {
        numOfCars++;
    }

    public void outputCount() {
        System.out.println("Number of cars so far = " + numOfCars);
    }
}
```

In this example, `numOfCars` is static, so every `CarMade` object shares the same variable.

### Important Ideas

* Static variables belong to the class.
* Instance variables belong to objects.
* All objects of the class can read or change the same static variable.
* Static variables should usually be private unless they are constants.

---

## Static Constants

A static constant uses `public`, `static`, and `final`.

Example:

```java
public static final int BIRTH_YEAR = 1982;
```

### Meaning of Each Keyword

* `public`: accessible outside the class
* `static`: belongs to the class
* `final`: value cannot be changed

When referencing a static constant from outside the class, use the class name.

Example:

```java
int year = MyClass.BIRTH_YEAR;
```

---

## Static Methods

A static method belongs to the class, not to an object.

A static method uses the `static` keyword in the method signature.

Example:

```java
public static double toCelsius(double degreesF) {
    return (5 * (degreesF - 32) / 9);
}
```

Static methods are called using the class name.

Example:

```java
Temperature.toCelsius(32);
```

### Static Method Rules

Static methods can:

* Call other static methods.
* Access static variables.

Static methods cannot:

* Directly call instance methods.
* Directly access instance variables.
* Use `this`.

---

## `this` in a Static Context

The keyword `this` refers to the current object instance.

Static methods do not belong to an object instance. They belong to the class. Because of this, there is no current object for `this` to refer to.

That is why using `this` inside a static method causes an error.

Example:

```java
public class Example {
    private String name;

    public static void staticMethod() {
        // System.out.println(this.name); // ERROR
    }
}
```

### Important Idea

If there is no object instance, there is no `this`.

---

## The Math Class

The `Math` class provides mathematical methods and constants.

No import statement is needed for `Math`.

All methods and data in the `Math` class are static.

### Common Math Constants

```java
Math.PI
Math.E
```

### Common Math Methods

```java
Math.pow(2.0, 3.0);
Math.abs(-42);
Math.min(42, 52);
Math.max(24, 42);
Math.round(41.57);
Math.ceil(41.3);
Math.floor(42.7);
Math.sqrt(1764);
```

### Important Idea

Because `Math` methods are static, they are called using the class name.

Example:

```java
double area = Math.PI * radius * radius;
```

---

## Wrapper Classes

Wrapper classes provide object versions of primitive types.

| Primitive Type | Wrapper Class |
| -------------- | ------------- |
| `byte`         | `Byte`        |
| `short`        | `Short`       |
| `int`          | `Integer`     |
| `long`         | `Long`        |
| `float`        | `Float`       |
| `double`       | `Double`      |
| `boolean`      | `Boolean`     |
| `char`         | `Character`   |

Wrapper classes contain useful constants and static methods.

### Examples

```java
Integer.MAX_VALUE
Integer.MIN_VALUE
Double.MAX_VALUE
Double.MIN_VALUE
Boolean.TRUE
Boolean.FALSE
```

---

## Boxing

Boxing is the conversion from a primitive value to a wrapper class object.

Example:

```java
Integer intObject = Integer.valueOf(42);
```

Automatic boxing can also happen.

Example:

```java
Integer intObject = 42;
```

---

## Unboxing

Unboxing is the conversion from a wrapper class object to the matching primitive value.

Example:

```java
int i = intObject.intValue();
```

Automatic unboxing can also happen.

Example:

```java
int i = intObject;
```

---

## Parsing and Converting Strings

Wrapper classes include static methods that convert strings into numbers.

Examples:

```java
Double.parseDouble("199.98");
Integer.parseInt("42");
Float.parseFloat("3.14");
```

Wrapper classes can also convert numeric values to strings.

Example:

```java
Double.toString(123.99);
```

---

## The `var` Keyword

The `var` keyword allows local variable type inference.

This means the compiler figures out the type based on the value on the right side.

Example:

```java
var name = "Carol";
var number = 42;
```

In this example, Java infers that `name` is a `String` and `number` is an `int`.

### Important Rules

* `var` only works for local variables.
* The compiler must be able to infer the type.
* `var` works in static and non-static contexts.
* `var` does not mean Java is dynamically typed.

---

## Comparing Objects with `==`

When comparing objects, `==` checks whether two references point to the same object in memory.

It does not check whether the objects contain the same values.

Example:

```java
Answer answer1 = new Answer();
Answer answer2 = new Answer();

System.out.println(answer1 == answer2); // false
```

Even if both objects contain the same data, they are two different objects in memory.

### Important Rule

Do not use `==` to compare object content.

---

## Comparing Strings

Strings are special in Java, but the safer rule is to use `.equals()` when comparing string content.

Example:

```java
String name1 = "Carol Danvers";
String name2 = "Carol Danvers";

System.out.println(name1.equals(name2));
```

### Important Idea

Use `.equals()` when checking whether two objects or strings have the same content.

---

## The `equals` Method

Every Java object inherits an `equals` method.

If a class does not override `equals`, it uses the closest parent version. If no parent class overrides it, the class uses `Object.equals`.

The default `Object.equals` behaves like `==`, meaning it checks whether two references point to the same object.

### Why Override `equals`

Override `equals` when you want to compare object content instead of memory location.

Example idea:

Two `Answer` objects might be considered equal if they both hold the same value, even if they are different objects in memory.

---

## The `hashCode` Method

When overriding `equals`, it is necessary to override `hashCode` too.

This is because Java has a contract between `equals` and `hashCode`.

### Important Rule

If two objects are equal according to `.equals()`, then they must return the same hash code.

The reverse is not always true. Two objects with the same hash code are not necessarily equal.

---

## The `toString` Method

The `toString` method controls what happens when an object is converted to a string or printed.

If a class does not override `toString`, printing the object usually shows a class name and hash code.

Example:

```java
System.out.println(myObject);
```

Without a custom `toString`, the output may not be useful.

### Why Override `toString`

Override `toString` to return a readable string representation of the object.

Example:

```java
@Override
public String toString() {
    return "Name: " + name + ", Value: " + value;
}
```

---

## `@Override`

`@Override` is an annotation.

It tells Java that a method is meant to replace a method inherited from a parent class or interface.

### Why `@Override` Is Useful

* It helps the compiler check that the method signature is correct.
* It makes the code clearer.
* It prevents mistakes when overriding inherited methods.

Example:

```java
@Override
public String toString() {
    return "Example object";
}
```

---
## `toString`, Shallow Copy, and Deep Copy

This lecture focused on the `toString` override method and the difference between shallow copy and deep copy.

---

## `toString` Override

The `toString` method creates a string representation of an object.

Every Java object already has a `toString` method because all objects inherit from the parent class `Object`.

If a class does not override `toString`, printing the object may show something like the class name plus a memory-style reference or hash code.

Example:

```java id="wv6zgq"
System.out.println(object);
```

Without a custom `toString`, the output may not clearly show the object's actual data.

### Why Override `toString`

It is usually a good idea to create a custom `toString` method for custom objects because it makes the object easier to read when printed.

Example:

```java id="c4knkn"
@Override
public String toString() {
    return "name=" + name + ", score=" + score + ", numbers=" + numbers;
}
```

In the lecture example, the object had fields such as:

* `name`
* `score`
* `numbers`

The custom `toString` printed these values instead of the default object reference.

---

## Object Aliases

An alias happens when two variables refer to the exact same object.

Example:

```java id="vzqxi5"
MyObject object1 = object;
```

This does not create a new object. It makes `object1` point to the same object as `object`.

If one reference changes the object, the other reference sees the same changes because both variables refer to the same object in memory.

### Important Idea

Assigning one object variable to another does not automatically make a copy.

---

## Copying Objects

A copy method can be used to create a new object based on an existing object.

Example idea:

```java id="ki4hy8"
MyObject object1 = MyObject.copy(object);
```

In the lecture example, the copy method was static, so it belonged to the class `MyObject`, not to a specific instance.

A copy method can create a new instance and copy over values from the original object.

---

## Shallow Copy

A shallow copy copies some values but may still share references to internal objects.

In the lecture example, `name` and `score` were copied, but the `numbers` list was still shared between the original object and the copied object.

That means changing the list in one object also changed the list seen by the other object.

### Important Idea

A shallow copy can leave two objects connected through shared internal references.

Example problem:

```java id="wc5qxh"
copy.setNumbers(original.getNumbers());
```

This copies the reference to the same list instead of creating a new list.

---

## Deep Copy

A deep copy creates a new object and also creates new copies of internal objects.

For the list example, a deep copy means creating a new `ArrayList` and copying each value into it.

Example:

```java id="a4z0sg"
List<Integer> numbersCopy = new ArrayList<>();

for (Integer i : original.getNumbers()) {
    numbersCopy.add(i);
}

copy.setNumbers(numbersCopy);
```

Now the copied object has its own separate list.

Changing the original list will not change the copied object's list.

---

## Deep Copy and Encapsulation

Deep copy helps preserve encapsulation.

Encapsulation means objects should control their own internal state. If two objects accidentally share the same internal list, then one object can affect the state of another object in unexpected ways.

A deep copy avoids this by making sure each object has its own independent copy of internal data.

---

## Main Takeaways

* `toString` creates a string representation of an object.
* Custom classes should often override `toString`.
* Assigning one object variable to another creates an alias, not a copy.
* A shallow copy may still share internal object references.
* A deep copy creates new copies of internal objects.
* Deep copy helps preserve encapsulation.
* When copying objects, be careful with fields that are objects or collections, such as `ArrayList`.


## Method Signatures

A method signature is the identifying part of a method.

The signature is determined by:

* Method name
* Parameters

When overriding a method, the method signature must match the inherited method.

If the signature does not match, the method is not actually overriding the parent method.

---

## Inheritance

Inheritance allows a new class to be created from an existing class.

The existing class is called the superclass, parent class, or base class.

The new class is called the subclass, child class, or derived class.

### Important Benefits

* Code reuse
* Less copy-paste
* Easier debugging and maintenance
* Ability to override methods
* Ability to extend classes with new fields and methods

---

## `extends`

The `extends` keyword is used to create a subclass.

Example:

```java
public class Book extends Product {
    // class body
}
```

In this example:

* `Product` is the superclass.
* `Book` is the subclass.

The subclass inherits accessible fields and methods from the superclass.

---

## Constructors and Inheritance

Constructors are not inherited.

A subclass constructor can call a superclass constructor using `super()`.

Example:

```java
public Book() {
    super();
}
```

If a subclass constructor does not explicitly call `super()`, Java automatically tries to call the no-argument constructor of the superclass.

### Important Rule

If the superclass does not have a no-argument constructor, and the subclass does not explicitly call a valid superclass constructor, the code will not compile.

---

## The `super` Keyword

The `super` keyword refers to the superclass.

It can be used to:

* Call a superclass constructor.
* Call a superclass method.
* Reuse superclass behavior inside an overridden method.

Example:

```java
@Override
public String toString() {
    return super.toString() + "Author: " + author + "\n";
}
```

This calls the parent class version of `toString()` and then adds more information.

---

## The `this` Constructor Call

Inside a constructor, `this()` can call another constructor in the same class.

Example:

```java
public ClassName() {
    this(param1, param2);
}
```

### Important Rule

If `this()` is used in a constructor, it must be the first line.

If `super()` is used in a constructor, it must also be the first line.

Because both must be first, a constructor cannot call both `this()` and `super()` directly in the same constructor body.

---

## Access Modifiers and Inheritance

Access modifiers affect what subclasses can access.

| Modifier        | Subclass Access                 |
| --------------- | ------------------------------- |
| `public`        | Accessible                      |
| `protected`     | Accessible                      |
| package-private | Accessible only in same package |
| `private`       | Not directly accessible         |

Private fields are not directly accessible in subclasses. A subclass should use public or protected getters and setters if available.

---

## Overriding Methods

A subclass can override an inherited method to customize behavior.

### Rules for Overriding

* The method must have the same signature.
* The method should use the `@Override` annotation.
* The subclass version replaces the superclass version when called on a subclass object.
* The subclass can still call the superclass version using `super`.

---

## Interfaces

An interface defines required behavior.

A class that implements an interface must provide the methods required by that interface.

### Important Ideas

* Interfaces describe what a class should do.
* Interfaces do not usually define exactly how the class should do it.
* A class uses `implements` to implement an interface.
* Interfaces support abstraction and polymorphism.

Example:

```java
public class MyClass implements MyInterface {
    // required methods go here
}
```

---

## Inheritance and Interfaces in UML

In UML diagrams:

* A solid line with a closed, unfilled arrowhead means `extends`.
* A dotted line with a closed, unfilled arrowhead means `implements`.
* The arrow points to the parent class or interface.

### Important Idea

Inheritance can refer to either extending a class or implementing an interface.

---

## The Object Class

Every Java class inherits from `Object`.

The `Object` class provides methods that all objects inherit, including:

* `toString`
* `equals`
* `hashCode`
* `clone`

This is why custom classes already have methods like `toString()` and `equals()`, even before those methods are written in the class.

---

## Polymorphism

Polymorphism allows objects to be treated as instances of their parent type.

For example, if `Book` and `Software` both extend `Product`, then both can be treated as `Product` objects.

### Important Idea

Polymorphism allows different subclasses to be grouped by their superclass while still behaving according to their own overridden methods.

---

## Abstract Classes

An abstract class is a class that cannot be directly instantiated.

Abstract classes can contain abstract methods.

An abstract method is a method without a body. A subclass must implement it unless the subclass is also abstract.

### Important Ideas

* Abstract classes support abstraction.
* They can define shared structure for subclasses.
* They can require subclasses to implement certain behavior.

---

## HashMap

A `HashMap` stores key-value pairs.

It is a generic container, like `ArrayList`, but it uses two type parameters.

Example:

```java
HashMap<String, Integer> fillings = new HashMap<>();
```

In this example:

* `String` is the key type.
* `Integer` is the value type.

### Important HashMap Rules

* Keys must be unique.
* Values can be repeated.
* The key type and value type are chosen when the `HashMap` is declared.
* If the same key is added twice, the new value overwrites the old value.
* Primitives cannot be used as key or value types; wrapper classes must be used instead.

---

## HashMap `put`

The `put` method adds or updates a key-value pair.

Example:

```java
HashMap<String, Integer> fillings = new HashMap<>();

fillings.put("lettuce", 1);
fillings.put("tomato", 2);
fillings.put("cheese", 1);
fillings.put("lettuce", 3);
```

The second `put("lettuce", 3)` overwrites the previous value for `"lettuce"`.

---

## HashMap `get`

The `get` method retrieves a value using a key.

Example:

```java
Integer lettuceCount = fillings.get("lettuce");
```

If the key does not exist, `get` returns `null`.

Example:

```java
Integer pickle = fillings.get("pickle"); // null
```

---

## Useful HashMap Methods

* `keySet()`: returns all keys.
* `containsKey(key)`: checks whether a key exists.
* `containsValue(value)`: checks whether a value exists.
* `remove(key)`: removes a key-value pair.
* `size()`: returns the number of entries.

---
## Generics

Generics in Java are containers that can hold a specific type of object. A generic lets the programmer define what type of data the container should store.

For example, a `List<Integer>` is a list that stores `Integer` objects.

```java
List<Integer> numbers = new ArrayList<>();
```

In this example, the list is named `numbers`, and it can store `Integer` values. Since `List` and `ArrayList` come from the Java utility library, they need to be imported from `java.util`.

```java
import java.util.List;
import java.util.ArrayList;
```

A generic container can store Java objects or custom objects. It cannot directly store primitive types like `int`, but it can store wrapper classes like `Integer`.

---

## List and ArrayList

A `List` is a generic type that can hold a collection of objects. An `ArrayList` is one implementation of a `List`.

Example:

```java
List<Integer> numbers = new ArrayList<>();
numbers.add(7);
numbers.add(42);
```

The `add` method adds values to the list.

The `size` method returns how many objects are in the list.

```java
System.out.println(numbers.size());
```

---

## HashMap as a Generic

A `HashMap` is also a generic container. It stores key-value pairs.

A `HashMap` takes two type parameters:

* the key type
* the value type

Example:

```java
HashMap<String, Integer> bookList = new HashMap<>();
```

In this example:

* `String` is the key type.
* `Integer` is the value type.
* The keys are book titles.
* The values are the number of copies.

---

## HashMap Example

```java
HashMap<String, Integer> bookList = new HashMap<>();

bookList.put("Interesting Times", 10);
bookList.put("Advanced Game Design", 2);
bookList.put("Eye of the World", 14);
bookList.put("Dune", 12);
```

The `put` method adds a key-value pair to the map.

In this example, the book title is the key, and the number of copies is the value.

---

## Useful HashMap Methods from the Demo

The lecture demo showed several useful `HashMap` methods:

* `put(key, value)`: adds a key-value pair.
* `size()`: returns how many entries are in the map.
* `keySet()`: returns all keys.
* `values()`: returns all values.
* `entrySet()`: returns all key-value pairs.
* `containsKey(key)`: checks whether a key exists.
* `containsValue(value)`: checks whether a value exists.
* `get(key)`: returns the value connected to a key.

Example:

```java
System.out.println(bookList.keySet());
System.out.println(bookList.values());
System.out.println(bookList.entrySet());
```

---

## Enhanced For Loop / For-Each Loop

An enhanced for loop, also called a for-each loop, can be used to loop through a collection.

Example:

```java
for (String key : bookList.keySet()) {
    System.out.println("We have " + bookList.get(key) + " copies of " + key);
}
```

This loop goes through each key in the `HashMap`. For each key, it gets the value connected to that key using `bookList.get(key)`.

Example output could be:

```text
We have 10 copies of Interesting Times
We have 2 copies of Advanced Game Design
We have 14 copies of Eye of the World
We have 12 copies of Dune
```

---

## Important Generics Takeaways

* A generic is a container that relies on the programmer to define what it holds.
* `List<Integer>` means a list that stores `Integer` objects.
* `HashMap<String, Integer>` means a map with `String` keys and `Integer` values.
* Generic containers hold objects, not primitive types.
* Use wrapper classes like `Integer` instead of primitive types like `int`.
* `HashMap` stores key-value pairs.
* `keySet()` gives the keys.
* `values()` gives the values.
* `entrySet()` gives all key-value pairs.
* An enhanced for loop can loop through keys and use `get(key)` to access values.

## Markov Chain Connection

The Markov assignment uses a `HashMap` to keep track of words and the words that follow them.

A first-order Markov chain looks at the current word and predicts or selects a possible next word.

### Basic Process

* Read text from a file.
* Split the text into words.
* Store each word as a key in a `HashMap`.
* Store words that follow it as values.
* Use the map to generate new text.

### Important Idea

A first-order Markov chain only looks back one token. It tracks the current word and possible next words.

---

## Main Takeaways

* Static variables and methods belong to the class, not an object.
* Instance variables and instance methods belong to objects.
* `this` cannot be used in a static context because there is no current object.
* The `Math` class uses static methods and constants.
* Wrapper classes provide object versions of primitive types.
* Boxing converts primitives to wrapper objects.
* Unboxing converts wrapper objects to primitives.
* `var` lets Java infer local variable types.
* `==` compares object references, not object content.
* `.equals()` should be used to compare object content.
* If `equals` is overridden, `hashCode` should also be overridden.
* `toString` controls how an object is printed as text.
* `@Override` helps safely replace inherited methods.
* Inheritance allows subclasses to reuse and customize superclass behavior.
* `super` refers to the parent class.
* Interfaces define required behavior.
* `HashMap` stores key-value pairs and is useful for fast lookup.
