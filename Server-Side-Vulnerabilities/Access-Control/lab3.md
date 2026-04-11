# Access Control - User Role Controlled by Cookie

## Overview
This lab demonstrates a broken access control vulnerability where the application determines user privileges based on a client-controlled cookie.

## Vulnerability
The application uses a cookie (`admin`) to determine whether a user has administrative privileges. Since cookies can be modified by the client, this allows privilege escalation.

## Objective
Access the admin panel and delete the user "carlos".

## Reconnaissance
Logged in using provided credentials:
wiener:peter

After login, inspected browser cookies using Developer Tools.

## Identified Cookie
admin=false

## Steps to Reproduce
1. Logged in as a normal user (wiener:peter).
2. Opened Developer Tools → Application tab.
3. Located cookies for the website.
4. Found the cookie:
   admin=false
5. Modified the value to:
   admin=true
6. Refreshed the page.
7. Gained access to the admin panel (/admin).
8. Deleted the user "carlos".

## Result
Successfully escalated privileges by modifying the cookie and accessed the admin panel to delete the user "carlos".

## Evidence
- Screenshot of login
<img width="755" height="540" alt="image" src="https://github.com/user-attachments/assets/e2e94a74-09c2-4673-9d6b-44ed92e92c19" />

- Screenshot of cookie before modification (admin=false)
<img width="496" height="170" alt="image" src="https://github.com/user-attachments/assets/91518e4c-1e5b-41c9-874b-bd4038b9a55f" />

- Screenshot of modified cookie (admin=true)
<img width="566" height="276" alt="image" src="https://github.com/user-attachments/assets/1a5f4064-c69d-4e6f-a5ae-1e846087df0c" />

- Screenshot of admin panel access
<img width="1340" height="684" alt="image" src="https://github.com/user-attachments/assets/1ed6ef97-7f44-434f-9568-68c4315c08d4" />

- Screenshot of user deletion
<img width="773" height="573" alt="image" src="https://github.com/user-attachments/assets/c23da67d-0a5c-4800-99c8-4b65b09eb8c0" />


## Tools Used
- Browser Developer Tools (Application tab)

## Key Learning
- Client-side data such as cookies should never be trusted for access control.
- Privilege decisions must be enforced on the server side.
- Cookie manipulation can lead to privilege escalation.
