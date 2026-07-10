# Week 3 Notes

## Overview

Week 3 focused on design patterns, black-box testing, white-box testing, JavaFX, Gradle, and midterm preparation. The week also included work connected to Project 1 and the Week 3 Learning Journal, which involved reviewing code with classmates and comparing that review to an AI-generated code review.

The main technical topics were:

* Design patterns
* Command Pattern
* Interfaces, inheritance, and abstract classes
* Black-box testing
* White-box testing
* Equivalence class partitioning
* Boundary value analysis
* JavaFX
* Stage, Scene, and Scene Graph
* JavaFX event handling
* Gradle
* Constructor chaining with `this()` and `super()`

---

## Week 3 Intro

The Week 3 intro explained that this week had lighter new content because it also included midterm preparation. The major videos covered design patterns, black-box testing, white-box testing, and an introduction to JavaFX.

There was also a midterm prep assignment called **SuperMaker**, which was meant to help practice Java and reinforce ideas that would appear on the midterm.

The Week 3 Learning Journal focused on code review. Students were asked to work with two or three classmates, review code from the Shapes Labs, and give useful feedback.

---

## Week 3 Learning Journal Code Review

For the Week 3 Learning Journal, the focus was reviewing code from Lab 00, Lab 01, and Lab 02, also called the Shapes Labs.

### Code Review Topics

When reviewing code, important things to look for include:

* Variable names
* Logic
* Unused imports
* Comments
* Javadoc comments for non-generated methods
* Which unit tests pass
* Whether the tests were changed
* Whether feedback is clear and actionable

### Actionable Feedback

Good feedback should be specific enough that the person can act on it.

Example of weak feedback:

```text
Make it better.
```

This is not very helpful because it does not explain what to improve.

Example of actionable feedback:

```text
Move global variable declarations to the top of the file.
```

This is better because it gives a specific action the programmer can take.

### AI Code Review

The learning journal also asks students to use an AI tool to review one piece of code. The goal is to compare the AI review with the human review.

Important questions include:

* What prompt was used?
* Did the prompt need to be changed?
* How was the AI review different from the human review?
* Do I agree or disagree with the AI review?
* Was the AI feedback clear and useful?

---

# Design Patterns

## What Are Design Patterns?

Design patterns are reusable solution ideas for common software design problems. They are not exact copy-and-paste solutions. Instead, they are mental models that can be adjusted depending on the problem.

A design pattern is like a tool. It should be used when it fits the problem.

A helpful idea from the lecture is:

```text
A simple structure used cleverly is better than a clever structure used simply.
```

This means that complicated solutions are not always better. Sometimes a simple structure used well is the best solution.

---

## Sources for Design Patterns

The lecture mentioned three major sources for learning design patterns:

* *Design Patterns: Elements of Reusable Object-Oriented Software*
* *Game Programming Patterns*
* SourceMaking.com

The first book is known as the Gang of Four design patterns book. The lecture also mentioned that *Game Programming Patterns* explains design patterns through game programming examples.

---

## Categories of Design Patterns

Design patterns can be grouped into several categories.

### Creational Patterns

Creational patterns are about creating objects.

Examples:

* Singleton
* Factory Method
* Builder

### Structural Patterns

Structural patterns are about how objects and classes are arranged.

Examples:

* Flyweight
* Decorator

### Behavioral Patterns

Behavioral patterns are about how objects communicate and behave.

Examples:

* Command
* Memento
* Observer
* State
* Strategy

---

## Design Patterns and Inheritance

Many design patterns rely on inheritance, interfaces, abstract classes, or polymorphism. These patterns often use object-oriented programming ideas to make code more flexible.

Design patterns should be understood as ideas, not as finished solutions. They provide a structure that can be adapted to different programs.

---

# Command Pattern

## What Is the Command Pattern?

The Command Pattern turns a method or request into an object.

This means the action can be stored, passed around, repeated, changed, logged, queued, or undone.

The lecture described the Command Pattern as promoting the invocation of a method on an object to full object status.

Another way to think about it:

```text
A command object represents an action.
```

---

## Why the Command Pattern Is Useful

The Command Pattern is useful because it allows programs to treat actions like objects.

This makes it possible to:

