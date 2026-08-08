Lab: SQL injection attack, listing the database contents on non-Oracle databases

Platform: PortSwigger Web Security Academy
Difficulty: Practitioner
Vulnerability Type: UNION-based SQL Injection (Information Schema Enumeration)

1. Objective
Exploit a SQL injection vulnerability within the product category filter to query database metadata, identify sensitive user tables and columns, extract the administrator's credentials, and log into the application.

2. Methodology & Exploitation
1. Intercepted the product category request using Burp Suite and sent it to Repeater.
2. Determined column count and string compatibility using `UNION SELECT` statements with `NULL` values.
3. Queried the database metadata schema (`information_schema.tables`) to discover the name of the custom user table:
   ```text
   '+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--

1. Queried information_schema.columns to map out the specific column names holding usernames and passwords inside the target table.

2. Extracted the administrator credentials from the dumped records and successfully logged into the application interface.

3. Proof of Concept
4. Remediation
Implement parameterized queries (prepared statements) to prevent user-supplied data from modifying query structures.

Restrict database permissions to prevent application users from querying metadata tables like information_schema