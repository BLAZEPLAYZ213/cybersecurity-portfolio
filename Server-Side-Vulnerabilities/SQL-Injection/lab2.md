# SQL Injection - Authentication Bypass

## Overview
This lab demonstrates how SQL injection can be used to bypass authentication mechanisms and gain unauthorized access to user accounts.

## Vulnerability
The application constructs a SQL query using unsanitized user input for username and password. This allows attackers to manipulate the query logic.

## Objective
Log in as the administrator user without knowing the password.

## Reconnaissance
The login functionality sends user credentials:

username=...
password=...

The backend query:

SELECT * FROM users WHERE username = 'username' AND password = 'password'

---

## Exploitation

### Step 1: Analyze Query Structure
Observed that both username and password are directly embedded in the SQL query.

---

### Step 2: Break Query Logic
Injected into username:

administrator'--

Password left blank.

---

### Step 3: Modify Query Behavior
The resulting query becomes:

SELECT * FROM users WHERE username = 'administrator'--' AND password = ''

---

### Step 4: Bypass Authentication
- The `--` comments out the password check.
- The query only checks for username = 'administrator'.
- Authentication succeeds without verifying password.

---

## Result
Successfully logged in as the administrator user without knowing the password.

## Evidence
- Screenshot of login request
<img width="772" height="340" alt="image" src="https://github.com/user-attachments/assets/d46eb838-5262-4e01-84bd-8fef078dd5e2" />


- Screenshot of successful login as administrator
<img width="798" height="318" alt="image" src="https://github.com/user-attachments/assets/b87d0b9f-9de3-4f4a-9bab-8255943d16d5" />

- Screenshot of lab completion
<img width="1355" height="687" alt="image" src="https://github.com/user-attachments/assets/ae415b87-ba84-4558-b5be-e85035f738e5" />

## Tools Used
- Browser

## Key Learning
- SQL injection can bypass authentication controls.
- Comment operators (`--`) can remove critical security checks.
- Never trust user input in authentication queries.
- Use parameterized queries and prepared statements to prevent SQL injection.
