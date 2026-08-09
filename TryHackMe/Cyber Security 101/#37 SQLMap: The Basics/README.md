# SQLMap: The Basics

## Room Overview

**TryHackMe Room:** SQLMap: The Basics
**Primary Topic:** SQL Injection and SQLMap
**Difficulty:** Beginner
**Main Tool:** SQLMap

This room introduces the fundamentals of **SQL Injection (SQLi)** and teaches how **SQLMap** can be used to automate SQL Injection testing. The room focuses on understanding how web applications communicate with databases, how insecure input handling can lead to SQL Injection, and how SQLMap can identify and extract information from a vulnerable application.

The goal of this repository is not simply to record the answers from the room. It documents the concepts, methodology, commands, practical lessons, and learning experience gained while completing the room.

---

## Learning Objectives

By completing this room, you should understand:

* How web applications interact with databases.
* What SQL and SQL queries are.
* How databases organize information using tables, rows, and columns.
* What SQL Injection is.
* Why improper input validation can create SQL Injection vulnerabilities.
* How Boolean logic can be abused in SQL Injection.
* How SQLMap automates SQL Injection testing.
* How to identify an injectable URL parameter.
* How to enumerate databases with SQLMap.
* How to enumerate tables.
* How to dump data from a specific table.
* How GET-based SQL Injection testing works.
* Why authenticated applications may require session cookies during testing.
* How to inspect web requests using browser developer tools.
* The basic workflow of an SQL Injection assessment.

---

## Prerequisites

Before starting this room, it is useful to understand:

* Basic SQL syntax.
* SQL `SELECT` queries.
* Databases, tables, rows, and columns.
* Basic Boolean operators such as `AND` and `OR`.
* HTTP GET and POST requests.
* Basic Linux command-line usage.
* Basic understanding of web applications.

---

## How Web Applications Communicate with Databases

A typical web application does not allow the browser to communicate directly with the database.

The general flow is:

```text
User / Browser
      |
      | HTTP Request
      v
Web Server / Application
      |
      | SQL Query
      v
Database Server
      |
      | Query Result
      v
Web Server / Application
      |
      | HTTP Response
      v
User / Browser
```

For example, when a user submits a login form, the application may receive a username and password and use that information to construct a SQL query.

A simplified query could look like:

```sql
SELECT * FROM users
WHERE username = 'john'
AND password = 'password123';
```

The database evaluates the query and returns the matching record to the application.

The important security concept is that **user-controlled input can become part of a SQL query**. If the application does not handle that input safely, an attacker may be able to manipulate the query's logic.

---

## Understanding Database Structure

A database can contain multiple tables.

For example:

```text
Database: users

+----+----------+------------+
| id | username | password   |
+----+----------+------------+
| 1  | john     | ********   |
| 2  | alice    | ********   |
| 3  | david    | ********   |
+----+----------+------------+
```

Here:

* `users` is the table.
* `id`, `username`, and `password` are columns.
* Each horizontal entry represents a row.
* `id` identifies a particular record.

A SQL query can be used to retrieve specific records.

Example:

```sql
SELECT * FROM users
WHERE username = 'john'
AND password = 'password123';
```

`SELECT *` means to retrieve all columns from the matching records.

---

## What Is SQL Injection?

**SQL Injection is a vulnerability that occurs when attacker-controlled input is improperly incorporated into a SQL query.**

Instead of being treated purely as data, the input can influence the structure or logic of the SQL statement.

A vulnerable application might conceptually construct:

```sql
SELECT * FROM users
WHERE username = 'USER_INPUT'
AND password = 'PASSWORD_INPUT';
```

If the application does not safely handle the input, specially crafted input may alter the intended query.

For example, Boolean-based SQL Injection can attempt to introduce a condition that evaluates to true.

A simplified example is:

```text
' OR 1=1 --
```

The exact behavior depends on the application's query construction and the database management system.

The important concept is not memorizing a payload. The important concept is understanding that **the attacker is attempting to change the query's intended logic through input manipulation**.

