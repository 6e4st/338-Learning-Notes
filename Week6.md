# Week 6 Notes

## Overview

Week 6 focused on project teamwork, Git workflow, GitHub issues, code review, database design, inner classes, threads, and REST APIs.

The main ideas were:

* How to use Git more effectively
* How to organize work with branches and GitHub issues
* How to write better user stories
* How to review code through pull requests
* How ERDs show database relationships
* How primary keys and foreign keys connect tables
* How inner classes work in Java
* Why background threads are needed
* What REST APIs are and how apps consume them

---

# Git

## What Is Git?

Git is a version control system.

A version control system tracks changes made to files in a folder.

Git is especially good for tracking text files, such as:

* Java files
* Markdown files
* Gradle files
* HTML/CSS files
* Plain text files

Git does not work as well with binary files, such as:

* Images
* Executables
* Word documents

This is because binary files are harder for Git to compare line by line.

---

## What `git init` Does

The command:

```bash id="1ic6m8"
git init
```

creates an empty Git repository in the current directory.

It creates a hidden folder named:

```text id="n30kpt"
.git
```

The `.git` folder contains metadata about the repository.

This includes information like:

* Config files
* Commit history
* Branch information
* Remote information
* Internal Git objects

---

# Git Configuration

Git has different levels of configuration.

## Local Config

Local config applies only to the current repository.

Example:

```bash id="az3i3g"
git config user.name "dclinkenbeard"
```

## Global Config

Global config applies to all repositories for the current user.

Example:

```bash id="qqo11f"
git config --global user.name "dclinkenbeard"
```

## Config Levels

Git configuration can happen at these levels:

| Level  | Meaning                            |
| ------ | ---------------------------------- |
| System | Applies to all users on the system |
| Global | Applies to the current user        |
| Local  | Applies to the current repository  |

Local settings can override global settings.

---

## Useful Git Config Options

Useful options include:

```bash id="eey0nt"
git config user.name "your username"
git config user.email "your email"
git config core.editor "your editor"
```

The `core.editor` setting controls which editor opens when Git needs you to type a commit message or edit something like an interactive rebase.

---

# Common Git Commands

## `git status`

Shows tracked and untracked files.

```bash id="3xk7a3"
git status
```

## `git add .`

Adds changed and untracked files to the staging area.

```bash id="uxkbt1"
git add .
```

## `git commit`

Records staged changes into the repository history.

```bash id="mqpc95"
git commit
```

## `git push`

Sends commits to the remote repository.

```bash id="z7m7s7"
git push
```

## `git pull`

Pulls changes from the remote repository.

```bash id="p854gf"
git pull
```

---

# Remotes

A remote is a version of the repository stored somewhere else, usually on GitHub.

Example:

```bash id="akevby"
git remote add origin <url>
```

To view remotes:

```bash id="zalxik"
git remote -v
```

The remote named `origin` usually points to the GitHub repository.

---

# Cloning a Repository

To copy an existing GitHub repository to your local computer, use:

```bash id="kqfw4y"
git clone <url>
```

This downloads the repository and sets up the remote automatically.

---

# Branching

A branch is a separate line of development.

Branches let developers work on features or fixes without changing `main` directly.

## Create a Branch

```bash id="rnbzji"
git branch landingPage
```

## Switch to a Branch

```bash id="7qfx17"
git checkout landingPage
```

## Create and Switch in One Command

```bash id="lsnmlp"
git checkout -b landingPage
```

## List Branches

```bash id="tslskp"
git branch
```

---

# Branch Naming

Good branch names help teams understand what work is happening.

Common branch prefixes:

| Prefix      | Meaning                       |
| ----------- | ----------------------------- |
| `feature/`  | New feature                   |
| `bugfix/`   | Bug fix                       |
| `hotfix/`   | Urgent production fix         |
| `release/`  | Release preparation           |
| `refactor/` | Code cleanup or restructuring |

Examples:

```text id="hokabn"
feature/user-auth
bugfix/login-error
refactor/cleanup-api
```

Good branch naming tips:

* Use lowercase.
* Use hyphens instead of spaces.
* Keep names short but clear.
* Be consistent as a team.

---

# Merge vs Rebase

## Merge

Merge preserves history.

Use merge for shared branches.

Example:

```bash id="qkbzv6"
git merge main
```

Merge creates a merge commit when combining branches.

This helps preserve who did what and when.

---

## Rebase

Rebase rewrites history.

