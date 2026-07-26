# Week 5 Notes

## Overview

Week 5 continued the JavaFX Todo App design pattern project. The main topics were the Singleton Pattern, tramp data, refactoring `DatabaseManager`, the Observer Pattern, `TodoRepository`, `TodoObserver`, `TodoItem`, JavaFX `ObservableList`, and layered architecture.

The main goal was to improve the design of the JavaFX app so each class has a clear responsibility and the UI can update automatically when data changes.

---

# Scene Factory Review

In the previous lesson, we used the Factory Pattern to move scene creation out of `Main.java`.

Instead of building every JavaFX scene directly inside the `start()` method, `Main.java` asks `SceneFactory` to create a scene.

Example:

```java
@Override
public void start(Stage stage) {
    stage.setTitle("Todo App");
    stage.setScene(SceneFactory.create(SceneType.MAIN, stage));
    stage.show();
}
```

This keeps `Main.java` focused on starting the app instead of building every button, label, layout, and event handler.

---

# Factory Pattern Review

The Factory Pattern is a creational design pattern.

A creational pattern focuses on how objects are made.

In the JavaFX app:

| Role    | Example        |
| ------- | -------------- |
| Client  | `Main.java`    |
| Factory | `SceneFactory` |
| Product | `Scene`        |

The client asks for a scene by type. The factory knows how to build the scene and returns it.

---

# SceneType Enum Review

A `SceneType` enum is used to identify which scene should be created.

Example:

```java
public enum SceneType {
    MAIN,
    DASHBOARD
}
```

Using an enum is better than using plain strings because:

* The compiler can catch invalid scene names.
* IntelliJ can autocomplete enum values.
* A switch expression can warn when a new scene type is not handled.
* Renaming is safer.

If we add a new enum value like this:

```java
public enum SceneType {
    MAIN,
    DASHBOARD,
    EDIT
}
```

then `SceneFactory` may show an error until the new `EDIT` case is handled. This is helpful because it reminds us to update the factory.

---

# SQLite Review

SQLite is a local database that stores the entire database in one file, such as:

```text
app.db
```

In Java, we use JDBC to connect to SQLite.

Example database URL:

```java
private static final String DB_URL = "jdbc:sqlite:app.db";
```

SQLite is useful for desktop apps because it does not require a separate database server.

---

# DatabaseManager Review

`DatabaseManager` is responsible for database work.

It handles things like:

* Opening the database connection
* Creating tables
* Inserting rows
* Reading rows
* Updating rows
* Deleting rows
* Closing the connection

This keeps database logic separate from JavaFX UI code.

---

# The Problem: Passing db Around

At first, the app created a `DatabaseManager` in `Main.java` and passed it through multiple method calls.

Example:

```java
db = new DatabaseManager();
stage.setScene(SceneFactory.create(SceneType.MAIN, stage, db));
```

Then `SceneFactory` also had to accept the database manager:

```java
public static Scene create(SceneType type, Stage stage, DatabaseManager db) {
    // code here
}
```

This works, but it can become messy as the app grows.

---

# Tramp Data

## What Is Tramp Data?

Tramp data is a code smell.

It happens when an object is passed through multiple layers that do not really use it, just so it can reach another deeper layer that does use it.

Example:

```text
Main.java passes db to SceneFactory
SceneFactory passes db to buildDashboardScene
buildDashboardScene finally uses db
```

The problem is that some methods receive `db` even if they do not actually need it.

This adds coupling without adding clarity.

---

## Why Tramp Data Is a Problem

Tramp data can make code harder to work with because:

* Method signatures get longer.
* Classes depend on things they do not really need.
* Adding new scenes may require changing method signatures.
* The code becomes more tightly coupled.
* It is harder to tell which class actually uses the object.

---

# Singleton Pattern

## What Is the Singleton Pattern?

The Singleton Pattern is a creational design pattern.

A Singleton is a class that:

1. Allows only one instance of itself to exist.
2. Provides a global access point to that one instance.

The common method name is:

```java
getInstance()
```

