# Week 4 Notes

## Overview

Week 4 focused on software design and application structure. The main topics were use case modeling, user stories, GitHub issues, the Factory Pattern, Scene Factory in JavaFX, SQLite, JDBC, `DatabaseManager`, CRUD operations, and a preview of the Observer Pattern.

This week also included the midterm. There were no regular quizzes because the midterm took their place.

---

# Week 4 Intro

Week 4 was described as the halfway point of the course. The main content was less technically difficult than some earlier weeks, but it focused on important software design ideas.

The major goal was learning how to think about what software should do before building it. This included use case modeling and user stories.

The week also introduced Scene Factory and SQLite in JavaFX, which connects JavaFX applications to better design patterns and local data storage.

---

# Requirements Analysis

## What Is Requirements Analysis?

Requirements analysis is the phase where developers try to understand the problem and requirements clearly.

It helps create an agreement between the client and the developer.

A requirement describes **what** the system should do, not **how** the system should do it.

For a medium-sized system, requirement specifications can become very long and detailed.

---

## Why Requirements Matter

Good requirements help developers understand:

* Who will use the system
* What users need to do
* What the system must support
* What the system should not do
* How to turn vague ideas into specific tasks

Requirements are especially important when working with AI tools because an AI will produce better code if the requirements and design are clear.

A vague prompt like this is not very useful:

```text id="0bj6fx"
Make me an app that does stuff.
```

A better prompt or requirement explains the user, goal, and expected behavior.

---

# Software Process

A software process is a set of phases in software development.

Common phases include:

* Requirements analysis
* Design
* Coding
* Testing
* Maintenance

The older waterfall model treated these phases as separate steps that happened in order. In practice, software development is usually more flexible than that. Requirements, design, code, and tests can change as the project develops.

Modern development often follows an Agile process, where teams work in sprints and repeatedly revisit requirements, design, coding, and testing.

---

# Use Cases

## What Is a Use Case?

A use case describes how an actor interacts with a system to complete a task.

A use case should describe the user’s interaction with the system, not the internal computations the system performs.

A use case usually includes:

* Actor
* Flow of events
* Postconditions

The goal of use case analysis is to model the system from the user’s point of view.

---

## Important Use Case Questions

When designing a system, ask:

* Who is going to use it?
* Where will it be used?
* How will it be used?
* What is the actor trying to do?
* What actions happen between the actor and the system?

---

## Actors

An actor is a role that interacts with the system.

An actor can be:

* A person
* Another system
* A machine
* An external device
* Software outside the system

An actor is outside the system and usually outside the control of the system.

### Examples of Actors

For a telephone switching system:

* Caller
* Callee
* Customer

For an ATM system:

* Account holder
* Bank
* Maintenance worker
* ATM itself
* Thief or robber

---

## Flow and Activity

A use case includes the flow of interaction.

Important terms:

* **Actor**: who or what is doing the thing
* **Flow**: how the information or actions interact
* **Activity**: what is being done

Example:

```text id="3ngp6h"
Actor: Caller
Activity: Place campus call
Flow: Caller enters a number, system connects to callee, call begins.
```

---

## Use Case Example: Telephone Switching System

Problem:

CSUMB wants a simple telephone switching system because internal calls currently cost too much money. The old system charges 10 cents per call, and the new system should reduce that to 1 cent per call.

Possible actors:

* Caller
* Callee
* Customer

Possible use cases:

* Place campus call
* Receive campus call
* Get call history
* View bills
* Access voicemail
* Use caller ID

---

# User Stories

## What Is a User Story?

A user story is a short description of what a user wants to do and why.

User stories are smaller and more focused than use cases.

A common format is:

```text id="lxem53"
As a [user], I want to [do something], so that [reason].
```

Example:

```text id="sx82u1"
As a campus telephone system user, I want to be able to make calls.
```

Another example:

```text id="o59jbe"
As a CSUMB phone system caller, I want to enter a number so I can connect to another person.
```

---

## User Story vs Use Case

| Use Case                              | User Story                      |
| ------------------------------------- | ------------------------------- |
| Bigger picture                        | Smaller and more focused        |
| Actor, flow of events, postconditions | Role, goal, acceptance criteria |
| Details actor-system interaction      | Briefly tells a story           |
| Describes a full task                 | Describes a user need           |

