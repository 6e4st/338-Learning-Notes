# Week 1 Notes

## Overview

Week 1 focused on getting comfortable with the course workflow, IntelliJ, Git, GitHub Classroom, Java basics, unit tests, and object-oriented programming concepts. The main assignments were Lab 00 and Lab 01. The lecture material introduced Java syntax, static typing, primitive and reference types, objects, methods, encapsulation, access modifiers, UML diagrams, code style, and Javadoc comments.

---

## Lab 00

The goal of Lab 00 was to get familiar with IntelliJ, Git, GitHub Classroom, and writing Java code.

### Main Tasks

* Join the GitHub Classroom assignment.
* Clone the project repository to the local machine.
* Follow the instructions in the README.
* Watch and follow the Rectangle walkthrough videos.
* Work with `Rectangle.java`.
* Work with `RectangleTest.java`.
* Use IntelliJ code completion.
* Practice Git commands.
* Submit the correct Java files.

### Important Files

* `Rectangle.java`
* `RectangleTest.java`

### Important Ideas

Lab 00 introduced the connection between writing Java code and using tests to check that the code works correctly. `Rectangle.java` contained the main class being worked on, while `RectangleTest.java` was used to test whether the rectangle code behaved as expected.

The lab also introduced the idea that code must compile before it can be tested. If the code does not build, the tests cannot successfully run.

---

## Lab 01

The goal of Lab 01 was to continue building comfort with IntelliJ, Java, Git, and GitHub.

### Main Tasks

* Clone or continue using the Lab 00 repository.
* Create a branch such as `lab01/part1`.
* Follow the video walkthrough and README.
* Work through the Java files up to part 5.
* Submit a PDF with a link to the GitHub repository.
* Include a screenshot showing branches.
* Show merged branches or closed pull requests if possible.

### Important Ideas

Lab 01 emphasized using Git branches to organize work. Branches make it possible to work on a separate version of the code before merging it back into the main branch. This helps keep changes organized and makes it easier to track progress.

The lab also emphasized that each student must submit their own work. Code that does not compile receives no credit, so it is important to test and fix code before submitting.

---

## Git and GitHub

Git is used to track changes in code. GitHub is used to store repositories online and submit work through GitHub Classroom.

### Common Git Commands

* `git clone`: copies a repository from GitHub to the local machine.
* `git status`: shows which files have changed.
* `git branch`: shows branches in the repository.
* `git checkout -b branch-name`: creates a new branch and switches to it.
* `git add`: stages changed files.
* `git commit`: saves a snapshot of staged changes.
* `git push`: uploads local commits to GitHub.
* `git merge`: combines changes from one branch into another.

### Why Git Matters

Git helps track changes over time. It also makes it easier to recover from mistakes, organize work into branches, and show progress through commits and pull requests.

---

## Unit Tests

Unit tests are used to check whether small pieces of code work correctly. In Week 1, `RectangleTest.java` was used to test the behavior of `Rectangle.java`.

### Why Unit Tests Are Useful

* They give quick feedback.
* They help find mistakes.
* They check whether code matches expected behavior.
* They make it easier to test code as it is written.
* They help prevent errors from building up over time.

Unit tests are especially helpful because writing a lot of code without running or testing it can lead to many errors at once. Testing early helps catch problems sooner.

---

## IntelliJ

IntelliJ is the IDE used for writing and running Java code in this course.

### Useful IntelliJ Features

* Code completion helps finish code faster.
* Linter errors show problems while writing code.
* Red squiggly underlines can identify type errors or syntax problems.
* Hovering over an error can give more information.
* IntelliJ can run Java files and unit tests.

### Linter Errors

A linter error is a warning or error shown while writing code. These should be fixed as soon as possible because errors can build on each other. If the code has linter errors, it may not compile or run correctly.

---

## Java Is Statically Typed

Java is statically typed. This means that once a variable is declared as a certain type, it cannot store a different type of value.

Example:

```java
int foo = 42;
// foo = "hello"; // This would cause an error because foo is an int.
```

If a variable is declared as an `int`, Java will not allow a `String` to be stored in it.

---

## Primitive Types

Primitive types are basic Java data types.

### Java Primitive Types

* `byte`
* `short`
* `int`
* `long`
* `float`
* `double`
* `boolean`
* `char`

Primitive types store simple values.

---

## Reference Types and Wrapper Classes

Reference types are object types. They have methods and data. The data inside an object represents the state of that object.

### Wrapper Classes

Primitive types have corresponding reference types called wrapper classes.

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

Wrapper classes are useful because they provide methods and behave like objects.

---

## Boxing and Unboxing

Boxing means converting a primitive value into its wrapper class.

Example:

```java
Integer number = 42;
```

Unboxing means converting a wrapper class object back into a primitive value.

Example:

```java
int value = number;
```

