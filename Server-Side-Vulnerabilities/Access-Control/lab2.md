# Access Control - Unprotected Admin Functionality (Obscured URL)

## Overview
This lab demonstrates a broken access control vulnerability where administrative functionality is hidden using an unpredictable URL but is still accessible without proper authorization.

## Vulnerability
Sensitive functionality was hidden (security by obscurity) but not protected by proper access control, allowing unauthorized users to access it.

## Objective
Access the hidden admin panel and delete the user "carlos".

## Reconnaissance
While analyzing the application, JavaScript code revealed a hidden admin panel URL.

The script contained:
var isAdmin = false;
if (isAdmin) {
   adminPanelTag.setAttribute('href', '/admin-4iupkx');
}

This exposed the admin endpoint.

## Discovered Endpoint
/admin-4iupkx

## Steps to Reproduce
1. Inspected the webpage source / JavaScript.
2. Found a script containing a hidden admin URL.
3. Identified the endpoint: /admin-4iupkx
4. Accessed the endpoint directly in the browser.
5. Gained access to admin panel without authentication.
6. Deleted the user "carlos".

## Result
Successfully accessed the hidden admin panel and deleted the user "carlos", completing the lab.

## Evidence
<img width="1091" height="674" alt="image" src="https://github.com/user-attachments/assets/95364dc0-4388-4333-b5f7-85d5df75bc78" />

<img width="1339" height="673" alt="image" src="https://github.com/user-attachments/assets/9d020053-fd42-4c21-b3af-2f81ccdcc314" />
<img width="1350" height="593" alt="image" src="https://github.com/user-attachments/assets/18cdf8f0-544e-45ad-8972-9181f5a249e7" />

## Tools Used
- Browser (Developer Tools)

## Key Learning
- Security by obscurity is not a valid protection mechanism.
- Sensitive endpoints must be protected with proper authentication and authorization.
- JavaScript files can leak critical information about application functionality.
