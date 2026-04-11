# Access Control - Horizontal to Vertical Privilege Escalation (Password Disclosure)

## Overview
This lab demonstrates how a horizontal privilege escalation vulnerability can be leveraged to achieve vertical privilege escalation by compromising an administrator account.

## Vulnerability
The application allows users to access other users' account pages by modifying the "id" parameter. Additionally, the account page exposes the user's password in a prefilled input field, leading to sensitive information disclosure.

## Objective
Retrieve the administrator's password and use it to delete the user "carlos".

## Reconnaissance
Logged in using provided credentials:
wiener:peter

Observed that the account page uses a parameter:
 /my-account?id=wiener

## Exploitation

### Step 1: Horizontal Privilege Escalation
- Modified the URL parameter:
  /my-account?id=administrator
- Gained access to the administrator account page.

### Step 2: Password Disclosure
- The password field was prefilled but masked.
- Viewed the page source / inspected the element.
- Retrieved the administrator's password from the HTML (`value` attribute).

### Step 3: Vertical Privilege Escalation
- Logged in as administrator using the retrieved password.
- Accessed the admin panel.
- Deleted the user "carlos".

## Result
Successfully escalated privileges from a normal user to administrator and deleted the user "carlos".

## Evidence
- Screenshot of modified URL (/my-account?id=administrator) and admin account page
<img width="1347" height="682" alt="image" src="https://github.com/user-attachments/assets/1ecb6cbc-fecb-469d-bc50-858853d20025" />

- Screenshot of password visible in page source
<img width="1340" height="667" alt="image" src="https://github.com/user-attachments/assets/9aac386f-bb87-42ec-820f-b2452492e640" />

- Screenshot of admin panel access
<img width="1357" height="546" alt="image" src="https://github.com/user-attachments/assets/6bbc79ab-66ee-4279-ad50-8f99777537d9" />

- Screenshot of user deletion
<img width="1346" height="557" alt="image" src="https://github.com/user-attachments/assets/04254d95-6dba-45a2-ac79-46d15291a883" />


## Tools Used
- Browser (for URL manipulation and inspection)

## Key Learning
- Horizontal privilege escalation can lead to full administrative compromise.
- Sensitive data like passwords must never be exposed in client-side code.
- Access control must be enforced on every request.
- Input parameters should not determine access without proper validation.