Use rebase mainly for private branches before pushing them to a shared repository.

Example:

```bash id="sv9z0b"
git rebase -i HEAD~3
```

This starts an interactive rebase for the last three commits.

Interactive rebase can be used to:

* Reword commit messages
* Squash commits together
* Drop commits
* Edit commits
* Clean up messy commit history

Important warning:

Do not rebase commits that have already been pushed to a shared branch unless your team knows exactly what is happening.

---

# Interactive Rebase Commands

Common interactive rebase commands:

| Command  | Meaning                                               |
| -------- | ----------------------------------------------------- |
| `pick`   | Keep the commit                                       |
| `reword` | Keep the commit but change the message                |
| `edit`   | Stop and allow changes                                |
| `squash` | Combine with previous commit and keep messages        |
| `fixup`  | Combine with previous commit and discard this message |
| `drop`   | Remove the commit                                     |

---

# Merge Conflicts

A merge conflict happens when Git cannot automatically combine changes.

This often happens when two branches edit the same line or same area of a file.

Basic conflict workflow:

1. Merge or pull changes.
2. Git reports a conflict.
3. Open the conflicted file.
4. Choose which code to keep.
5. Remove conflict markers.
6. Add the resolved file.
7. Commit the resolution.

Merge conflicts are normal in team projects.

---

# GitHub Issues

## What Is a GitHub Issue?

A GitHub issue is like a ticket.

It can represent:

* A bug
* A feature
* A task
* A user story
* A piece of project planning

Issues help a team break a larger project into smaller pieces.

---

# User Stories and Issues

A user story describes what a user wants to do.

A common format is:

```text id="emtp87"
As a [user], I want to [do something], so that [reason].
```

GitHub issues can break user stories into smaller developer tasks.

Example user story:

```text id="akpyfo"
As a user, I want to log in so that I can access my saved data.
```

Possible issues:

* Create username field
* Create password field
* Add login button
* Validate username and password
* Show error message for failed login
* Store user login state

---

# INVEST Criteria

Good user stories or issues should follow INVEST.

INVEST stands for:

| Letter | Meaning     |
| ------ | ----------- |
| I      | Independent |
| N      | Negotiable  |
| V      | Valuable    |
| E      | Estimable   |
| S      | Small       |
| T      | Testable    |

---

## Independent

An issue should be as self-contained as possible.

It should not depend too heavily on many other tasks.

Example:

```text id="t049ry"
Create username and password input fields.
```

This is more independent than:

```text id="db1q3b"
Build the entire user account system.
```

---

## Negotiable

The details should not be completely locked in too early.

The team should be able to discuss how the issue will be implemented.

Example:

```text id="zkyptz"
Should login use our own username/password database, or an external authentication system?
```

---

## Valuable

The issue should provide value to the app or user.

A login screen is valuable if the app needs user accounts.

A random feature that does not support the app’s goals may not be valuable.

---

## Estimable

The team should be able to estimate how long the issue might take.

If an issue is too vague, it is hard to estimate.

Too vague:

```text id="97ozmz"
Use machine learning to predict user behavior.
```

More estimable:

```text id="txwuzv"
Create a screen that displays the user's saved workouts.
```

---

## Small

An issue should be small enough to finish in one iteration or sprint.

For this class, an iteration is about one week.

If an issue feels too large, split it into smaller issues.

---

## Testable

The team should be able to prove whether the issue is done.

Example acceptance criteria:

```markdown id="rhpv9m"
- User can enter a username.
- User can enter a password.
- User sees an error message if login fails.
- User reaches the dashboard if login succeeds.
```

---

# Estimating Issues

When estimating an issue, ask whether it is:

* Very easy
* Easy
* Average
* Challenging
* Very challenging

If something is very challenging, it may need to be split into smaller issues.

---

# Splitting, Merging, and Spiking Issues

## Splitting

Splitting means breaking a large issue into smaller issues.

Example large issue:

```text id="k2tcdg"
Create login system.
```

Smaller issues:

```text id="ax6l9k"
Create login screen.
Validate username and password.
Show login error.
Save logged-in state.
```

## Merging

Merging means combining issues that are too small or too closely related.

Example:

```text id="xi3put"
Create repository.
Add teammates.
Set up README.
```

These might be combined into one setup issue.

## Spiking

A spike is a research task.

Use a spike when the team does not yet know how to estimate or implement something.

Example:

```text id="uv9y6i"
Research which API library we should use.
```