* Store commands
* Repeat commands
* Undo commands
* Send commands over a network
* Change controls dynamically
* Queue or log requests
* Support replay systems

In game programming, this can be used for controls. For example, a button press can execute a command like jump, duck, attack, or move.

---

## Command Pattern Example

A command interface can define one required method.

Example:

```java
public interface ICommand {
    void execute();
}
```

A specific command class can implement the interface.

Example:

```java
public class JumpCommand implements ICommand {
    private final Player player;

    public JumpCommand(Player player) {
        this.player = player;
    }

    @Override
    public void execute() {
        player.jump();
    }
}
```

In this example:

* `ICommand` is the interface.
* `JumpCommand` implements the interface.
* `Player` is the receiver object.
* `execute()` calls the action.

---

## Controller Example

A controller can store command objects for different buttons.

Example:

```java
public class Controller {
    private final Player player;
    private ICommand aButton;
    private ICommand bButton;

    public Controller(Player player) {
        this.player = player;
        aButton = new JumpCommand(player);
        bButton = new DuckCommand(player);
    }

    public void pressA() {
        aButton.execute();
    }

    public void pressB() {
        bButton.execute();
    }
}
```

In this example, pressing a button does not directly call `player.jump()` or `player.duck()`. Instead, it executes the command object assigned to that button.

This allows the controls to be changed more easily.

---

## Command Pattern Checklist

The lecture gave a general checklist for implementing the Command Pattern:

1. Define a command interface with a method such as `execute()`, `do()`, or `activate()`.
2. Create one or more derived classes that represent specific commands.
3. Store the receiver object, method to call, and needed arguments.
4. Instantiate command objects for actions that should happen later.
5. Pass command objects from the creator to the invoker.
6. Let the invoker decide when to execute the command.

---

# Interfaces

## Interface Review

An interface defines required behavior.

A class that implements an interface must provide the methods listed by that interface.

Example:

```java
public interface IStone {
    void activate();
}
```

A class can implement the interface like this:

```java
public class PowerStone implements IStone {
    @Override
    public void activate() {
        // activation code
    }
}
```

---

## Interface Rules

Important interface rules from the lecture:

* Interfaces are declared similarly to classes.
* Interfaces use the `.java` file extension.
* The interface name and file name should match.
* Interfaces compile to `.class` files.
* Interfaces are implemented by classes.
* Interfaces can extend other interfaces.
* Interfaces cannot be instantiated.
* Interfaces do not contain constructors.
* Interface fields are `public static final`.
* Interface fields act like symbolic constants.

---

## Interfaces and Multiple Inheritance of Type

A Java class cannot extend multiple classes.

However, a Java class can implement multiple interfaces.

Example:

```java
public class Example implements InterfaceA, InterfaceB {
    // required methods from both interfaces
}
```

This is one major reason interfaces are useful. They allow a class to promise multiple types of behavior.

---

# Abstract Methods and Abstract Classes

## Abstract Methods

An abstract method is a method without a body.

Example:

```java
public abstract void activate();
```

Abstract methods can have:

* Parameters
* Return types
* Access modifiers

Abstract methods must be declared inside either an interface or an abstract class.

---

## Abstract Classes

An abstract class cannot be instantiated directly.

This means `new` will fail if used with an abstract class.

Example:

```java
public abstract class GameObject {
    public abstract void update();
}
```

A subclass can extend the abstract class and implement the abstract methods.

Example:

```java
public class Player extends GameObject {
    @Override
    public void update() {
        // update player
    }
}
```

### Abstract Class Rules

* Abstract classes cannot be directly instantiated.
* Abstract classes can be extended.
* Abstract classes can have fields.
* Abstract classes can have regular methods.
* Abstract classes can have abstract methods.

---

## Abstract Class vs Interface

Use an abstract class when:

* Code will be shared among closely related classes.
* The class needs access modifiers other than `public`.
* The design needs non-static or non-final fields.

Use an interface when:

* Unrelated classes should share behavior.
* The goal is to specify behavior but not implementation.
* Multiple inheritance of type is useful.

---

# Final Classes

A final class cannot be extended.

Example:

```java
public final class FinalExample {
    // class body
}
```

This means no other class can inherit from it.

