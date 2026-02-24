# PortSwigger Lab: SQL Injection (Login Bypass)

## Objective
To exploit a SQL injection vulnerability in the login functionality and gain access as the `administrator` user.

## Lab Description
The application contains a login form vulnerable to SQL injection. User input is directly used in a SQL query without proper sanitisation.

---

## Exploitation

### 1. Initial Observation
The application contains a standard login page with username and password fields.

This suggested that the backend query was something like:

```
SELECT * FROM users WHERE username = '' AND password = ''
```

---

### 2. Initial Injection Attempt
I initially tried injecting the following payload into the username field:

```
Administrator'--
```

However, the application required both fields to be filled. Submitting without a password was not allowed, so this attempt failed.

---

### 3. Adjusting the Approach
Since the password field was mandatory, I entered a valid username (`Administrator`) and focused on injecting into the password field.

I decided to use a logical condition that always evaluates to true using an `OR` statement.

---

### 4. Exploitation
I used the following inputs:

Username:
```
Administrator
```

Password:
```
admin' OR 0=0--
```

---

### 5. Explanation

- `'` closes the original string in the SQL query  
- `OR 1=1` makes the condition always true  
- `--` comments out the rest of the query  

This effectively bypasses the password check.

---

### 6. Result
The login was successful, and I gained access as the administrator user.

---

## Impact
An attacker can bypass authentication and gain unauthorised access to sensitive accounts, including administrative access.

---

## Key Learning

- Login forms are common targets for SQL injection attacks  
- Unsanitized user input can lead to authentication bypass  
- Logical conditions like `OR 0=0` can force queries to return valid results