---

## The Three Cs

User stories focus on the three Cs:

* Card
* Conversation
* Confirmation

### Card

The short written version of the user story.

### Conversation

The discussion between the developer and the client/user about what the story really means.

### Confirmation

The acceptance criteria that prove the story is complete.

---

## Acceptance Criteria

Acceptance criteria explain how to know when a user story is finished.

Example user story:

```text id="gbwy5y"
As a user, I want to log in so that I can access my account.
```

Possible acceptance criteria:

* User can enter a username.
* User can enter a password.
* System rejects incorrect credentials.
* System allows access with correct credentials.
* User sees an error message if login fails.

---

# Turning Stories into GitHub Issues

User stories can be turned into GitHub issues.

GitHub issues help organize work into smaller tasks.

A good issue should include:

* Title
* User story
* Description
* Acceptance criteria
* Notes or requirements
* Possible tasks

Example issue:

```markdown id="6nv6fe"
## User Story

As a GymLog user, I want to save my workouts so that I can access them later.

## Acceptance Criteria

- User can enter a workout name.
- User can enter workout details.
- User can save the workout.
- Saved workouts persist after closing the app.
- User can view saved workouts later.
```

---

# Design Patterns Review

A design pattern is a reusable solution to a common software design problem.

Design patterns are not exact copy-and-paste solutions. They are reusable mental models that can be adapted to fit the problem.

Design patterns are often grouped into three families:

| Category   | Concern                  |
| ---------- | ------------------------ |
| Creational | How objects are made     |
| Structural | How objects are composed |
| Behavioral | How objects communicate  |

Week 4 focused mainly on the **Factory Pattern**, which is a creational pattern.

---

# Single Responsibility Principle

## What Is the Single Responsibility Principle?

The Single Responsibility Principle, or SRP, says:

```text id="36m4t0"
A class should have one, and only one, reason to change.
```

This means a class should focus on one main job.

---

## Main.java Responsibility

In a JavaFX app, `Main.java` should be responsible for:

* Bootstrapping the JavaFX runtime
* Showing the first scene
* Cleaning up when the app closes

`Main.java` should not be responsible for:

* Building every button and label
* Knowing the internal layout of every screen
* Mixing UI construction with application logic

---

# The Problem: start() Gets Messy

In JavaFX, the `start(Stage stage)` method can become very large if all scenes, buttons, labels, layouts, and event handlers are built inside it.

This creates a code smell called a **God Method**.

A God Method is one method doing too much.

Problems with a God Method:

* Hard to read
* Hard to test
* Hard to change
* Easy to break
* Mixes too many responsibilities

The solution is to move scene construction into a separate class.

---

# Factory Pattern

## Core Idea

The Factory Pattern moves object creation into a separate class.

In this case, `Main.java` asks for a scene, and `SceneFactory` builds and returns it.

Basic idea:

```text id="m3vd96"
Main.java -> asks SceneFactory for a Scene -> SceneFactory returns Scene
```

Roles:

| Role    | Example        |
| ------- | -------------- |
| Client  | `Main.java`    |
| Factory | `SceneFactory` |
| Product | `Scene`        |

---

## Why Use a Factory?

A factory helps separate responsibilities.

Without a factory:

* All scene code lives in `Main.java`.
* Adding a scene means editing a large method.
* UI and logic are tangled.
* Scene construction is hard to test.

With a factory:

* Scene code is moved into private builder methods.
* `Main.java` stays clean.
* Scene construction is centralized.
* Adding scenes is more organized.
* Code is easier to test and maintain.

---

# SceneType Enum

## Why Use an Enum?

A `SceneType` enum identifies each scene in the application.

Example:

```java id="nbucn8"
public enum SceneType {
    MAIN,
    LOGIN,
    DASHBOARD
}
```

Using an enum is better than using strings because:

* It is type-safe.
* The compiler rejects unknown values.
* IntelliJ can autocomplete values.
* A switch expression can be exhaustive.
* Renaming is easier and safer.

---

# SceneFactory

## SceneFactory Shell

`SceneFactory` is the class responsible for creating scenes.

Example:

```java id="33h31p"
import javafx.scene.Scene;
import javafx.stage.Stage;

public class SceneFactory {

    public static Scene create(SceneType type, Stage stage) {
        return switch (type) {
            case MAIN -> buildMainScene(stage);
            case LOGIN -> buildLoginScene(stage);
            case DASHBOARD -> buildDashboardScene(stage);
        };
    }

    private static Scene buildMainScene(Stage stage) {
        return null;
    }

    private static Scene buildLoginScene(Stage stage) {
        return null;
    }

    private static Scene buildDashboardScene(Stage stage) {
        return null;
    }
}
```

The public `create()` method is the entry point.

The private `build*Scene()` methods contain the actual scene construction.

---

## Exhaustive Switch

The switch expression is exhaustive.

This means if a new `SceneType` is added, the compiler can warn that `SceneFactory` does not handle it yet.

This helps prevent bugs when adding new screens.

---

## Building a Scene in SceneFactory

Example:

```java id="wm81ab"
private static Scene buildMainScene(Stage stage) {
    Label title = new Label("Welcome to Todo App");
    title.setStyle("-fx-font-size: 20px; -fx-font-weight: bold;");

    Button goBtn = new Button("Open Dashboard");
    goBtn.setOnAction(e ->
        stage.setScene(create(SceneType.DASHBOARD, stage))
    );

    VBox layout = new VBox(16, title, goBtn);
    layout.setAlignment(Pos.CENTER);

    return new Scene(layout, 600, 400);
}
```

This method:

* Builds the label
* Builds the button
* Sets the button action
* Builds the layout
* Returns a new scene

The scene construction is now isolated inside the factory.

---

# Clean Main.java

Before using a factory, `Main.java` might contain many lines of UI setup.

After using `SceneFactory`, `Main.java` can be much cleaner.

Example:

```java id="mvlsfl"
@Override
public void start(Stage stage) {
    stage.setTitle("Todo App");
    stage.setScene(SceneFactory.create(SceneType.MAIN, stage));
    stage.show();
}
```

Now `Main.java` only starts the app and shows the first scene.

---

# Open/Closed Principle

The Open/Closed Principle says:

```text id="j84wzi"
Classes should be open for extension, closed for modification.
```

This means code should be designed so new behavior can be added without constantly changing existing working code.

With `SceneFactory`, adding a new scene usually means:

* Add a value to `SceneType`
* Add a new private `build*Scene()` method
* Add a new switch case

---

# SQLite

## What Is SQLite?

SQLite is a self-contained, serverless SQL database engine.

Important features:

* The entire database lives in one file.
* No server process is required.
* It supports SQL.
* It supports tables, selects, joins, transactions, and constraints.
* It is useful for local data storage.
* It is good for desktop apps and prototypes.

SQLite is commonly used in:

* Desktop apps
* Mobile apps
* Browsers
* Local storage systems
* Offline-first apps

SQLite is not designed for high-concurrency multi-user server backends.

---

# JDBC

## What Is JDBC?

JDBC stands for Java Database Connectivity.

It is the standard Java API for connecting to databases.

A Java program can use JDBC to:

* Connect to a database
* Send SQL commands
* Read query results
* Insert data
* Update data
* Delete data

---

# Adding SQLite to Gradle

To use SQLite in a JavaFX/Gradle project, add the SQLite JDBC driver to `build.gradle`.

Example:

```gradle id="47g95u"
dependencies {
    implementation 'org.xerial:sqlite-jdbc:3.46.1.3'
}
```

After changing `build.gradle`, sync the Gradle project.

---

# DatabaseManager

## What Is DatabaseManager?

`DatabaseManager` is a class responsible for database work.

It should handle:

* Connecting to the database
* Creating tables
* Inserting data
* Reading data
* Updating data
* Deleting data

This keeps database code separate from UI code.

---

## Why Use DatabaseManager?

Without a `DatabaseManager`, database logic might be scattered throughout scene-building code.

That would make the program harder to:

* Read
* Test
* Debug
* Maintain
* Update later

Using `DatabaseManager` supports separation of concerns.

---

# Creating a Database Connection

SQLite uses a database file.

Example database URL:

```java id="3pbx4c"
private static final String DB_URL = "jdbc:sqlite:app.db";
```

A connection can be opened using `DriverManager`.

Example:

```java id="xvz4fd"
Connection conn = DriverManager.getConnection(DB_URL);
```

