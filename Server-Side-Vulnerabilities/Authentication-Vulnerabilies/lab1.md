# Authentication - Username Enumeration & Brute-force Attack

## Overview
This lab demonstrates an authentication vulnerability where differences in server responses allow username enumeration, followed by a brute-force attack to obtain valid credentials.

## Vulnerability
The application reveals different responses for valid and invalid usernames, enabling username enumeration. It also lacks protection against brute-force attacks, allowing attackers to guess passwords.

## Objective
Enumerate a valid username and brute-force its password to access the account.

## Reconnaissance
Analyzed the login functionality and observed that the application responds differently for valid and invalid usernames.

## Username Enumeration

### Tool Used
ffuf

### Method
Used ffuf to fuzz the username parameter and identify differences in response size.

### Result
Identified a valid username based on a unique response size.

## Password Brute-force

### Tool Used
Hydra

### Method
1. Identified login POST request:
   - Endpoint: /login
   - Parameters: username, password

2. Used Hydra with the valid username and password wordlist to perform brute-force attack.

3. Adjusted Hydra configuration to match the exact failure response:
   "Incorrect password"

### Result
Successfully discovered the correct password.

## Exploitation
1. Logged in using the discovered credentials.
2. Accessed the user account successfully.
3. Lab completed.

## Evidence
- Screenshot of ffuf output showing response differences

<img width="785" height="519" alt="image" src="https://github.com/user-attachments/assets/a40cab07-8406-41f0-9c7d-6084a9be830d" />

- Screenshot of Hydra output with valid credentials

<img width="1320" height="520" alt="image" src="https://github.com/user-attachments/assets/a4e6a224-9205-4adf-9091-a93dcfba9926" />

- Screenshot of successful login

<img width="1359" height="591" alt="image" src="https://github.com/user-attachments/assets/c9ff86ed-0fcc-4782-89d4-a8cf8828dcfe" />

## Tools Used
- ffuf (for username enumeration)
- Hydra (for password brute-force)
- Browser Developer Tools (for request analysis)

## Key Learning
- Authentication responses should not reveal whether a username is valid.
- Brute-force protection mechanisms (rate limiting, CAPTCHA) are essential.
- Exact matching in automated tools is critical to avoid false positives.
- Combining enumeration and brute-force leads to efficient attacks.








