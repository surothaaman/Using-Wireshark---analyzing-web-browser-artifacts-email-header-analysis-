# Ex 10 Using-Wireshark---analyzing-web-browser-artifacts-email-header-analysis
## AIM:
To use Wireshark to analyze web browser activities and inspect email headers from captured network traffic.
## Architecture Diagram:
```mermaid
flowchart TD
    A[User System] --> B[Web Browser]
    A --> C[Email Client]
    B --> D[Network Traffic]
    C --> D
    D --> E[Wireshark Capture Engine]
    E --> F[Protocol Decoders HTTP SMTP IMAP POP]
    F --> G[Browser Artifacts URLs Cookies Auth]
    F --> H[Email Headers Source IP Server Timestamps]
    G --> I[Findings and Reports]
    H --> I
```
## DESIGN STEPS:
### Step 1:
- Install Wireshark and ensure correct network adapter selection.
- Enable packet capturing for your active interface (Wi-Fi/Ethernet).

### Step 2:
**Web Browser Artifact Analysis**
- Open a browser and visit websites with login forms (use dummy credentials).
- In Wireshark, filter traffic with:
    - ```http``` for normal HTTP requests
    - ```http.cookie``` for cookies
    - ```http.authbasic``` for basic authentication
- Identify:
    - URLs visited
    - GET/POST requests
    - Cookies & session IDs
    - Credentials (if plaintext HTTP is used)
### Step 3:
- Capture email traffic by sending/receiving emails (dummy mail server or provided PCAP).
- Use filters:
    - ```smtp``` (Simple Mail Transfer Protocol)
    - ```pop``` / ```imap``` (for received mail)
- Inspect email headers:
    - Source IP
    - Mail server hostname
    - Timestamps
    - Possible forged headers
## PROGRAM:
```mermaid
flowchart TD
    A[Start Wireshark Capture] --> B[Generate Traffic: Web Browsing & Emails]
    B --> C[Apply Protocol Filters: HTTP/SMTP/IMAP/POP]
    C --> D[Extract Browser Artifacts: URLs, Cookies, Credentials]
    C --> E[Analyze Email Headers: Source, Server, Metadata]
    D --> F[Save Findings]
    E --> F[Save Findings]
    F --> G[Generate Digital Forensic Report]
```

## A. Capturing Traffic in Wireshark

1. Open Wireshark and start capturing on the active interface (Wi-
Fi/Ethernet).

<img width="1920" height="1080" alt="Screenshot (35)" src="https://github.com/user-attachments/assets/150bb117-f067-467f-822b-a5a0d139ac05" />



2. Perform activities like opening a website or sending an email through a
client (e.g., Gmail via browser or Thunderbird).


<img width="1920" height="1080" alt="Screenshot (34)" src="https://github.com/user-attachments/assets/492de60b-730d-4fcd-a5cf-097a409ee5be" />



4. Stop the capture once done.


## B. Analyzing Web Browser Artifacts
1. Apply filters like: http, tcp.port == 443 (for HTTPS), or dns to isolate
browser traffic.
<img width="1920" height="1080" alt="Screenshot (34)" src="https://github.com/user-attachments/assets/b72305a1-62a8-4beb-99b3-167dd4a94860" />



3. Inspect HTTP GET/POST requests:
o Look for URLs, hostnames, user agents, and cookies in the HTTP
headers.
o Follow TCP Stream to reconstruct page request flow:
▪ Right-click a packet → Follow → TCP Stream.

<img width="1920" height="1080" alt="Screenshot (40)" src="https://github.com/user-attachments/assets/6255e296-9564-4283-9306-ada6f5cf04d1" />



Analyze DNS Queries:
o Filter: dns
o Reveal domains the browser tried to resolve.


<img width="1920" height="1080" alt="Screenshot (40)" src="https://github.com/user-attachments/assets/d00d9592-46d6-42a5-b37c-c543aa3d6f79" />


## C. Email Header Analysis
1. Apply relevant filters:
o For POP3: tcp.port == 110
o For SMTP: tcp.port == 25 or 587
o For IMAP: tcp.port == 143 or 993

<img width="1920" height="1080" alt="Screenshot (42)" src="https://github.com/user-attachments/assets/8a656915-520d-4ab5-8d7c-c57ae6620c16" />



3. Locate email data:
o Look for SMTP packets to see sender/receiver email addresses.
o Use "Follow TCP Stream" to view the full email headers and body if
unencrypted.


![WhatsApp Image 2025-10-04 at 13 45 21_c9b8c9c3](https://github.com/user-attachments/assets/2f083355-3ff6-46d2-ba58-8bf34fdf9376)



5. Extract Email Header Fields:
o Analyze From, To, Subject, Date, Message-ID, and relay servers used
in sending the email.

![WhatsApp Image 2025-10-04 at 13 45 16_4d187906](https://github.com/user-attachments/assets/e851758a-3662-42dd-8df6-6bc017b4dd38)



## OUTPUT:
Captured Web Activity and Email Header Information

## RESULT:
Web browser artifacts and email headers were successfully analyzed using Wireshark.

