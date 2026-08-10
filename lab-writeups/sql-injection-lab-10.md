Lab: SQL injection UNION attack, retrieving multiple values in a single column

Platform: PortSwigger Web Security Academy
Difficulty: Practitioner
Vulnerability Type: UNION-based SQL Injection (String Concatenation / Multiple Value Extraction)

1. Objective
Exploit a SQL injection vulnerability in an application where the query only returns a **single column** of text, requiring the concatenation of multiple values (usernames and passwords from the `users` table) into that one column to successfully extract the `administrator` credentials and log in.

2. Methodology & Exploitation
1. Intercepted the product category filter request using Burp Suite and sent it to Repeater.
2. Determined that the application's query only allows the retrieval of data through a single text-compatible column.
3. Utilized database-specific string concatenation syntax (e.g., using `||` or `CONCAT()`) to merge the `username` and `password` fields together with a separator like `~`:
   text
   /filter?category=Gifts'+UNION+SELECT+username+||+'+%27+|+password,+NULL+FROM+users--

1. Examined the application response to view the combined strings, extracted the administrator credentials, and logged into the application to solve the lab.

3. Proof of Concept
4. Remediation
Implement parameterized queries (prepared statements) to prevent structural query tampering.

Enforce strict input handling and type constraints on backend data processing.