# OS Command Injection - Simple Case

## Overview
This lab demonstrates an OS command injection vulnerability where user input is directly used in a system command without proper sanitization.

## Vulnerability
The application executes a shell command using user-supplied input (productID and storeID). This allows attackers to inject additional commands.

## Objective
Execute the `whoami` command to determine the current system user.

## Reconnaissance
Identified a stock check feature that sends a request:

POST /product/stock

Parameters:
- productID
- storeID

The application uses these inputs in a backend shell command.

## Exploitation

### Step 1: Identify Injection Point
Tested input and observed command execution behavior via error messages.

---

### Step 2: Inject Command
Used command separator to inject:

productID=1;whoami #&storeID=1

---

### Step 3: Bypass Argument Issues
- Used `;` to execute a new command.
- Used `#` to comment out trailing input and prevent syntax errors.

---

### Step 4: Execute Command
The final executed command resembled:

stockreport.sh 1; whoami

---

## Result
Successfully executed the `whoami` command and retrieved the system user.

## Evidence
- Screenshot of injected request
<img width="513" height="319" alt="image" src="https://github.com/user-attachments/assets/33e736c7-b676-455f-8775-5a72d99bc593" />

- Screenshot of response showing command output
<img width="520" height="312" alt="image" src="https://github.com/user-attachments/assets/37d70984-56fd-4b6b-a74c-3bf839298b82" />

- Screenshot of lab completion
<img width="1355" height="599" alt="image" src="https://github.com/user-attachments/assets/798e37b0-138e-4267-a6c2-edfb8dbc8ad9" />


## Tools Used
- Burp Suite (Proxy + Repeater)
- Browser

## Key Learning
- Unsanitized user input can lead to OS command injection.
- Command separators (`;`, `&&`, `|`) allow chaining commands.
- Comment operator (`#`) can neutralize trailing input.
- Proper input validation and sanitization are critical.