Java can often do boxing and unboxing automatically.

---

## Functions and Methods

A function is a collection of code that can be called by name.

A method is a function that belongs to an object.

Methods are accessed using dot notation.

Example:

```java
foo.addition();
```

In this example, `addition()` is a method being called on the object `foo`.

---

## Objects

An object is a collection of data and methods that operate on that data. An object is an instance of a class.

Objects are responsible for maintaining their own state.

### State

The state of an object means the values it holds at a specific time. For example, if an object stores a name, score, or position, those values are part of its state.

A major goal in object-oriented programming is controlling and protecting an object's state.

---

## Four Pillars of Object-Oriented Programming

The four pillars of object-oriented programming are:

* Encapsulation
* Polymorphism
* Inheritance
* Abstraction

A helpful way to remember them is **PIEA**:

* Polymorphism
* Inheritance
* Encapsulation
* Abstraction

---

## Encapsulation

Encapsulation is a language mechanism for restricting direct access to some parts of an object. It also means bundling data together with the methods that operate on that data.

### Why Encapsulation Matters

Objects should control their own state. External code should not be able to directly change the internal state of an object without going through controlled methods.

Encapsulation helps make code safer because it limits what outside code can access or modify.

---

## Access Modifiers

Access modifiers control the visibility of classes, methods, and variables. In other words, they control who can access or modify parts of the code.

### Java Access Modifiers

| Modifier                      | Class | Package | Subclass | World |
| ----------------------------- | ----- | ------- | -------- | ----- |
| `public`                      | Yes   | Yes     | Yes      | Yes   |
| `protected`                   | Yes   | Yes     | Yes      | No    |
| no modifier / package-private | Yes   | Yes     | No       | No    |
| `private`                     | Yes   | No      | No       | No    |

### Public

`public` means the member can be accessed from anywhere.

### Protected

`protected` means the member can be accessed inside the class, package, and subclasses.

### Package-Private

Package-private happens when no modifier is written. It means the member can be accessed inside the class and package, but not by subclasses outside the package or the rest of the world.

### Private

`private` means the member can only be accessed inside the class where it is defined.

---

## Getters and Setters

Getters and setters are methods used to control access to an object's data.

### Getter

A getter returns a value.

Example:

```java
public String getName() {
    return name;
}
```

### Setter

A setter changes a value.

Example:

```java
public void setName(String name) {
    this.name = name;
}
```

Getters and setters support encapsulation because they allow controlled access to private data.

---

## UML Diagrams

UML stands for Unified Modeling Language. UML diagrams are used to show the structure of classes and relationships in a program.

A class diagram can show:

* Class name
* Attributes or member variables
* Methods
* Access levels
* Return types
* Parameter types

### UML Access Symbols

* `+` means public
* `-` means private
* `#` means protected
* `~` means package-private

### Example UML Layout

```text
------------------------
| ClassA               |
------------------------
| + attribute1 : int   |
| - attribute2 : String|
| # attribute3 : double|
| ~ attribute4 : boolean|
------------------------
| + method1() : void   |
| - method2(int) : String |
| # method3() : double |
| ~ method4() : boolean|
------------------------
```

UML diagrams can be made using tools like IntelliJ Ultimate, Draw.io, PowerPoint, Google Slides, pencil and paper, or a whiteboard.

---

## Java Style

The course expects Java code to follow common Java style rules.

### Style Rules

* Class names should be capitalized.
* File names should match class names.
* Every statement should use braces `{ }`.
* Braces should be placed on the same line as the statement.
* Code should include comments where appropriate.
* IntelliJ can auto-format code.

Example of preferred Java brace style:

```java
if (condition) {
    // code here
}
```

Not preferred:

```java
if (condition)
{
    // code here
}
```

---

## Javadoc Comments

Javadoc comments are special comments used to document methods.

A Javadoc comment starts with:

```java
/**
 *
 */
```

Each method that is created manually should have a Javadoc comment unless it is auto-generated or a simple getter/setter.

### Example

```java
/**
 * Returns a random action.
 * @return A String representing a generic action.
 */
private static String getRandomAction() {
    // method body
}
```

Javadoc is useful because it explains what a method does. In IntelliJ, hovering over a method can show the Javadoc information, which helps when using the method later.

---

## Main Takeaways

* Lab 00 introduced IntelliJ, GitHub Classroom, Java files, and unit tests.
* Lab 01 built more practice with Git branches, GitHub, Java files, and submitting work.
* Java is statically typed, so variables must hold values of the correct type.
* Primitive types store simple values.
* Reference types are objects and can have methods and data.
* Objects are responsible for maintaining their own state.
* Encapsulation protects an object's internal data.
* Access modifiers control visibility.
* Getters and setters provide controlled access to object data.
* UML diagrams help plan and understand class structure.
* Java style and Javadoc comments make code easier to read and maintain.
