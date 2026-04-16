# SSRF - Blacklist Filter Bypass

## Overview
This lab demonstrates how weak blacklist-based SSRF defenses can be bypassed using encoding and alternative representations.

## Vulnerability
The application fetches data from a user-supplied URL but implements weak filtering to block:
- localhost / 127.0.0.1
- /admin endpoint

These defenses are insufficient and can be bypassed.

## Objective
Bypass SSRF filters to access the internal admin panel and delete the user "carlos".

## Reconnaissance
Identified a stock check feature using:

stockApi=http://...

Observed that direct requests to:
- http://localhost/admin
- http://127.0.0.1/admin

were blocked.

---

## Exploitation

### Step 1: Bypass IP Filter
Used alternative IP representation:

http://127.1/

This bypassed filtering for localhost.

---

### Step 2: Bypass Path Filter
The `/admin` path was blocked.

Used double URL encoding:

%2561dmin → decoded to %61dmin → admin

---

### Step 3: Combine Bypasses
Final payload:

http://127.1/%2561dmin

---

### Step 4: Access Admin Panel
Successfully accessed internal admin interface.

---

### Step 5: Perform Action
Used endpoint to delete user:

/admin/delete?username=carlos

---

## Result
Successfully bypassed SSRF filters and accessed internal functionality.

## Evidence
- Screenshot of bypass payload
<img width="501" height="315" alt="image" src="https://github.com/user-attachments/assets/fc9e41de-82fb-4064-9f5d-8e981c3706ac" />
- Screenshot of admin panel access
<img width="1028" height="325" alt="image" src="https://github.com/user-attachments/assets/ca1813d2-0420-4f92-be68-1323fc2ae92d" />

- Screenshot of successful deletion
<img width="1021" height="310" alt="image" src="https://github.com/user-attachments/assets/242340f0-b118-471d-818d-e14c6884f52b" />

- Screenshot of lab completion
<img width="1346" height="592" alt="image" src="https://github.com/user-attachments/assets/5ad1905e-d0a5-4e05-bdfe-cc82634262ef" />


## Tools Used
- Burp Suite (Proxy + Repeater)
- Browser

## Key Learning
- Blacklist-based filtering is ineffective against SSRF.
- URL encoding can bypass input validation.
- Alternate IP representations can evade filters.
- Multiple bypass techniques often need to be combined.