---

# Code Review

## What Is Code Review?

Code review is a systematic examination of source code by peers.

The goals are to:

* Catch bugs before production
* Improve code quality
* Improve maintainability
* Share knowledge
* Ensure consistency
* Encourage collaboration

---

# Why Code Review Matters

Code review has technical and team benefits.

Technical benefits:

* Catches bugs early
* Improves architecture
* Ensures test coverage
* Maintains consistency

Team benefits:

* Knowledge sharing
* Mentorship
* Collective code ownership
* Better collaboration

---

# Code Review Mindset

## For Reviewers

The reviewer is a collaborator, not a critic.

The goal is to improve the code, not prove that the reviewer is smarter.

Good reviewers:

* Ask questions
* Give specific feedback
* Explain concerns clearly
* Point out good solutions
* Focus on improvement

## For Authors

Feedback is about the code, not the person.

Good authors:

* Stay humble
* Assume good intentions
* Respond professionally
* Learn from the review
* Avoid taking feedback personally

---

# What to Look For in Code Review

## Design and Architecture

Ask:

* Is the code well designed?
* Does it follow SOLID principles?
* Is separation of concerns clear?
* Are components decoupled?
* Does it fit the existing architecture?

## Functionality

Ask:

* Does the code work as intended?
* Are edge cases handled?
* Is error handling present?
* Are security concerns addressed?

## Testing

Ask:

* Are unit tests included?
* Are tests meaningful?
* Do tests pass?
* Is coverage adequate?

Important rule:

```text id="296tb9"
If it does not run or tests fail without explanation, do not approve.
```

---

# Code Quality

When reviewing code quality, check:

* Complexity
* Naming
* Comments
* Documentation

Good questions:

* Could this be simpler?
* Can another teammate understand it?
* Are names clear?
* Do comments explain why, not just what?
* Was the README or documentation updated if needed?

---

# What Not to Focus On

Do not spend too much time on:

* Whitespace
* Formatting
* Personal style preferences
* Tiny nitpicks
* Rewriting the author’s code in your preferred style

Use the team style guide instead of personal preference.

Let the IDE handle formatting.

---

# Good Review Comments

Bad comments:

```text id="rk2xqp"
This is wrong.
Don't do it this way.
```

Better comments:

```text id="b2vrlq"
What is the purpose of this function?
Consider extracting this logic into a helper method for reuse.
```

Good review comments are specific, constructive, and actionable.

---

# Pull Request Best Practices

Before submitting a pull request, the author should make sure:

* Code runs without errors.
* Tests pass.
* New features have tests.
* The PR description is clear.
* The PR is focused and not too large.
* Known issues are explained.

A good PR description should include:

* What changed
* Why it changed
* How to test it
* Known issues or limitations

---

# Three Key Code Review Questions

During code review, keep asking:

1. Do I understand what this code does?
2. Does it function as I expect it to?
3. Does this fulfill the requirements?

---

# Code Review Limits

Code reviews should stay manageable.

Recommended limits:

* About 60 minutes maximum
* About 400 lines of code

Large changes should be split into smaller pull requests when possible.

---

# When to Approve

Approve a pull request if:

* The code works correctly.
* Tests pass.
* It improves the codebase.
* It follows team standards.
* There are no major issues.

---

# When to Request Changes

Request changes if:

* The code does not run.
* Tests fail without explanation.
* There are security problems.
* It breaks existing functionality.
* Critical tests are missing.

The goal is improvement, not perfection.

---

# Team Pull Request Expectations

For team projects:

* All code changes should go through pull requests.
* Pull requests should require approvals.
* Branch names should follow team conventions.
* PR descriptions should be meaningful.
* Review comments should be constructive.
* Tests should pass before approval.
* Team members should not review their own PRs.

---

# ERDs

## What Is an ERD?

ERD stands for Entity Relationship Diagram.

An ERD shows database tables and how they relate to each other.

ERDs are useful for planning database structure before writing code.

---

# Primary Keys

A primary key uniquely identifies a record in a table.

In general, every table should have a primary key.

Example:

```text id="7hc2kh"
User
- userId primary key
- username
- password
```

The `userId` can uniquely identify one user.

---

# Foreign Keys

A foreign key is a reference to a primary key in another table.

Foreign keys connect tables.

Example:

```text id="b7xvt9"
Log
- logId primary key
- userId foreign key
- date
- notes
```

