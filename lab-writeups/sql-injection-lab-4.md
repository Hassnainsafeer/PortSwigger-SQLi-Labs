Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft

Platform: PortSwigger Web Security Academy
Difficulty: Practitioner
Vulnerability Type: UNION-based SQL Injection (MySQL / Microsoft SQL Server)

1. Objective
Extract and display the database version string from a MySQL or Microsoft SQL Server database by exploiting a SQL injection vulnerability in the product category filter.

2. Methodology & Exploitation
1. Intercepted the product category filter request in **Burp Suite**.
2. Determined the number of columns returned by the original query using the `ORDER BY` technique.
3. Tested column compatibility using `NULL` values to find which column accepts text data.
4. Crafted a clean `UNION SELECT` payload utilizing the database-specific version function/variable `@@version`:
   text
   filter?category=Lifestyle'%20UNION%20SELECT%20@@version,NULL%23