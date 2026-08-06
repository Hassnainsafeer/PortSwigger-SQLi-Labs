Lab: SQL injection vulnerability allowing login bypass

Platform:PortSwigger Web Security Academy
Difficulty:Apprentice
Vulnerability Type: Authentication Bypass via SQL Injection (CWE-89)

1. Objective
Log into the application as the `administrator` user without knowing their password by exploiting a SQL injection vulnerability in the login form.

2. Methodology & Exploitation
1. Navigated to the application's login page (/login) and captured the authentication request using Burp Suite.
2. Noticed the `POST` request body contained the parameters:
   text
   username=...&password=...
Modified the username parameter to target the administrator account and injected a SQL comment payload into the password parameter to comment out the rest of the backend query check:

Plaintext
username=administrator&password=--
Forwarded the modified request to the server. The backend query evaluated to true for the administrator account, completely bypassing password verification.

3. Proof of Concept / Results
Here is the captured request modification in Burp Suite and the successfully solved lab state:

4. Remediation
Parameterized Queries: Use prepared statements (parameterized queries) so that user input is treated strictly as data, never as executable query code.

Secure Authentication Logic: Ensure authentication checks validate password hashes securely through proper framework APIs rather than constructing dynamic SQL statements with concatenated user input.