Lab: SQL injection UNION attack, determining the number of columns returned by the query

Platform: PortSwigger Web Security Academy
Difficulty: Practitioner
Vulnerability Type: UNION-based SQL Injection (Column Enumeration)

1. Objective
Determine the exact number of columns returned by the original database query in the product category filter by performing a SQL injection UNION attack that appends an additional row containing `NULL` values.

2. Methodology & Exploitation
1. Intercepted the product category filter request using **Burp Suite** and sent it to Repeater.
2. Tested column counts iteratively using the `ORDER BY` technique or by appending `UNION SELECT NULL` values until the application stopped throwing internal errors.
3. Successfully structured a `UNION` payload containing the correct number of `NULL` columns:
   text
   /filter?category=Gifts'+UNION+SELECT+NULL,++NULL--

1. Verified that the application successfully returned the extra row, confirming the column count and solving the lab.

3. Proof of Concept
4. Remediation
Implement parameterized queries (prepared statements) to prevent user-supplied input from modifying structural query execution.