---

# Constructor Chaining with `this()` and `super()`

## `this()` in Constructors

Inside a constructor, `this()` can call another constructor in the same class.

Example:

```java
public Example() {
    this(0);
}

public Example(int value) {
    // constructor code
}
```

## `super()` in Constructors

Inside a subclass constructor, `super()` can call a constructor from the superclass.

Example:

```java
public Child() {
    super();
}
```

## Why `this()` and `super()` Must Come First

Both `this()` and `super()` must be the first statement in a constructor.

This is because Java must establish the object construction chain before running the rest of the constructor body.

Important rules:

* A constructor can call another constructor in the same class using `this()`.
* A constructor can call a parent constructor using `super()`.
* If `this()` is used, it must be first.
* If `super()` is used, it must be first.
* A constructor cannot directly call both `this()` and `super()` because both would need to be first.
* If no `super()` call is written, Java tries to insert a no-argument `super()` call automatically.

---

# Black-Box Testing

## What Is Black-Box Testing?

Black-box testing is also called functional testing.

In black-box testing, the tester treats the software like a black box. The tester provides inputs and observes outputs without using the internal structure of the code.

The tester does not use:

* Source code
* Internal data
* Internal design documentation

Instead, the test cases are based on design specifications and expected behavior.

---

## Black-Box Testing Example

If testing a Celsius-to-Fahrenheit conversion program, the tester does not need to know how the formula is implemented in the code.

The tester gives an input temperature and checks whether the output is correct.

Example:

```text
Input: 0°C
Expected output: 32°F
```

---

## Equivalence Class Partitioning

Equivalence Class Partitioning, or ECP, is a type of black-box testing.

The idea is to divide possible inputs into groups. These groups are called equivalence classes.

Common groups include:

* Valid inputs
* Invalid inputs

The tester then runs at least one test case from each equivalence class.

### Example

For a program that accepts numbers from 0 to 100:

Valid class:

```text
0 through 100
```

Invalid classes:

```text
Less than 0
Greater than 100
Non-numeric input
```

A tester should choose values from each class.

---

## Boundary Value Analysis

Boundary Value Analysis focuses on values at the edge of equivalence classes.

Programs often fail at boundaries or edge cases.

Example range:

```text
0 <= x <= 1.0
```

Possible boundary tests:

```text
0
0.000001
0.5
0.999999
1.0
```

It is also useful to test just outside the boundaries.

Examples:

```text
-0.000001
1.000001
```

---

## Edge Cases and Unusual Inputs

Important edge cases include:

* Empty input
* Blank input
* Null values
* Repeated values
* Negative numbers
* Non-numeric input in numeric fields
* Values that are too large
* Values that are too small

Testing should include reasonable but incorrect assumptions developers might have made.

---

# White-Box Testing

## What Is White-Box Testing?

White-box testing is also called structural testing or glass-box testing.

In white-box testing, the tester can examine the internal structure of the program.

The tester may use:

* Source code
* Design documents
* Internal data
* Runtime behavior
* Algorithm steps

White-box testing focuses on implementation.

---

## White-Box Testing Goals

White-box testing can focus on:

* Control flow
* All possible paths through code
* Statement coverage
* Branch coverage
* Edge coverage

The goal is to make sure important parts of the code are tested.

---

## Control Flow Testing

Control flow testing looks at the paths that can be taken through code.

Example:

```java
read(x);
sum = 0;

if (x < 0) {
    x = -x;
}

while (x >= 0) {
    sum = sum + x;
    x = x - 1;
}

write(sum);
```

Useful test cases might include:

* A negative value
* Zero
* A positive value

These test cases help cover different paths through the `if` and `while` logic.

---

## Statement Coverage

Statement coverage means each statement should be executed at least once during testing.

This does not always mean every branch has been fully tested. A program can have every statement executed while still missing some possible decision outcomes.

### Important Idea

Statement coverage is useful, but it is not enough by itself.

---

## Black-Box vs White-Box Testing

| Testing Type      | Also Called                     | Focus                   | Tester Sees Code? |
| ----------------- | ------------------------------- | ----------------------- | ----------------- |
| Black-box testing | Functional testing              | Inputs and outputs      | No                |
| White-box testing | Structural or glass-box testing | Internal implementation | Yes               |

