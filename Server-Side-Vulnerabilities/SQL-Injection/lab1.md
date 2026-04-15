# SQL Injection - Retrieving Hidden Data

## Overview
This lab demonstrates a SQL injection vulnerability that allows attackers to manipulate database queries and retrieve hidden data.

## Vulnerability
The application uses user input directly in a SQL query without proper sanitization. This allows attackers to inject SQL syntax and alter the query logic.

## Objective
Perform a SQL injection attack to display unreleased products.

## Reconnaissance
The application filters products based on category using a URL parameter:

/products?category=Gifts

The backend query:

SELECT * FROM products WHERE category = 'Gifts' AND released = 1

---

## Exploitation

### Step 1: Identify Injection Point
Tested input using `'` and observed abnormal behavior, confirming possible SQL injection.

---

### Step 2: Break Query Structure
Injected:

Gifts'

---

### Step 3: Use SQL Comment
Injected:

Gifts'--

This removed the condition:
AND released = 1

---

### Step 4: Force True Condition
Injected:

Gifts' OR 1=1--

This modified the query to:

SELECT * FROM products WHERE category = 'Gifts' OR 1=1

---

### Step 5: Retrieve Hidden Data
The condition `OR 1=1` always evaluates to TRUE, causing the application to return all products, including unreleased ones.

---

## Result
Successfully retrieved hidden (unreleased) products by exploiting SQL injection.

## Evidence
- Screenshot of normal product view
<img width="1330" height="674" alt="image" src="https://github.com/user-attachments/assets/9966d48c-0def-4292-97a3-6abd7c14cf0a" />

- Screenshot of injected URL
<img width="766" height="42" alt="image" src="https://github.com/user-attachments/assets/6a459285-93ee-42fd-90e0-c1f9f06990b5" />

- Screenshot showing additional (hidden) products
<img width="1352" height="676" alt="image" src="https://github.com/user-attachments/assets/a0c47835-6326-4207-9a66-2793abec9013" />

## Tools Used
- Browser

## Key Learning
- SQL injection allows attackers to manipulate database queries.
- Comment operators (`--`) can remove security conditions.
- Boolean conditions (`OR 1=1`) can bypass filters.
- Input validation and parameterized queries are essential defenses.