Here, `userId` in the `Log` table points to `userId` in the `User` table.

This lets the app find all logs that belong to a specific user.

---

# ERD Example: User and Log

Example relationship:

```text id="m6hdai"
User
- userId primary key
- username

Log
- logId primary key
- userId foreign key
- workoutInfo
```

Meaning:

* One user can have many logs.
* Each log belongs to one user.
* The foreign key connects the log to the user.

---

# Relation Tables

A relation table can connect multiple tables, especially when there are many-to-many relationships.

Example:

```text id="j6g4ka"
Student
Course
Class
```

A student can take many courses.

A course can have many students.

A relation table can store IDs that connect them.

---

# SQL Query Example

Example query:

```sql id="g9nzvq"
SELECT *
FROM Class
WHERE ClassID = :cID;
```

This selects records from the `Class` table where the class ID matches a specific value.

---

# Android Room Example

In Android Room, an entity can declare a foreign key.

Example idea:

```java id="06tyid"
@Entity(
    tableName = "pets",
    foreignKeys = @ForeignKey(
        entity = User.class,
        parentColumns = "userId",
        childColumns = "ownerId",
        onDelete = ForeignKey.CASCADE
    )
)
public class Pet {
    @PrimaryKey(autoGenerate = true)
    public long petId;

    public String petName;

    public long ownerId;
}
```

Here, `ownerId` references the `userId` from the `User` table.

---

# Android Database Tests

Database tests can use an in-memory database.

An in-memory database is useful for testing because it does not permanently save test data.

Example test setup:

```java id="fwi9j8"
@Before
public void createDb() {
    Context context = ApplicationProvider.getApplicationContext();
    db = Room.inMemoryDatabaseBuilder(context, GymLogDatabase.class).build();
    userDao = db.userDAO();
}
```

Example cleanup:

```java id="7xnve5"
@After
public void closeDb() throws IOException {
    db.close();
}
```

Example test:

```java id="4iar95"
@Test
public void writeUserAndReadInList() {
    String username = "testuser1";
    String password = "password";
    User user = new User(username, password);

    userDao.insert(user);

    List<User> users = userDao.getAllUsersList();

    assertNotNull(users.get(0));
    assertEquals(username, users.get(0).getUsername());
}
```

This test writes a user, reads the users back, and checks that the saved username matches.

---

# Inner Classes

## What Is an Inner Class?

An inner class is a class defined inside another class.

Example:

```java id="9s0vpr"
public class Outer {

    public void showInner() {
        Inner inner = new Inner();
        inner.print();
    }

    private class Inner {
        public void print() {
            System.out.println("this is an inner class");
        }
    }
}
```

Normally, Java classes are placed in their own files. An inner class is different because it lives inside another class.

---

# Types of Inner Classes

There are three main kinds:

* Non-static inner classes
* Static inner classes
* Anonymous inner classes

---

# Why Use Inner Classes?

Inner classes can help with:

* Encapsulation
* Security
* Organization
* Hiding implementation details
* Keeping related code close together

They are useful when one class only makes sense inside another class.

---

# Inner Class Access

An inner class can access private fields and methods of the outer class.

The outer class can also use the inner class.

Example idea:

```java id="9aa9y3"
public class Hobbit {
    private boolean isVisible = true;
    private int evilness = 0;
    private OneRing precious;

    public void wearRing() {
        precious.turnInvisible();
    }

    private class OneRing {
        void turnInvisible() {
            isVisible = false;
            evilness++;
        }
    }
}
```

Even though `isVisible` and `evilness` are private, the inner class can access them.

---

# Actual Use: Iterator

An `ArrayList` can return an iterator.

The iterator needs to know about the internal state of the `ArrayList`.

Using an inner class for the iterator helps because:

* `ArrayList` can create iterator instances.
* `ArrayList` can call iterator methods.
* The iterator can access private members of `ArrayList`.
* The iterator can implement an interface while hiding implementation details.

---

# Static Inner Classes

A static inner class is like an inner class, but it is static.

Example:

```java id="426tbk"
public class Outer {

    public static class StaticInner {

        static int addition(int x, int y) {
            return x + y;
        }
    }
}
```

You can call it like:

```java id="3bleao"
System.out.println(Outer.StaticInner.addition(4, 10));
```

---

# Anonymous Inner Classes

An anonymous inner class is a class without a name.

It is often used when you need a quick implementation of an abstract class or interface.

Example:

