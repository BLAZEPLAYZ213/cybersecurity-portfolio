# Authentication - Two-Factor Authentication Bypass

## Overview
This lab demonstrates a flawed two-factor authentication (2FA) implementation where the second authentication step can be bypassed.

## Vulnerability
The application creates a valid authenticated session after the username and password are verified, without enforcing completion of the 2FA step. This allows attackers to bypass 2FA entirely.

## Objective
Access Carlos's account without providing the 2FA verification code.

## Reconnaissance
Valid credentials were already provided:
carlos:montoya

After logging in, the application prompted for a 2FA verification code.

## Exploitation

### Step 1: Initial Login
- Logged in using:
  carlos:montoya

### Step 2: 2FA Bypass
- Instead of entering the 2FA code, navigated directly to the homepage or another authenticated page.

### Step 3: Access Account
- The application allowed access without verifying the 2FA step.
- Successfully accessed Carlos's account.

## Result
Successfully bypassed two-factor authentication and accessed a protected account without providing the verification code.

## Evidence
- Screenshot of login page
<img width="1135" height="402" alt="image" src="https://github.com/user-attachments/assets/d7c3841f-a09f-49f1-9e64-1d2add9a3826" />

- Screenshot of 2FA prompt
<img width="1024" height="303" alt="image" src="https://github.com/user-attachments/assets/868726fe-512c-4180-94b2-c865455e8f71" />


- Screenshot showing access to account without completing 2FA

<img width="1344" height="601" alt="image" src="https://github.com/user-attachments/assets/13f2ddcb-a181-4e54-b68d-0f74dfdcb4b8" />


## Tools Used
- Browser

## Key Learning
- Two-factor authentication must be enforced server-side, not just at the user interface level.
- Authentication should not be considered complete until all steps are verified.
- Improper implementation of 2FA can completely nullify its security benefits.