---

## Boolean Logic and SQL Injection

Boolean operators are important when understanding SQL Injection.

For example:

```sql
1 = 1
```

is a true condition.

An SQL expression using `OR` can become true if at least one side of the condition is true.

Conceptually:

```text
FALSE OR TRUE = TRUE
```

By contrast, `AND` requires both conditions to be true:

```text
TRUE AND TRUE   = TRUE
TRUE AND FALSE  = FALSE
FALSE AND TRUE  = FALSE
```

This distinction is important for understanding why certain SQL Injection techniques can alter the result of a vulnerable query.

---

## What Is SQLMap?

**SQLMap is an open-source command-line tool designed to automate SQL Injection detection and exploitation.**

Manual SQL Injection testing can require trying many different inputs and analyzing how the application responds.

SQLMap automates much of this process.

At a high level, SQLMap can:

```text
Send test payloads
       |
       v
Analyze application responses
       |
       v
Identify possible SQL Injection
       |
       v
Fingerprint the database
       |
       v
Enumerate databases
       |
       v
Enumerate tables
       |
       v
Extract data
```

SQLMap does not simply send one payload. It can test different SQL Injection techniques and analyze the application's responses to determine whether a parameter appears injectable.

---

## SQLMap as a Command-Line Tool

SQLMap is primarily operated from the terminal.

A beginner-friendly mode is:

```bash
sqlmap --wizard
```

The wizard provides an interactive workflow and asks questions about the target and testing process.

This is useful when learning SQLMap because the tool guides the user through its options instead of requiring every command-line option to be memorized.

---

## Basic SQLMap Workflow

The room introduces a basic workflow:

```text
1. Identify an injectable parameter
2. Confirm SQL Injection
3. Enumerate databases
4. Enumerate tables
5. Dump required data
```

This workflow is important because SQL Injection testing is not simply about running a tool and immediately extracting information.

The tester first needs to identify the potential injection point and understand what the application is doing.

---

## Step 1: Test a URL Parameter

A GET request may contain parameters directly in the URL.

Example:

```text
http://target.example/page.php?cat=1
```

Here:

```text
cat
```

is the parameter and:

```text
1
```

is its value.

A basic SQLMap scan can be performed with:

```bash
sqlmap -u "http://target.example/page.php?cat=1"
```

SQLMap can test whether the parameter appears to be injectable.

The important part is understanding that the **parameter is the potential injection point**.

---

## Step 2: Enumerate Databases

After identifying a vulnerable target, SQLMap can enumerate available databases.

```bash
sqlmap -u "http://target.example/page.php?cat=1" --dbs
```

The `--dbs` option requests the available database names.

Conceptually:

```text
Target
 |
 +-- Database 1
 |
 +-- Database 2
 |
 +-- Database 3
```

The actual number and names depend on the target.

---

## Step 3: Enumerate Tables

Once a database has been identified, SQLMap can enumerate its tables.

Example:

```bash
sqlmap -u "http://target.example/page.php?cat=1" -D users --tables
```

Here:

```text
-D users
```

selects the `users` database.

```text
--tables
```

asks SQLMap to enumerate the tables inside that database.

The conceptual structure becomes:

```text
Database: users

+-- accounts
+-- customers
+-- sessions
```

---

## Step 4: Dump Table Data

After identifying a table, SQLMap can dump its contents.

Example:

```bash
sqlmap -u "http://target.example/page.php?cat=1" -D users -T accounts --dump
```

Here:

```text
-D users
```

selects the database.

```text
-T accounts
```

selects the table.

```text
--dump
```

requests the table data.

A more targeted extraction can specify particular columns:

```bash
sqlmap -u "http://target.example/page.php?cat=1" -D users -T accounts -C email,password --dump
```

The `-C` option specifies the columns to retrieve.

---

## GET Requests and SQLMap

The room primarily focuses on **GET-based SQL Injection testing**.

A GET request may expose parameters in the URL:

```text
/page.php?cat=1
```

This makes the parameter relatively easy to identify and test.

For example:

```bash
sqlmap -u "http://target.example/page.php?cat=1"
```

SQLMap can then test the parameter.

---

## POST Requests

POST requests commonly place submitted data inside the request body instead of directly exposing it in the URL.

For example, login data may conceptually look like:

```text
username=john&password=password123
```

The room does not focus deeply on POST request testing.

The important distinction is:

```text
GET
Parameter commonly visible in URL

POST
Parameter commonly contained in request body
```

For POST-based testing, the request generally needs to be captured and provided to SQLMap appropriately.

---

## Capturing Hidden GET Parameters

One practical challenge in the room is that the complete GET request may not always be obvious from the visible page.

Browser Developer Tools can help identify the request.

A basic process is:

```text
Open target application
        |
        v
Open Developer Tools
        |
        v
Open Network tab
        |
        v
Perform the action
        |
        v
Locate the request
        |
        v
Inspect the URL and parameters
```

For example, after submitting a login form, the Network tab may reveal:

```text
email=test
password=test
```

inside the request URL.

The complete URL can then be provided to SQLMap for authorized testing.

---

## Authentication and Cookies

Some web applications require authentication before allowing access to functionality.

Simply providing the URL to SQLMap may not be sufficient because the request may be treated as unauthenticated.

A logged-in browser session may contain a session cookie.

Conceptually:

```text
Login
  |
  v
Server creates session
  |
  v
Browser receives session cookie
  |
  v
Browser sends cookie with future requests
  |
  v
Application recognizes authenticated user
```

SQLMap can use cookies when authorized testing requires an authenticated session.

A simplified example is:

```bash
sqlmap -u "http://target.example/page.php?cat=1" --cookie="session=VALUE"
```

The exact cookie value should come from the authorized test environment.

---

## SQL Injection Techniques

SQLMap can test multiple SQL Injection techniques.

Common categories include:

* Boolean-based blind SQL Injection
* Error-based SQL Injection
* Time-based blind SQL Injection
* UNION-based SQL Injection

Different applications behave differently, so the most suitable technique depends on how the target responds to injected input.

---

## Practical Room Methodology

The practical exercise followed this general process:

```text
Target Login Page
        |
        v
Submit Test Input
        |
        v
Inspect Network Requests
        |
        v
Identify GET Request
        |
        v
Obtain Complete URL
        |
        v
Run SQLMap
        |
        v
Identify SQL Injection
        |
        v
Enumerate Databases
        |
        v
Enumerate Tables
        |
        v
Dump Relevant Data
```

The vulnerable parameter in the practical exercise was identified from the captured request.

The exercise then demonstrated how SQLMap could move from vulnerability detection to database enumeration and data extraction.

---

## Key SQLMap Commands

### Test a URL

```bash
sqlmap -u "TARGET_URL"
```

### Enumerate databases

```bash
sqlmap -u "TARGET_URL" --dbs
```

### Enumerate tables

```bash
sqlmap -u "TARGET_URL" -D DATABASE_NAME --tables
```

### Dump a table

```bash
sqlmap -u "TARGET_URL" -D DATABASE_NAME -T TABLE_NAME --dump
```

### Dump specific columns

```bash
sqlmap -u "TARGET_URL" -D DATABASE_NAME -T TABLE_NAME -C COLUMN1,COLUMN2 --dump
```

### Use an authenticated session cookie

```bash
sqlmap -u "TARGET_URL" --cookie="SESSION_COOKIE"
```

### Interactive SQLMap wizard

```bash
sqlmap --wizard
```

---

## Practical Learning Exercises

### Exercise 1: Understand SQL Queries

Create a small example database containing:

```text
id
username
password
```

Write SQL queries that retrieve:

```text
All users
One specific user
Users matching a specific username
Users matching both username and password
```

The goal is to become comfortable reading SQL before using SQLMap.

### Exercise 2: Understand Boolean Logic

Practice evaluating:

```text
1 = 1
1 = 2
TRUE AND TRUE
TRUE AND FALSE
FALSE OR TRUE
FALSE OR FALSE
```

Then connect the results to how SQL Injection can manipulate query logic.

### Exercise 3: Identify GET Parameters

Open a deliberately vulnerable practice application and inspect its Network requests.

Identify:

```text
HTTP method
URL
Parameter names
Parameter values
Response
```

### Exercise 4: SQLMap Enumeration

On an authorized TryHackMe or local lab target:

```text
Identify injectable parameter
        ↓
Enumerate databases
        ↓
Choose a database
        ↓
Enumerate tables
        ↓
Choose a table
        ↓
Inspect relevant columns
        ↓
Extract permitted lab data
```

The objective is to understand the workflow rather than memorize commands.

---

## Common Beginner Mistakes

### Confusing a Database with a Table

A database can contain multiple tables.

```text
Database
 |
 +-- Table
 +-- Table
 +-- Table
```

Do not treat the database name and table name as interchangeable.

### Forgetting the URL Parameter

SQLMap needs to know what request it should test. A URL such as:

```text
http://target.example/page.php
```

is different from:

```text
http://target.example/page.php?cat=1
```

The second URL contains a parameter that may be testable.

### Testing Without Authorization

SQL Injection testing against systems without permission can be illegal and harmful.

Use SQLMap only against systems you own or environments where you have explicit authorization, such as TryHackMe labs.

### Blindly Copying Commands

Memorizing:

```bash
--dbs
--tables
--dump
```

is less valuable than understanding what each option does and why it is being used.

---

## Real-World Security Relevance

SQL Injection can expose sensitive application data when an application constructs SQL queries unsafely.

Depending on the vulnerability and database permissions, an attacker may potentially:

```text
Read sensitive data
Enumerate database structures
Modify records
Bypass authentication
Access confidential information
```

The actual impact depends on the application's architecture, database permissions, query construction, and security controls.

Modern applications should prevent SQL Injection through secure development practices such as parameterized queries and prepared statements rather than relying on input filtering alone.

---

## Important Security Lessons

The room demonstrates an important principle:

> **User input should never be blindly trusted when constructing database queries.**

A secure application should separate data from SQL instructions.

The preferred defense is generally **parameterized queries / prepared statements**.

Other security controls can provide additional protection, but input filtering alone should not be treated as the primary SQL Injection defense.

---

## What I Learned From This Room

This room connected several concepts that are important for web application security.

First, I understood the relationship between the browser, web server, and database. The browser sends a request to the web application, the application interacts with the database using SQL, and the resulting data is returned to the user.

Second, I understood SQL Injection as a **query-logic manipulation problem**, rather than simply memorizing SQL Injection payloads.

Third, I learned that SQLMap automates much of the repetitive work involved in SQL Injection testing. It can test parameters, analyze responses, identify possible vulnerabilities, enumerate databases and tables, and retrieve data from authorized targets.

Finally, the practical exercise demonstrated that finding the correct request is an important part of the assessment. Before using SQLMap, the tester needs to understand the application's request and identify the parameter that may be vulnerable.

---

## Final Takeaways

The most important concepts from this room are:

```text
SQL
 |
 +-- Language used to interact with relational databases
 |
 +-- Databases contain tables
 |
 +-- Tables contain rows and columns

SQL Injection
 |
 +-- Caused by unsafe handling of SQL-related input
 |
 +-- Can manipulate query logic
 |
 +-- May expose sensitive database information

SQLMap
 |
 +-- Automates SQL Injection testing
 |
 +-- Can identify injectable parameters
 |
 +-- Can enumerate databases
 |
 +-- Can enumerate tables
 |
 +-- Can extract authorized lab data
```

The most important lesson is to understand **why the commands work**, not simply memorize them. SQLMap is a powerful automation tool, but effective security testing still requires understanding HTTP requests, SQL, database structure, application behavior, and the underlying vulnerability.
