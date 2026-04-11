# Path Traversal - Accessing Sensitive Files

## Overview
This lab demonstrates a path traversal vulnerability where an attacker can access files outside the intended directory using directory traversal sequences.

## Vulnerability
Path traversal (directory traversal) allows attackers to access restricted files by manipulating file path inputs using sequences like "../".

## Target Endpoint
/image?filename=

## Payload Used
../../../etc/passwd

## Steps to Reproduce
1. Identified a file parameter in the URL:
   /image?filename=

2. Modified the parameter by adding directory traversal sequences:
   ../../../etc/passwd

3. Sent the request to the server.

4. The server processed the request and attempted to retrieve a system file.

## Result
The lab was successfully completed, indicating that the application allowed access to a sensitive system file.

## Evidence
<img width="1346" height="670" alt="image" src="https://github.com/user-attachments/assets/dcef9dc8-2cc7-4f2c-8dd8-a258d6b3a140" />

<img width="526" height="236" alt="image" src="https://github.com/user-attachments/assets/b7b42a4c-97cb-431a-942a-273275b4e67f" />

- Lab completion confirmation
- <img width="1336" height="605" alt="image" src="https://github.com/user-attachments/assets/4923ed05-1f15-445e-a7df-6c2fdc173496" />


## Tools Used
- Browser (for initial testing)
- Burp Suite (for request interception and analysis)

## Key Learning
- Applications must properly validate and sanitize user input.
- Directory traversal sequences can bypass file access restrictions.
- Even if output is not clearly visible, backend processing may still succeed.
