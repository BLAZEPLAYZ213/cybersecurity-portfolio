# SSRF - Basic SSRF Against Local Server

## Overview
This lab demonstrates a Server-Side Request Forgery (SSRF) vulnerability that allows an attacker to make the server send requests to internal services.

## Vulnerability
The application fetches stock data from a URL provided by the user. This allows attackers to manipulate the request and access internal resources such as the admin panel.

## Objective
Access the internal admin panel and delete the user "carlos".

## Reconnaissance
Identified a stock check feature that sends a POST request containing a parameter:

stockApi=http://...

This parameter is used by the server to fetch data.

## Exploitation

### Step 1: SSRF to Internal Admin Panel
- Intercepted the request using Burp Suite.
- Modified the parameter:
  stockApi=http://localhost/admin
- Sent the request.
- Received the admin panel response in Burp.

### Step 2: Extract Internal Endpoint
- Analyzed the response HTML.
- Found delete functionality:
  /admin/delete?username=carlos

### Step 3: Trigger Admin Action via SSRF
- Modified request again:
  stockApi=http://localhost/admin/delete?username=carlos
- Sent the request.

## Result
Successfully deleted the user "carlos" by exploiting SSRF vulnerability.

## Evidence
- Screenshot of intercepted request
<img width="1349" height="573" alt="image" src="https://github.com/user-attachments/assets/a134fdff-0626-41a9-9319-369441fdd44e" />

- Screenshot of SSRF response showing admin panel
<img width="498" height="386" alt="image" src="https://github.com/user-attachments/assets/cc984350-be06-4e61-9aaa-b7bfb3e2cb1d" />

- Screenshot of delete request
<img width="513" height="389" alt="image" src="https://github.com/user-attachments/assets/2922115c-f860-4ddc-9171-a09185994010" />

- Screenshot of lab completion
<img width="1355" height="604" alt="image" src="https://github.com/user-attachments/assets/99b83575-cdfe-4e08-a0dd-59ee26dcfc10" />


## Tools Used
- Burp Suite (for intercepting and modifying requests)
- Browser

## Key Learning
- SSRF allows attackers to interact with internal services.
- Internal endpoints often trust localhost requests.
- SSRF can be used not only to read data but also to perform actions.
- Always validate and restrict external URL inputs.
