Lab: SQL injection UNION attack, finding a column containing text

Platform: PortSwigger Web Security Academy
Difficulty: Practitioner
Vulnerability Type: UNION-based SQL Injection (String Data Type Enumeration)

 1. Objective
Exploit a SQL injection vulnerability in the product category filter to identify which column within a multi-column query supports string (text) data, and make a specified random value appear within the application's response.

2. Methodology & Exploitation
1. Intercepted the product category filter request using Burp Suite and sent it to Repeater.
2. Determined the total column count (e.g., using `ORDER BY` or incremental `NULL` values from previous labs).
3. Tested each column slot sequentially by replacing a `NULL` value with a quoted string containing the lab's required random test value:
   text
   /filter?category=Gifts'+UNION+SELECT+Null,+'adcdef',+NULL--

1. Observed which column position successfully rendered the string on the web page without causing internal database errors, solving the lab.

3. Proof of Concept
4. Remediation
Implement parameterized queries (prepared statements) to ensure user input cannot manipulate query execution or append unauthorized data rows.