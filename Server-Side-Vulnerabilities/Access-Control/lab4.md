# Access Control - Horizontal Privilege Escalation (IDOR with GUID)

## Overview
This lab demonstrates a horizontal privilege escalation vulnerability where a user can access another user's data by manipulating a request parameter.

## Vulnerability
The application uses a user-controlled parameter (id) to fetch account data without proper authorization checks. This leads to an Insecure Direct Object Reference (IDOR).

## Objective
Find the GUID for the user "carlos" and retrieve his API key.

## Reconnaissance
Logged in using provided credentials:
wiener:peter

While browsing the application, found a post made by the user "carlos". By clicking on his profile, his user ID (GUID) was revealed in the URL.

## Discovered Information
Carlos's GUID was exposed in the URL when accessing his profile.

## Steps to Reproduce
1. Logged in as a normal user (wiener:peter).
2. Navigated through the application and found a post by "carlos".
3. Clicked on the user "carlos" to view his profile.
4. Observed the URL and copied his GUID.
5. Navigated to the account page:
   /my-account?id=<your-id>
6. Replaced the id parameter with Carlos's GUID.
7. Accessed Carlos's account page.
8. Retrieved his API key.

## Result
Successfully accessed another user's account data and retrieved sensitive information (API key), completing the lab.

## Evidence
- Screenshot of Carlos profile showing GUID
<img width="1339" height="678" alt="image" src="https://github.com/user-attachments/assets/74f82219-e153-453d-8f33-6f5764d4245d" />

- Screenshot of Carlos id
<img width="1341" height="684" alt="image" src="https://github.com/user-attachments/assets/ec4859fc-a440-44fc-a45a-9c05af752666" />

- Screenshot of modified URL
<img width="1349" height="678" alt="image" src="https://github.com/user-attachments/assets/74f4efd3-b254-4a1d-ad70-ec9c25a2c173" />

- Screenshot of retrieved API key
<img width="1352" height="599" alt="image" src="https://github.com/user-attachments/assets/e2acbd3b-f4d8-43ef-b872-78f68d95cc60" />


## Tools Used
- Browser (for navigation and URL manipulation)

## Key Learning
- User-controlled parameters should not be trusted for access control.
- Applications must enforce authorization checks on every request.
- Sensitive identifiers (GUIDs) should not be exposed unnecessarily.
- IDOR vulnerabilities can lead to unauthorized data access.