---

## When Singleton Is Appropriate

Singleton can be appropriate when there should be exactly one shared resource.

Examples:

* One database connection manager
* One configuration manager
* One logger

Singleton is usually not appropriate for regular domain objects.

Do not use Singleton for objects like:

* `TodoItem`
* `User`
* `Order`
* `Student`

Those objects should usually have many separate instances.

---

# DatabaseManager as a Singleton

`DatabaseManager` is a good candidate for Singleton because the app should only need one database manager.

The goal is to avoid writing this in many places:

```java
new DatabaseManager()
```

Instead, we use:

```java
DatabaseManager.getInstance()
```

---

## Refactored DatabaseManager

Example:

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DatabaseManager {

    private static final String DB_URL = "jdbc:sqlite:app.db";
    private static DatabaseManager instance;

    private Connection connection;

    private DatabaseManager() {
        try {
            connection = DriverManager.getConnection(DB_URL);
            createTables();
        } catch (SQLException e) {
            System.err.println("Connection failed: " + e.getMessage());
        }
    }

    public static DatabaseManager getInstance() {
        if (instance == null) {
            instance = new DatabaseManager();
        }

        return instance;
    }

    public void close() {
        try {
            if (connection != null && !connection.isClosed()) {
                connection.close();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }

        instance = null;
    }

    private void createTables() {
        // create database tables here
    }
}
```

---

# Two Key Singleton Changes

## 1. Private Constructor

The constructor becomes private:

```java
private DatabaseManager() {
    // setup code
}
```

This means outside classes cannot do this anymore:

```java
DatabaseManager db = new DatabaseManager();
```

The compiler rejects it because the constructor has private access.

---

## 2. Static getInstance Method

The class provides a static method:

```java
public static DatabaseManager getInstance() {
    if (instance == null) {
        instance = new DatabaseManager();
    }

    return instance;
}
```

The first time `getInstance()` is called, the object is created.

Every later call returns the same object.

---

# Lazy Initialization

Lazy initialization means the object is not created until it is first needed.

In this code:

```java
if (instance == null) {
    instance = new DatabaseManager();
}
```

the `DatabaseManager` is only created the first time `getInstance()` is called.

---

# Simplified Main.java with Singleton

Before Singleton, `Main.java` needed to store and pass around the database manager.

Before:

```java
private DatabaseManager db;

@Override
public void start(Stage stage) {
    db = new DatabaseManager();
    stage.setScene(SceneFactory.create(SceneType.MAIN, stage, db));
    stage.show();
}

@Override
public void stop() {
    if (db != null) {
        db.close();
    }
}
```

After Singleton:

```java
@Override
public void start(Stage stage) {
    stage.setTitle("Todo App");
    stage.setScene(SceneFactory.create(SceneType.MAIN, stage));
    stage.show();
}

@Override
public void stop() {
    DatabaseManager.getInstance().close();
}
```

Now `Main.java` no longer creates the database manager directly.

---

# Simplified SceneFactory with Singleton

Before Singleton:

```java
public static Scene create(SceneType type, Stage stage, DatabaseManager db) {
    return switch (type) {
        case MAIN -> buildMainScene(stage, db);
        case DASHBOARD -> buildDashboardScene(stage, db);
    };
}
```

After Singleton:

```java
public static Scene create(SceneType type, Stage stage) {
    return switch (type) {
        case MAIN -> buildMainScene(stage);
        case DASHBOARD -> buildDashboardScene(stage);
    };
}
```

A scene builder can get the database manager only when it actually needs it:

```java
private static Scene buildDashboardScene(Stage stage) {
    DatabaseManager db = DatabaseManager.getInstance();

    // build dashboard scene here
}
```

This keeps method signatures cleaner.

---

# Singleton Benefits and Trade-Offs

| Benefit                                    | Trade-Off                     |
| ------------------------------------------ | ----------------------------- |
| Guarantees one instance                    | Creates global state          |
| Removes tramp data                         | Can make testing harder       |
| Easy to access from different parts of app | Can hide dependencies         |
| Lazy initialization                        | Not automatically thread-safe |

For this JavaFX app, thread safety is less of a concern because the app is mainly running on the JavaFX application thread.

---

# Design Principle: DRY

DRY stands for:

```text
Don't Repeat Yourself
```

Using a Singleton for `DatabaseManager` gives the app one source of truth for the database connection.

There is one place to open the connection and one place to close it.

---

# TodoRepository

## Why Add TodoRepository?

After `DatabaseManager` becomes a Singleton, the next design improvement is adding a `TodoRepository`.

`TodoRepository` sits between the UI and the database.

Instead of scenes directly calling database methods, scenes call repository methods.

Example:

```java
repo.add("Buy milk");
```

Then the repository handles the database update.

---

## TodoRepository Before and After Singleton

Before Singleton:

```java
public class TodoRepository {

    private final DatabaseManager db;

    public TodoRepository(DatabaseManager db) {
        this.db = db;
    }
}
```

After Singleton:

```java
public class TodoRepository {

    private final DatabaseManager db = DatabaseManager.getInstance();
}
```

Now `TodoRepository` can get the single database manager itself.

---

# The UI Coupling Problem

Once the app has a database and multiple UI components, another problem appears.

Example:

```java
Label countLabel = new Label("Items: " + db.getAllItems().size());

addBtn.setOnAction(e -> {
    db.insertItem(nameField.getText());
    list.getItems().setAll(db.getAllItems());
    // forgot to refresh countLabel
});
```

The list updates, but the label still shows the old count.

This becomes worse as the app grows.

If five UI components display todo data, every event handler would need to remember to refresh all five components.

That creates tight coupling.

---

# Tight Coupling

Tight coupling means parts of the code depend too directly on each other.

Example:

```text
addBtn handler knows about:
- database
- list view
- count label
- status bar
- header badge
```

This is fragile because changing one thing requires changing many other things.

A better design would be:

```text
addBtn handler calls repo.add(item)

Repository updates data

Repository notifies all observers automatically
```

The event handler should not need to know who cares about the data change.

---

# Observer Pattern

## What Is the Observer Pattern?

The Observer Pattern is a behavioral design pattern.

A behavioral pattern focuses on how objects communicate.

The Observer Pattern defines a one-to-many dependency between objects.

When one object changes state, all of its dependents are notified and updated automatically.

---

# Observer Pattern Participants

| Role              | What It Does                            | In the Todo App            |
| ----------------- | --------------------------------------- | -------------------------- |
| Subject           | Holds state and maintains observer list | `TodoRepository`           |
| Observer          | Interface that receives notifications   | `TodoObserver`             |
| Concrete Observer | Reacts to notifications                 | Dashboard scene components |
| Client            | Registers observers                     | `SceneFactory` or `Main`   |

---

# Observer Pattern Core Idea

Instead of this:

```text
Button handler manually refreshes every UI component.
```

we want this:

```text
Button handler changes the data.
Repository announces the data changed.
Observers update themselves.
```

The button handler does not need to know about every label, list, or counter.

---

# TodoObserver Interface

`TodoObserver` is the observer interface.

Example:

```java
import java.util.List;

/**
 * Any component that wants to react to changes in the todo list
 * must implement this interface.
 */
public interface TodoObserver {

    /**
     * Called by the Subject whenever the todo list changes.
     *
     * @param todos the current list of todo items
     */
    void onTodosChanged(List<TodoItem> todos);
}
```

Any class or component that wants todo updates can implement this interface.

---

# TodoItem Model

`TodoItem` represents one row in the `todos` table.

Example:

```java
public class TodoItem {

    private final int id;
    private final String title;
    private boolean done;

    public TodoItem(int id, String title, boolean done) {
        this.id = id;
        this.title = title;
        this.done = done;
    }

    public int getId() {
        return id;
    }

    public String getTitle() {
        return title;
    }

    public boolean isDone() {
        return done;
    }

    @Override
    public String toString() {
        return (done ? "✓ " : "○ ") + title;
    }
}
```

---

## Separation of Concerns in TodoItem

`TodoItem` is a plain model object.

It should not know about:

* JavaFX scenes
* Buttons
* Labels
* SQLite
* JDBC
* Observer registration

It only represents todo item data.

This makes it easier to test and safer to change.

---

# TodoRepository as the Subject

`TodoRepository` acts as the Subject in the Observer Pattern.

It stores a list of observers.

Example:

```java
import java.util.ArrayList;
import java.util.List;

public class TodoRepository {

    private final DatabaseManager db = DatabaseManager.getInstance();
    private final List<TodoObserver> observers = new ArrayList<>();

    public void addObserver(TodoObserver observer) {
        observers.add(observer);
    }

    public void removeObserver(TodoObserver observer) {
        observers.remove(observer);
    }

    private void notifyObservers() {
        List<TodoItem> current = getAll();

        for (TodoObserver observer : observers) {
            observer.onTodosChanged(current);
        }
    }

    public List<TodoItem> getAll() {
        return db.getAllTodos();
    }
}
```

The repository does not need to know what kind of object each observer is.

It only knows that each observer has an `onTodosChanged()` method.

---

# Write Operations Notify Observers

Every method that changes data should call `notifyObservers()`.

Example:

```java
public void add(String title) {
    db.insertTodo(title);
    notifyObservers();
}

public void markDone(int id) {
    db.markDone(id);
    notifyObservers();
}

public void delete(int id) {
    db.deleteTodo(id);
    notifyObservers();
}
```

Pattern rule:

```text
Every mutating method ends with notifyObservers().
```

Read methods do not need to notify observers because they do not change data.

---

# Registering an Observer

In `SceneFactory`, after building the dashboard scene, we can register an observer.

Example:

```java
repo.addObserver(todos -> {
    listView.getItems().setAll(todos);
    count.setText("Active: " + todos.stream()
        .filter(todo -> !todo.isDone())
        .count());
});
```

This observer updates the `ListView` and count label whenever the repository changes.

---

# Dashboard Scene Layout

Example controls:

```java
ListView<TodoItem> listView = new ListView<>();
TextField titleField = new TextField();

titleField.setPromptText("New todo...");

Button addBtn = new Button("Add");
Button doneBtn = new Button("Mark Done");
Label count = new Label();
```

Example layout:

```java
HBox inputRow = new HBox(8, titleField, addBtn);
HBox actionRow = new HBox(8, doneBtn, count);

VBox root = new VBox(12,
    new Label("My Todos"),
    listView,
    inputRow,
    actionRow
);
```

---

# Dashboard Scene Event Handlers

The event handlers call repository methods instead of manually updating the UI.

Example add button:

```java
addBtn.setOnAction(e -> {
    String text = titleField.getText().trim();

    if (!text.isEmpty()) {
        repo.add(text);
        titleField.clear();
    }
});
```

Example mark done button:

```java
doneBtn.setOnAction(e -> {
    TodoItem selected = listView.getSelectionModel().getSelectedItem();

    if (selected != null) {
        repo.markDone(selected.getId());
    }
});
```

The handlers do not directly refresh the list or count label.

The repository notifies the observers, and the observers update the UI.

---

# Full Add Button Call Chain

When the user clicks **Add**, this is the flow:

```text
addBtn handler
    |
    v
repo.add("Buy milk")
    |
    v
db.insertTodo("Buy milk")
    |
    v
notifyObservers()
    |
    v
observer.onTodosChanged(freshList)
    |
    v
listView and count label update
```

The event handler only makes one call:

```java
repo.add(text);
```

Everything else happens through the repository and observers.

---

# Updated Main.java with TodoRepository

Example:

```java
public class Main extends Application {

    private final TodoRepository repo = new TodoRepository();

    @Override
    public void start(Stage stage) {
        stage.setTitle("Todo App");
        stage.setScene(SceneFactory.create(SceneType.DASHBOARD, stage, repo));
        stage.show();
    }

    @Override
    public void stop() {
        DatabaseManager.getInstance().close();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

`Main.java` creates the repository and passes it to the factory.

It does not know about scenes, layouts, observers, or database details.

---

# Updated SceneFactory with TodoRepository

Example:

```java
public class SceneFactory {

    public static Scene create(SceneType type, Stage stage, TodoRepository repo) {
        return switch (type) {
            case MAIN -> buildMainScene(stage, repo);
            case DASHBOARD -> buildDashboardScene(stage, repo);
        };
    }
}
```

The scenes interact with the repository, not the raw database manager.

---

# Layered Architecture

The app now has layers:

```text
Main
  ↓
SceneFactory
  ↓
Scenes
  ↓
TodoRepository
  ↓
DatabaseManager
  ↓
SQLite
```

Each layer knows only about the layer directly below it.

This makes the app easier to change.

---

# Why Layered Architecture Helps

Layered architecture helps because each part has one main job.

| Layer             | Main Job                                     |
| ----------------- | -------------------------------------------- |
| `Main`            | Start and stop the app                       |
| `SceneFactory`    | Build scenes                                 |
| Scenes            | Display UI and handle user events            |
| `TodoRepository`  | Provide todo operations and notify observers |
| `DatabaseManager` | Talk to SQLite                               |
| SQLite            | Store the data                               |

---

# JavaFX Has Observer Built In

JavaFX already uses observer-style behavior.

Example:

```java
button.setOnAction(e -> {
    // code here
});
```

The button is like the Subject.

The lambda is like the Observer.

When the button is clicked, JavaFX notifies the event handler.

---

# ObservableList

JavaFX has a built-in reactive list called `ObservableList`.

A `ListView` can watch an `ObservableList`.

Example:

```java
ObservableList<TodoItem> observableItems =
    FXCollections.observableArrayList(repo.getAll());

listView.setItems(observableItems);
```

Then when the observable list changes, the `ListView` can refresh automatically.

---

# ObservableList with Repository Observer

Example:

```java
repo.addObserver(todos -> {
    observableItems.setAll(todos);
});
```

Now the repository updates the observable list, and the `ListView` observes the list.

This combines the custom Observer Pattern with JavaFX’s built-in observable tools.

---

# When to Use Custom Observer vs ObservableList

| Situation                                     | Good Choice              |
| --------------------------------------------- | ------------------------ |
| Simple JavaFX list display                    | `ObservableList`         |
| Multiple different UI components need updates | Custom `TodoObserver`    |
| Non-JavaFX code or tests                      | Custom Observer          |
| Form fields tied to model values              | JavaFX property bindings |

---

# Pattern Family Check-In

Week 5 used multiple design patterns together.

| Pattern   | Family     | Purpose                               |
| --------- | ---------- | ------------------------------------- |
| Factory   | Creational | Creates scenes                        |
| Singleton | Creational | Ensures one database manager          |
| Observer  | Behavioral | Notifies components when data changes |

Good design often uses multiple patterns together.

No single pattern solves every problem.

---

# Main Week 5 Takeaways

* Tramp data is a code smell where an object gets passed through methods that do not really use it.
* Singleton is a creational pattern that allows exactly one instance of a class.
* `DatabaseManager` can be refactored as a Singleton.
* A private constructor prevents outside classes from calling `new DatabaseManager()`.
* `getInstance()` returns the one shared instance.
* Lazy initialization creates the object only when it is first needed.
* Singleton can remove tramp data, but it can make testing harder.
* The Observer Pattern is a behavioral pattern.
* Observer helps solve tight coupling between data changes and UI updates.
* `TodoRepository` acts as the Subject.
* `TodoObserver` is the Observer interface.
* `TodoItem` is a plain model object.
* Every write operation in the repository should call `notifyObservers()`.
* JavaFX uses observer ideas with event handlers and `ObservableList`.
* The app uses layered architecture: `Main → SceneFactory → Scenes → TodoRepository → DatabaseManager → SQLite`.
* Factory, Singleton, and Observer can work together in one design.
