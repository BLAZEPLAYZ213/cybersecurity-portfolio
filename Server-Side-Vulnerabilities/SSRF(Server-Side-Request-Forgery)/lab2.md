# SSRF - Basic SSRF Against Internal Network

## Overview
This lab demonstrates how a Server-Side Request Forgery (SSRF) vulnerability can be used to scan internal networks and access hidden services.

## Vulnerability
The application fetches data from a user-supplied URL, allowing attackers to make the server send requests to internal IP addresses.

## Objective
Scan the internal 192.168.0.X network, locate the admin interface, and delete the user "carlos".

## Reconnaissance
Identified a stock check feature that sends a request with a parameter:

stockApi=http://...

This parameter is used by the server to fetch data.

## Exploitation

### Step 1: Internal Network Scanning
- Used SSRF to send requests to internal IP range:
  http://192.168.0.X:8080/admin
- Automated scanning using Burp Suite Intruder.

### Step 2: Identify Live Host
- Observed different responses:
  - 400 → invalid requests
  - 404 → valid host but incorrect endpoint
- Identified a live internal IP based on response differences.

### Step 3: Access Admin Panel
- Corrected the request path and accessed:
  http://192.168.0.X:8080/admin
- Received admin panel response.

### Step 4: Extract Endpoint
- Analyzed HTML response.
- Found delete functionality:
  /admin/delete?username=carlos

### Step 5: Execute Action via SSRF
- Modified request:
  stockApi=http://192.168.0.X:8080/admin/delete?username=carlos
- Sent request.

## Result
Successfully scanned internal network, accessed admin panel, and deleted the user "carlos".

## Evidence
- Screenshot of SSRF scanning (Intruder results)
<img width="1336" height="579" alt="image" src="https://github.com/user-attachments/assets/31612145-03a9-4ad7-9548-ba30df8609ec" />
- Screenshot of response differences (400 vs 404 vs valid)
<img width="1316" height="562" alt="image" src="https://github.com/user-attachments/assets/e53d4e39-294f-4dbe-b068-d8768ac11750" />
- Screenshot of admin panel response
<img width="1334" height="571" alt="image" src="https://github.com/user-attachments/assets/02fced57-f0b4-47ff-a029-f4f2d2878da3" />
- Screenshot of delete request
<img width="1330" height="569" alt="image" src="https://github.com/user-attachments/assets/8ddbe7ee-0bda-4226-b25d-e8676d2d0ee0" />

- Screenshot of lab completion
<img width="1343" height="594" alt="image" src="https://github.com/user-attachments/assets/1ab80057-9016-47d3-acd4-10971613bf28" />


## Tools Used
- Burp Suite (Intruder + Repeater)
- Browser

## Key Learning
- SSRF can be used for internal network scanning.
- Response analysis (status codes, length) is crucial.
- Internal services are often exposed on private IP ranges.
- SSRF can lead to full compromise of internal systems.