Both approaches are useful and work well together.

---

# JavaFX

## What Is JavaFX?

JavaFX is a GUI toolkit for Java. GUI means graphical user interface.

JavaFX is used to build Java programs with windows, buttons, labels, text fields, shapes, tables, charts, and other visual controls.

JavaFX replaced older Java GUI tools like Swing and AWT.

Since Java 11, JavaFX is available as a separate library called OpenJFX instead of being bundled directly with the JDK.

---

## JavaFX and OOP

JavaFX is based heavily on object-oriented programming.

The lecture emphasized that JavaFX is still just Java classes and inheritance.

Examples:

* A JavaFX app extends `Application`.
* UI controls are Java objects.
* Buttons, labels, and text fields inherit from JavaFX classes.
* Layout containers inherit from pane classes.

---

## JavaFX Application Lifecycle

A JavaFX app extends `javafx.application.Application`.

The main method calls `launch(args)`.

JavaFX then calls the `start(Stage primaryStage)` method.

Inside `start()`, the program builds the user interface and calls `stage.show()`.

Example:

```java
public class HelloWorldApp extends Application {
    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) {
        // build UI here
        primaryStage.show();
    }
}
```

Important steps:

1. `main()` calls `launch(args)`.
2. JavaFX takes control.
3. JavaFX calls `start(Stage)`.
4. The UI is built inside `start()`.
5. `stage.show()` displays the window.

---

## JavaFX Inheritance

`Application` is abstract, so a JavaFX app must override `start()`.

Simplified JavaFX hierarchy:

```text
Object
└── Node
    └── Parent
        └── Region
            ├── Control
            └── Pane
```

Examples:

* `Label`, `Button`, and `TextField` extend `Control`.
* `StackPane`, `VBox`, and `HBox` extend `Pane`.

This shows that JavaFX uses inheritance heavily.

---

## Stage, Scene, and Scene Graph

### Stage

The `Stage` is the operating system window.

It includes:

* Title bar
* Minimize button
* Maximize button
* Close button

### Scene

The `Scene` is the content area inside the window.

It contains the root node of the scene graph and defines the width and height of the content area.

### Scene Graph

The Scene Graph is the tree of visual nodes.

The root node is usually a layout container, such as `StackPane`.

Children can be controls, shapes, text, or other layout containers.

Example structure:

```text
Stage
└── Scene
    └── StackPane
        ├── Label
        ├── Button
        ├── Ellipse
        └── Text
```

---

## Creating JavaFX Controls

JavaFX controls are created using normal Java object construction.

Example:

```java
Label label = new Label("Hello World!");
Button mainButton = new Button("did it work?");
```

Shapes and text can also be created:

```java
Ellipse ellipse = new Ellipse(110, 70);
Text text = new Text("Ahh yiss shapes");
```

Properties are set using setter methods.

Example:

```java
ellipse.setFill(Color.GREENYELLOW);
text.setFont(new Font("Times New Roman", 24));
```

This connects to earlier course topics about objects, state, getters, and setters.

---

## Building the Scene Graph

A layout container can be used as the root node.

Example:

```java
StackPane root = new StackPane(label);
root.getChildren().addAll(mainButton, ellipse, text);

Scene scene = new Scene(root, 400, 300);

primaryStage.setTitle("JavaFX Hello World");
primaryStage.setScene(scene);
primaryStage.show();
```

Important ideas:

* `StackPane` stacks children on top of each other.
* `getChildren()` returns the children of the layout container.
* `addAll()` adds multiple nodes.
* `Scene` wraps the root node.
* `Stage` displays the scene.

---

## Layout Containers

Common JavaFX layout containers include:

### StackPane

Stacks children on top of each other, centered.

### VBox

Arranges children vertically from top to bottom.

### HBox

Arranges children horizontally from left to right.

### BorderPane

Divides the layout into five regions:

* Top
* Bottom
* Left
* Right
* Center

### GridPane

Arranges children in rows and columns.

---

# JavaFX Event Handling

## Events

An event is something that happens in a GUI program.

Examples:

* Button click
* Mouse movement
* Mouse entering a control
* Key press
* Window resize

