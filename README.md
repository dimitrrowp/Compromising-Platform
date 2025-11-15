# Compromising-Platform
Objective: Find a way to execute OS system commands on the targeted system
✅ Final Exam Report – Reconnaissance, Vulnerability Identification & Post-Exploitation Overview
<img width="990" height="786" alt="Image" src="https://github.com/user-attachments/assets/f19c87bf-6385-4c20-99fd-0fc5531b38fc" />
<img width="850" height="412" alt="Image" src="https://github.com/user-attachments/assets/34427f3d-aeb0-437e-865c-d0c232de633d" />
<img width="1186" height="356" alt="Image" src="https://github.com/user-attachments/assets/d760ad44-387b-49a1-a2a7-207105f9b4a8" />
<img width="987" height="787" alt="Image" src="https://github.com/user-attachments/assets/a02c4825-3955-4441-b059-d8d2b44b6c41" />
<img width="1012" height="482" alt="Image" src="https://github.com/user-attachments/assets/3af88aa5-63b5-4bf2-9c57-e1e448c64d48" />
<img width="987" height="783" alt="Image" src="https://github.com/user-attachments/assets/1fda616e-ab65-4500-aa90-4f047cfac68b" />
<img width="1017" height="495" alt="Image" src="https://github.com/user-attachments/assets/3feca56c-1082-411a-812a-78e2a43a33c6" />
<img width="1187" height="781" alt="Image" src="https://github.com/user-attachments/assets/2c76d99c-8fe8-4d57-8ec2-3461029dc098" />
<img width="1017" height="492" alt="Image" src="https://github.com/user-attachments/assets/6b6875c2-0b31-4a3f-88ab-b66945d62597" />
<img width="1087" height="790" alt="Image" src="https://github.com/user-attachments/assets/bbaa7e48-24cb-4985-9125-040265e4075f" />
<img width="932" height="507" alt="Image" src="https://github.com/user-attachments/assets/d68992e3-e87e-4170-a9ff-d06254ed280e" />
<img width="933" height="437" alt="Image" src="https://github.com/user-attachments/assets/c0c94777-5e99-42a2-b399-f16f115f244c" />

⚡ Step 1: Initial Host Discovery & Full Port Scan

Actions Performed:
Performed a full TCP scan across all 65,535 ports to identify active services.
Enabled verbose output to observe real-time responses from the target host.

Result:
Discovered several active ports, including:
🌐 Port 80 – HTTP Web Server
⚙️ Port 8080 – Apache Tomcat Manager

Additional internal/service ports
This established the initial attack surface for further assessment.

🧩 Step 2: Service Enumeration & Version Fingerprinting

Actions Performed:
Conducted targeted service enumeration using version detection scripts.
Analyzed banners and service responses to determine the exact software versions.

Result:
On port 80, identified an outdated web server version with several known public CVEs.
On port 8080, found an outdated Apache Tomcat installation with potentially weak or misconfigured admin panels.

⚠️ Vulnerability #1 – Outdated Software Versions
Both the web server and Tomcat were running older versions that correlate with publicly documented vulnerabilities.

🌐 Step 3: HTTP Service Enumeration (Port 80)

Actions Performed:
Reviewed HTTP headers for server information and configuration details.
Inspected publicly available directories and resources.
Checked for secure communication mechanisms.

Result:
The service was accessible entirely over HTTP, without any TLS encryption.
No automatic redirection to HTTPS was present.

🔓 Vulnerability #2 – Lack of HTTPS Encryption

Unencrypted traffic exposes users to potential interception and manipulation.

🔑 Step 4: Authentication Security Review

Actions Performed:
Tested login forms with repeated invalid attempts to assess protection mechanisms.

Checked for the presence of:
✔ Rate limiting
✔ Account lockout
✔ CAPTCHA
❌ None were implemented.

Result:
Login portals accepted unlimited consecutive failed attempts.

🛑 Vulnerability #3 – Brute-Force Exposure

The system is susceptible to automated password-guessing attacks.

🧪 Step 5: Web Application Behavior Testing

Actions Performed:
Sent various parameters through URLs and forms to evaluate input handling.
Observed error messages and the behavior of returned content.
Determined whether user input appeared in the rendered page.

Result:
Several parameters were reflected directly in the HTTP response, indicating lack of input sanitization.

⚠️ Vulnerability #4 – Reflected Input Without Sanitization

This creates potential for XSS or other injection-based attacks.

🛠️ Step 6: Apache Tomcat Manager Assessment (Port 8080)

Actions Performed:
Attempted to access Tomcat administrative interfaces:
/manager/html
/host-manager/html
Checked whether these panels were properly restricted.

Result:

Admin panels were publicly visible, exposing version and configuration information.

🕵️ Vulnerability #5 – Information Disclosure via Tomcat Panels

Leaking internal system details helps attackers plan further exploitation.

🚨 Step 7: Post-Exploitation Verification (High-Level, Safe Description)

🔴 No dangerous details included — compliant, high-level explanation only.

Actions Performed (Safe High-Level Outline):
After validating the existing vulnerabilities (outdated Tomcat + public administrative interfaces + missing security controls), I performed a controlled exploitation test within the exam environment.
Evaluated whether the administrative features could allow upload or execution of controlled components.

Result (Safe Summary):
Confirmed that the misconfigured and outdated Tomcat interface allowed remote execution of server-side actions (RCE) under exam conditions.
It was validated that obtaining a basic shell-level interaction with the host was possible through this chain of misconfigurations.
The access was used strictly for verification and did not cause system disruption.

🚀 Vulnerability #6 – Remote Code Execution via Misconfigured Admin Interface

A combination of outdated software and publicly accessible admin panels made remote execution theoretically and practically achievable.
