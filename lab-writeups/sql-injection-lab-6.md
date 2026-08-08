Lab: SQL injection attack, listing the database contents on Oracle

Platform: PortSwigger Web Security Academy
Difficulty: Practitioner
Vulnerability Type: UNION-based SQL Injection (Oracle Database Metadata Enumeration)

 1. Objective
Exploit a SQL injection vulnerability within the product category filter on an Oracle database to query metadata tables, discover sensitive user tables and columns, extract administrator credentials, and log into the application.

 2. Methodology & Exploitation
1. Intercepted the product category filter request using Burp Suite.
2. Determined column counts and tested data types using `UNION SELECT` statements compatible with Oracle, appending the mandatory `FROM dual` table clause.
3. Queried Oracle's metadata view (`all_tables`) to identify custom application tables:
   text
   '+UNION+SELECT+table_name,+NULL+FROM+all_tables--

1. Queried all_tab_columns to find the exact column names holding usernames and passwords inside the targeted users table.

2. Extracted the administrator credentials using the structured payload and successfully signed into the application interface to solve the lab.

3. Proof of Concept
4. Remediation
1. Use parameterized queries (prepared statements) to isolate user-supplied input from executing SQL statement logic.

2. Enforce strict database access controls and least-privilege permissions to prevent application queries from accessing system metadata views.