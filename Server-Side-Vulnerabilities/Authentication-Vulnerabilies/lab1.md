# Authentication - Username Enumeration & Brute-force Attack

## Overview
This lab demonstrates an authentication vulnerability where username enumeration and password brute-force attacks can be used to gain unauthorized access.

## Vulnerability
The application provides different responses for valid and invalid usernames, enabling username enumeration. Additionally, it lacks protection against brute-force attacks, allowing attackers to guess passwords.

## Objective
Enumerate a valid username and brute-force its password to access the account.

## Reconnaissance
Analyzed the login functionality and identified that the application behaves differently for valid and invalid usernames.

## Username Enumeration

### Tool Used
ffuf

### Method
Used ffuf to test multiple usernames and identify differences in server responses based on response size.

### Result
Identified a valid username based on a different response size.

## Password Brute-force

### Tool Used
Hydra

### Method
1. Identified login POST request:
   - Endpoint: /login
   - Parameters: username, password

2. Used Hydra with the valid username and password wordlist to perform brute-force attack.

### Result
Successfully discovered the correct password for the valid username.

## Exploitation
1. Logged in using the discovered credentials.
2. Accessed the user account successfully.
3. Lab completed.

## Evidence
- Screenshot of ffuf output showing different response size
<img width="785" height="519" alt="image" src="https://github.com/user-attachments/assets/a40cab07-8406-41f0-9c7d-6084a9be830d" />


- Screenshot of Hydra output with valid credentials
<img width="1320" height="520" alt="image" src="https://github.com/user-attachments/assets/a4e6a224-9205-4adf-9091-a93dcfba9926" />


- Screenshot of successful login
<img width="1359" height="591" alt="image" src="https://github.com/user-attachments/assets/c9ff86ed-0fcc-4782-89d4-a8cf8828dcfe" />



## Tools Used
- ffuf (for username enumeration)
- Hydra (for password brute-force)
- Browser (for request analysis and login)

## Key Learning
- Applications should not reveal different responses for valid and invalid usernames.
- Brute-force protection mechanisms (rate limiting, account lockout) are essential.
- Automation tools significantly improve attack efficiency.
- Proper authentication mechanisms are critical for application security.
