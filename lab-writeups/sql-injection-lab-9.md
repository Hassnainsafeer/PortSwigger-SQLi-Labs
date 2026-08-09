Lab: SQL injection UNION attack, retrieving data from other tables

Platform: PortSwigger Web Security Academy
Difficulty: Practitioner
Vulnerability Type: UNION-based SQL Injection (Cross-Table Data Retrieval)

 1. Objective
Exploit a SQL injection vulnerability in the product category filter to retrieve all usernames and passwords from a separate database table (`users`), then use the obtained credentials to log in as the `administrator`.

 2. Methodology & Exploitation
1. Intercepted the product category filter request using Burp Suite and sent it to Repeater.
2. Determined the column count and identified string-compatible columns using techniques from previous labs.
3. Constructed a `UNION SELECT` payload targeting the custom `users` table to extract concatenated or mapped user credentials:
   text
   /filter?category=Gifts'+UNION+SELECT+username,+password+FROM+users--

1. Examined the application's response to capture the credentials for all registered users, including the administrator.

2. Authenticated successfully on the login page using the extracted administrator password to solve the lab.

3. Proof of Concept
4. Remediation
Implement parameterized queries (prepared statements) to ensure user input cannot modify query logic or execute unauthorized UNION operations across different database tables.