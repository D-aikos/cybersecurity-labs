## Objective:
To exploit a SQL injection vulnerability in the login functionality and gain access as the administrator user.
Lab Link: https://portswigger.net/web-security/sql-injection/lab-login-bypass

## Initial Analysis
The application contains a standard login page with username and password fields.
Since authentication systems typically validate credentials against a database, it is likely that both inputs are incorporated into a backend SQL query. The objective of the lab is to manipulate this query and bypass authentication.

## Exploitation
#### First Attempt
Username:
`Administrator'--`
This was my initial attempt to comment out the password check entirely.
However, the application required both the username and password fields to be populated before the request could be submitted, so this approach was unsuccessful.

#### Final Payload
Username:
`Administrator`
Password:
`admin' OR 0=0--`
This payload successfully authenticated me as the administrator user.
The injected quote closes the original string, `OR 0=0` creates a condition that always evaluates to true, and `--` comments out the remainder of the query.

#### Result
The login was successful, and I gained access as the administrator account, completing the lab.

## Conclusion
The login functionality was vulnerable to SQL injection and allowed authentication to be bypassed entirely. By manipulating the SQL query, it was possible to gain access to the administrator account without knowing the correct password.

## Key Learning
Authentication forms are common targets for SQL injection attacks. If user input is incorporated into database queries without proper sanitisation or parameterisation, attackers may be able to bypass authentication and gain unauthorised access to sensitive accounts.
