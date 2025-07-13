\# SQL Injection – DVWA (Low Security)

\##  Vulnerability
The application does not sanitize user input in the "User ID" field, allowing attackers to inject SQL commands.

\##  Payload Used

```sql
1' OR '1'='1

\##  Result

All users in the database were returned, showing that the SQL query was vulnerable.

\##  Mitigation

\- Use prepared statements (parameterized queries)
\- Validate and sanitize all user inputs
\- Apply least privilege on database user accounts

\##  Notes

\- DVWA security level: Low
\- Tested on: Kali Linux (local VM), DVWA running via Apache2
