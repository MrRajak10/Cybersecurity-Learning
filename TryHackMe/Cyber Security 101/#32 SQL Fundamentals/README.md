# README.md

# SQL Fundamentals — TryHackMe

A learning-focused repository documenting my journey through the **TryHackMe SQL Fundamentals** room. This repository focuses on understanding SQL concepts, relational databases, CRUD operations, SQL clauses, operators, functions, and how these concepts apply to cybersecurity rather than simply completing the room.

---

## Overview

Databases are used by almost every modern application. Whether it is a social media platform, banking website, e-commerce application, or enterprise software, user information is stored inside databases.

As cybersecurity professionals, understanding databases is essential because attackers frequently target them, and defenders must understand how data is stored, accessed, modified, and protected.

This room introduces SQL from a beginner's perspective and builds the foundation required for later topics such as SQL Injection, authentication bypass, database enumeration, digital forensics, threat hunting, and secure application development.

---

# Learning Objectives

After completing this room, I learned how to:

* Understand what a database is.
* Differentiate between relational and non-relational databases.
* Understand tables, rows, and columns.
* Understand Primary Keys and Foreign Keys.
* Understand the purpose of DBMS.
* Learn what SQL is and why it exists.
* Perform CRUD operations.
* Create and manage databases and tables.
* Retrieve and manipulate data using SQL.
* Use SQL clauses.
* Use SQL operators.
* Use SQL functions.
* Practice SQL directly inside MySQL.

---

# Topics Covered

## Database Fundamentals

* What is a database?
* Why databases are important
* Real-world examples
* Structured data storage

---

## Types of Databases

### Relational Databases

Examples:

* MySQL
* PostgreSQL
* MariaDB

Characteristics:

* Tables
* Rows
* Columns
* Structured data
* SQL-based

---

### Non-Relational Databases (NoSQL)

Examples:

* MongoDB

Characteristics:

* Key-Value
* Document
* Graph
* Flexible schema

---

## Database Structure

Learned:

* Tables
* Rows
* Columns
* Records

---

## Keys

### Primary Key

Purpose:

* Identifies each record uniquely.
* Cannot contain duplicate values.
* Cannot contain NULL values.

Example:

```
Student_ID
Book_ID
Employee_ID
```

---

### Foreign Key

Purpose:

* Connects two tables.
* Maintains relationships.
* References another table's Primary Key.

---

# DBMS

Examples:

* MySQL
* Oracle
* MariaDB
* MongoDB

A Database Management System (DBMS) acts as the interface between users/applications and the database.

Responsibilities include:

* Managing data
* Retrieving data
* Updating records
* Deleting records
* Organizing storage

---

# SQL Basics

SQL (Structured Query Language) is used to communicate with relational databases.

Common tasks include:

* Creating data
* Reading data
* Updating data
* Deleting data

---

# Database Statements Learned

## Database Operations

* CREATE DATABASE
* SHOW DATABASES
* USE
* DROP DATABASE

---

## Table Operations

* CREATE TABLE
* SHOW TABLES
* DESCRIBE
* ALTER TABLE
* DROP TABLE

---

# CRUD Operations

## Create

Used to insert new records.

Statement:

```
INSERT INTO
```

---

## Read

Used to retrieve information.

Statement:

```
SELECT
```

---

## Update

Used to modify existing records.

Statement:

```
UPDATE
```

---

## Delete

Used to remove records.

Statement:

```
DELETE
```

---

# SQL Clauses Learned

* FROM
* WHERE
* DISTINCT
* GROUP BY
* ORDER BY
* HAVING

---

# SQL Operators Learned

Logical Operators

* AND
* OR
* NOT

Pattern Matching

* LIKE

Range

* BETWEEN

Comparison

* =
* !=
* <
* >
* <=
* > =

---

# SQL Functions Learned

## String Functions

* CONCAT()
* GROUP_CONCAT()
* SUBSTRING()
* LENGTH()

---

## Aggregate Functions

* COUNT()
* SUM()
* MAX()
* MIN()

---

# Hands-on Practice

Practical activities completed during the room included:

* Connecting to MySQL
* Creating databases
* Listing databases
* Selecting active databases
* Creating tables
* Viewing table structures
* Reading table data
* Filtering records
* Sorting results
* Grouping results
* Using operators
* Using SQL functions

---

# Cybersecurity Relevance

Understanding SQL is important because it directly supports many cybersecurity roles.

## Penetration Testing

* SQL Injection testing
* Authentication bypass testing
* Database enumeration
* Data extraction

---

## SOC Analyst

* Understanding application data
* Investigating alerts involving databases
* Log analysis
* Incident investigation

---

## Threat Hunting

* Investigating database activity
* Identifying suspicious queries
* Detecting unauthorized access

---

## DFIR

* Reviewing stored information
* Investigating compromised databases
* Understanding attacker activity

---

# Key Takeaways

* Databases store organized information.
* Relational databases use tables.
* SQL is used to communicate with relational databases.
* CRUD operations are fundamental to SQL.
* Clauses help filter, group, and sort data.
* Operators define conditions.
* Functions manipulate and summarize data.
* SQL fundamentals form the foundation for SQL Injection and many cybersecurity topics.

---

# Skills Gained

* Database fundamentals
* SQL basics
* Database management
* Query writing
* Data retrieval
* Data manipulation
* SQL filtering
* SQL sorting
* SQL grouping
* Understanding relational databases
* Understanding DBMS

---

# Next Learning Goals

* SQL Injection
* Authentication Bypass
* UNION-based SQL Injection
* Error-based SQL Injection
* Blind SQL Injection
* Database Enumeration
* Web Application Security
* Burp Suite
* OWASP Top 10

---

# Resources

* TryHackMe — SQL Fundamentals
* MySQL Documentation
* PostgreSQL Documentation
* SQLBolt
* W3Schools SQL Tutorial

---

# Disclaimer

This repository is intended for educational purposes only. The focus is on learning SQL concepts and understanding how databases work in cybersecurity environments.