JavaFX uses event handlers to respond to events.

---

## Lambda Expressions

A lambda expression can be used to write event-handling code concisely.

Example:

```java
mainButton.setOnAction(actionEvent -> {
    toggle(mainButton);
});
```

This code says that when the button action happens, the `toggle()` method should run.

---

## Anonymous Inner Classes

The same event handler can be written using an anonymous inner class.

Example:

```java
mainButton.setOnAction(new EventHandler<ActionEvent>() {
    @Override
    public void handle(ActionEvent e) {
        toggle(mainButton);
    }
});
```

Both approaches are valid, but lambdas are shorter and often easier to read.

---

## Functional Interfaces

`setOnAction()` expects an `EventHandler<ActionEvent>`.

`EventHandler` is a functional interface because it has one main method to implement.

That is why a lambda can be used.

---

## Mouse Events

JavaFX can also respond to mouse events.

Example:

```java
mainButton.setOnMouseEntered(new EventHandler<MouseEvent>() {
    @Override
    public void handle(MouseEvent mouseEvent) {
        double x = mainButton.getTranslateX();
        double cX = mouseEvent.getSceneX();
        System.out.println("Where does this print?");
    }
});
```

`System.out.println()` prints to the console or terminal, not to the GUI window.

---

## Helper Method Example: `toggle()`

A helper method can change the state of a button.

Example:

```java
private void toggle(Button button) {
    String label = button.getText();

    if (label.equalsIgnoreCase("Hello there!")) {
        label = "GENERAL KENOBI";
    } else {
        label = "Hello there!";
    }

    button.setText(label);
}
```

Important ideas:

* `getText()` gets the button text.
* `setText()` changes the button text.
* UI controls are objects with state.
* Changing the state of a control updates what appears in the window.

---

# Gradle

## What Is Gradle?

Gradle is an automated build tool.

It can:

* Compile code
* Manage dependencies
* Run the app
* Run tests
* Package the project

Gradle is useful for JavaFX because JavaFX is no longer bundled with the JDK. Gradle can download the needed JavaFX libraries automatically.

---

## Gradle and JavaFX

A JavaFX Gradle project uses plugins.

Example:

```gradle
plugins {
    id 'java'
    id 'application'
    id 'org.openjfx.javafxplugin' version '0.1.0'
}
```

Common plugins:

* `java`: compiles Java files
* `application`: adds the ability to run the app
* `org.openjfx.javafxplugin`: handles JavaFX setup

---

## Gradle JavaFX Configuration

Example:

```gradle
javafx {
    version = '21'
    modules = ['javafx.controls', 'javafx.fxml']
}

application {
    mainClass = 'HelloWorldApp'
}
```

This tells Gradle which JavaFX version and modules to use and what the main class is.

---

## Gradle Commands

Common commands:

```bash
./gradlew build
./gradlew run
./gradlew test
```

On Windows, the command may use:

```bash
gradle.bat run
```

### Important JavaFX Note

In IntelliJ, pressing the normal run button may show an error saying JavaFX runtime components are missing. The lecture explained that the components are not necessarily missing; IntelliJ may not know where to find them. Running the project through Gradle is the easier option.

---

# Main Week 3 Takeaways

* Design patterns are reusable mental models for solving common software design problems.
* Design patterns should be adapted to the problem, not blindly copied.
* The Command Pattern turns an action or request into an object.
* Command objects can be stored, executed, repeated, changed, or undone.
* Interfaces are important for defining shared behavior.
* Abstract classes can share code and define abstract methods.
* Java classes cannot extend multiple classes, but they can implement multiple interfaces.
* `this()` and `super()` must be first in a constructor.
* Black-box testing focuses on inputs and outputs without looking at code.
* White-box testing focuses on internal structure and implementation.
* Equivalence class partitioning divides inputs into valid and invalid groups.
* Boundary value analysis tests edge cases.
* JavaFX is a GUI toolkit for Java.
* JavaFX apps extend `Application` and override `start(Stage)`.
* A `Stage` is the window, a `Scene` is the content area, and the Scene Graph is the tree of nodes.
* JavaFX event handlers can use lambdas or anonymous inner classes.
* Gradle helps build and run JavaFX projects.