```java id="rqmrpv"
AbstractOuter anon = new AbstractOuter() {
    @Override
    public void myMethod() {
        System.out.println("well this is weird.");
    }
};

anon.myMethod();
```

This creates an object that extends `AbstractOuter` and provides the method implementation immediately.

---

# Why Anonymous Inner Classes Are Useful

Anonymous inner classes let you:

* Implement code exactly where you need it.
* Keep related code close together.
* Fulfill a required contract.
* Provide a method implementation without creating a separate named class.

This should look familiar from event handlers.

---

# Event Handler Connection

Anonymous inner classes are related to how event handlers work.

Example idea:

```java id="qz1l5h"
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        // code that runs when clicked
    }
});
```

The code defines what happens when the element is clicked while still fulfilling the `OnClickListener` contract.

---

# Javadoc

Javadoc comments are special comments that can generate HTML documentation.

Example:

```java id="rv1oqt"
/**
 * A Hobbit class used to show off inner classes.
 *
 * @author Drew A. Clinkenbeard
 * @version 0.1
 * @since 2019-11-30
 */
public class Hobbit {
    // code here
}
```

Javadocs are useful for explaining classes, methods, parameters, and return values.

---

# Threads

## What Is a Thread?

A thread is the smallest unit of work managed by the operating system scheduler.

In a single CPU system, the CPU is shared among multiple threads using time slicing.

In a multi-CPU system, multiple threads can run concurrently.

---

# Why Use Background Threads?

Long-running tasks should happen on a background thread.

Examples:

* Database queries
* Network requests
* Accessing a remote server
* Downloading data
* Processing large data

If these tasks happen on the UI thread, the app can appear to freeze.

---

# Java Threads

A background task can be defined using the `Runnable` interface.

A `Runnable` must have a `run()` method.

Example:

```java id="dgh8h9"
public class MyThread implements Runnable {

    @Override
    public void run() {
        // code for background task goes here
    }
}
```

To run it:

```java id="kb36fm"
Thread thread = new Thread(new MyThread());
thread.start();
```

Important:

```text id="h0216j"
start() returns immediately.
It does not wait for the background task to finish.
```

---

# UI Thread and Background Thread

Background tasks should not directly update UI components.

Two threads accessing the same UI object at the same time can cause problems.

For example:

* UI thread updates a button.
* Background thread updates the same button.
* The timing overlaps.
* The app behaves unpredictably.

---

# Android Handler

Android uses a `Handler` object to schedule work on the UI thread.

The handler can post a `Runnable` to the UI thread’s message queue.

The UI thread then processes that work safely.

Basic idea:

```text id="m3gsx1"
Background thread does long task.
Background thread posts result to Handler.
Handler schedules UI update.
UI thread updates screen.
```

---

# Looper

A Looper takes messages from a queue and has the UI thread process them.

This is how Android can handle events like:

* Button clicks
* Focus changes
* Timer events
* Posted Runnable tasks

---

# REST APIs

## What Is a REST API?

REST stands for Representational State Transfer.

A REST API is a way for applications to communicate over a network.

Think of it like a waiter:

```text id="cin1kp"
Client makes request.
Server processes request.
Server sends response.
```

---

# REST API Characteristics

REST APIs commonly follow these ideas:

* Stateless
* Client-server separation
* Cacheable responses
* Uniform interface

## Stateless

Each request contains the information needed to process it.

The server should not need to remember hidden state from a previous request.

## Client-Server

The client and server have separate responsibilities.

The client handles the user interface.

The server handles data and business logic.

---

# HTTP Methods and CRUD

REST APIs often map HTTP methods to CRUD operations.

| HTTP Method | CRUD Operation | Purpose                        |
| ----------- | -------------- | ------------------------------ |
| GET         | Read           | Retrieve data                  |
| POST        | Create         | Create new data                |
| PUT         | Update         | Replace existing data          |
| PATCH       | Update         | Partially update existing data |
| DELETE      | Delete         | Remove data                    |

Most common methods in typical applications are `GET` and `POST`.

---

# REST API URLs

APIs use URLs called endpoints.

Example:

```text id="madw2r"
https://api.example.com/v1/users
```

Parts:

| Part                      | Meaning             |
| ------------------------- | ------------------- |
| `https://api.example.com` | Base URL            |
| `/v1`                     | API version         |
| `/users`                  | Resource collection |

Common patterns:

```text id="45f4uu"
GET /users
GET /users/123
GET /users/123/posts
POST /users
PUT /users/123
DELETE /users/123
```

---

# API Request and Response

A request may include:

* HTTP method
* URL
* Headers
* Body

Example request:

```http id="ngv76e"
GET /api/users/123 HTTP/1.1
Host: api.example.com
Authorization: Bearer abc123
Content-Type: application/json
Accept: application/json
```

A response includes:

* Status code
* Headers
* Body

Example response:

```http id="bwskpd"
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "name": "John Doe",
  "email": "john@example.com"
}
```

---

# HTTP Status Codes

HTTP status codes describe what happened.

## 2xx Success

Examples:

```text id="pid6zr"
200 OK
201 Created
204 No Content
```

## 3xx Redirect

Examples:

```text id="5eia8q"
301 Moved
302 Found
304 Not Modified
```

## 4xx Client Error

Examples:

```text id="oayiq9"
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
```

## 5xx Server Error

Examples:

```text id="uea5pr"
500 Internal Server Error
502 Bad Gateway
503 Unavailable
```

---

# Consuming APIs with Kotlin

The REST API slides showed Kotlin examples using Retrofit.

## Dependencies

Example Gradle dependencies:

```kotlin id="xd7wpu"
dependencies {
    implementation("com.squareup.retrofit2:retrofit:2.9.0")
    implementation("com.squareup.retrofit2:converter-gson:2.9.0")
    implementation("com.squareup.okhttp3:logging-interceptor:4.11.0")
}
```

---

## Data Class

Example:

```kotlin id="tcr44l"
data class User(
    val id: Int,
    val name: String,
    val email: String,
    val created: String
)
```

---

## API Interface

Example:

```kotlin id="gkjyph"
interface ApiService {

    @GET("users")
    suspend fun getUsers(): List<User>

    @GET("users/{id}")
    suspend fun getUser(@Path("id") id: Int): User

    @POST("users")
    suspend fun createUser(@Body user: User): User

    @DELETE("users/{id}")
    suspend fun deleteUser(@Path("id") id: Int): Response<Unit>
}
```

The annotations describe the HTTP method and endpoint.

---

## Retrofit Client

Example:

```kotlin id="sqvejq"
object RetrofitClient {

    private const val BASE_URL = "https://api.example.com/v1/"

    val api: ApiService = Retrofit.Builder()
        .baseUrl(BASE_URL)
        .addConverterFactory(GsonConverterFactory.create())
        .build()
        .create(ApiService::class.java)
}
```

---

# API Best Practices

Important REST API best practices:

## Error Handling

* Use try/catch blocks.
* Check HTTP status codes.
* Handle network timeouts.
* Show meaningful error messages.

## Authentication

* Use auth headers.
* Store tokens securely.
* Refresh tokens before expiration.
* Handle `401 Unauthorized`.

## Performance

* Use async operations.
* Cache when appropriate.
* Paginate large data sets.
* Request only needed fields.

## Testing

* Test different response codes.
* Test network failures.
* Test JSON parsing edge cases.
* Use mock servers when possible.

---

# Main Week 6 Takeaways

* Git is a version control system that tracks changes in a folder.
* `git init` creates a `.git` folder with repository metadata.
* Git configuration can be local, global, or system-level.
* Remotes are repositories stored somewhere else, like GitHub.
* Branches allow separate lines of development.
* Good branch names use prefixes like `feature/`, `bugfix/`, and `refactor/`.
* Merge preserves history and is useful for shared branches.
* Rebase rewrites history and is best for private cleanup.
* Merge conflicts happen when Git cannot automatically combine changes.
* GitHub issues can represent tasks, features, bugs, or user stories.
* Good issues should follow INVEST: independent, negotiable, valuable, estimable, small, and testable.
* Code review should be collaborative, specific, and focused on improvement.
* Pull requests should include what changed, why it changed, how to test it, and known issues.
* ERDs show database tables and relationships.
* Primary keys uniquely identify records.
* Foreign keys connect records across tables.
* Inner classes are classes defined inside other classes.
* Inner classes can access private members of the outer class.
* Anonymous inner classes are useful for event handlers and quick interface implementations.
* Threads allow long-running work to happen in the background.
* Background threads should not directly update UI components.
* REST APIs let apps communicate with servers using HTTP.
* HTTP methods map to CRUD operations.
* Status codes tell whether an API request succeeded or failed.
* Retrofit is one way Kotlin apps can consume REST APIs.
