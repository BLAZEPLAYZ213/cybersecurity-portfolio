# Access Control - Unprotected Admin Functionality

## Overview
This lab demonstrates a broken access control vulnerability where administrative functionality is accessible without proper authentication.

## Vulnerability
Unprotected admin functionality allows attackers to access sensitive endpoints directly without proper authorization.

## Objective
Delete the user "carlos".

## Reconnaissance
Performed directory enumeration using Gobuster and discovered the file "/robots.txt".

The robots.txt file contained:
Disallow: /administrative-panel

This revealed the hidden admin endpoint.

## Discovered Endpoint
/administrative-panel

## Steps to Reproduce
1. Used Gobuster to find hidden files and directories.
2. Discovered "/robots.txt".
3. Accessed robots.txt and found:
   Disallow: /administrative-panel
4. Navigated to "/administrative-panel".
5. Accessed admin panel without authentication.
6. Deleted the user "carlos".

## Result
Successfully accessed the admin panel and deleted the user "carlos", completing the lab.

## Evidence
<img width="579" height="455" alt="image" src="https://github.com/user-attachments/assets/e1d7a73d-8934-4c4d-9dd5-2463c15823f5" />
<img width="1353" height="598" alt="image" src="https://github.com/user-attachments/assets/cd26efa6-f6c6-4349-911a-2bb1c8f45a8a" />


## Tools Used
- Gobuster
- Browser

## Key Learning
- robots.txt can expose sensitive endpoints.
- Security should not rely on hidden URLs.
- Proper access control must be enforced on all sensitive functionalities.