---

# Creating Tables

Creating tables is called DDL, or Data Definition Language.

Example:

```java id="ao055m"
String sql = """
    CREATE TABLE IF NOT EXISTS tasks (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        title TEXT NOT NULL,
        completed INTEGER NOT NULL DEFAULT 0
    );
""";
```

This creates a `tasks` table if it does not already exist.

---

# CRUD Operations

CRUD stands for:

* Create
* Read
* Update
* Delete

These are the four basic database operations.

---

## Create: INSERT

Create means adding new data.

Example:

```sql id="2n5yhz"
INSERT INTO tasks (title, completed)
VALUES ('Study Java', 0);
```

In Java, an INSERT would usually be done through JDBC using a SQL string and a prepared statement.

---

## Read: SELECT

Read means retrieving data.

Example:

```sql id="dd472v"
SELECT id, title, completed
FROM tasks;
```

A Java program can use a `ResultSet` to loop through the returned rows.

---

## Update: UPDATE

Update means changing existing data.

Example:

```sql id="go5hka"
UPDATE tasks
SET completed = 1
WHERE id = 3;
```

---

## Delete: DELETE

Delete means removing data.

Example:

```sql id="v82sno"
DELETE FROM tasks
WHERE id = 3;
```

---

# Prepared Statements

A prepared statement is safer than building SQL by concatenating strings.

Prepared statements help prevent SQL injection and make SQL code cleaner.

Example:

```java id="ag2lzb"
String sql = "INSERT INTO tasks (title, completed) VALUES (?, ?)";

PreparedStatement stmt = conn.prepareStatement(sql);
stmt.setString(1, title);
stmt.setInt(2, 0);
stmt.executeUpdate();
```

The `?` placeholders are filled in using setter methods.

---

# Wiring DatabaseManager into the App

A JavaFX app can pass a `DatabaseManager` into scene construction.

The `SceneFactory` method signature may change from this:

```java id="c9q57h"
public static Scene create(SceneType type, Stage stage)
```

to something like this:

```java id="8g091g"
public static Scene create(SceneType type, Stage stage, DatabaseManager db)
```

This allows scenes to use the database without creating their own database connections.

---

# Updated SceneFactory Signature

Example:

```java id="xnqe03"
public static Scene create(SceneType type, Stage stage, DatabaseManager db) {
    return switch (type) {
        case MAIN -> buildMainScene(stage, db);
        case LOGIN -> buildLoginScene(stage, db);
        case DASHBOARD -> buildDashboardScene(stage, db);
    };
}
```

Each scene builder can receive the same `DatabaseManager`.

This helps keep the app organized.

---

# SQLite Best Practices

Important SQLite and database best practices:

* Keep database code out of UI code.
* Use a `DatabaseManager`.
* Use prepared statements.
* Create tables when the app starts.
* Close database resources when finished.
* Do not open unnecessary duplicate connections.
* Keep SQL organized and readable.
* Handle exceptions carefully.

---

# Observer Pattern Preview

After adding multiple scenes and a database, a new problem appears: components need to communicate with each other.

For example:

* One scene updates data.
* Another scene needs to refresh.
* A button changes state.
* A list needs to update after a database change.

This leads into the Observer Pattern.

The Observer Pattern is a behavioral design pattern about communication between objects.

The lecture previewed this as the next design pattern topic.

---

# Main Week 4 Takeaways

* Requirements analysis focuses on what the system should do, not how it should do it.
* Use cases describe how actors interact with a system.
* Actors can be people, systems, machines, or external devices.
* User stories describe user goals in a short format.
* User stories can be converted into GitHub issues.
* Good acceptance criteria help show when a story is complete.
* The Single Responsibility Principle says a class should have one reason to change.
* A messy `start()` method in JavaFX can become a God Method.
* The Factory Pattern moves object creation into a separate class.
* `SceneFactory` builds scenes so `Main.java` can stay clean.
* `SceneType` enums are safer than strings for choosing scenes.
* SQLite is a local, file-based database.
* JDBC lets Java connect to databases.
* `DatabaseManager` keeps database logic separate from UI logic.
* CRUD means Create, Read, Update, and Delete.
* Prepared statements are safer than string-concatenated SQL.
* The Observer Pattern helps solve communication problems between components.
