Lab: SQL injection attack, querying the database type and version on Oracle

Platform: PortSwigger Web Security Academy
Difficulty: Practitioner
Vulnerability Type: SQL Injection / UNION Attack (Oracle DB)

1. Objective
Retrieve the database version string from an Oracle database by exploiting a SQL injection vulnerability within the product category filter.

2. Methodology & Exploitation
1. Intercepted the product category filter request using **Burp Suite**.
2. Determined the number of columns returned by the original query using the `ORDER BY` clause.
3. Tested data types using `NULL` values to find columns compatible with string data.
4. Constructed an Oracle-specific `UNION SELECT` payload targeting the built-in `v$version` table and the mandatory null table:
   text
   '+UNION+SELECT+banner,+NULL+FROM+v$version--
3. Proof of Concept
4. Remediation
Implement parameterized queries (prepared statements) to prevent user-supplied input from altering SQL query logic.

Ensure strict input validation and type casting on database parameters.