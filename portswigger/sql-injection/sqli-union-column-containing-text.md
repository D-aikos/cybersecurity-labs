## Objective:
To solve the lab, perform a SQL injection UNION attack that returns an additional row containing the value provided. 
This technique helps you determine which columns are compatible with string data.

## Initial Analysis
As the description states, it appears that the website categorises its products based on category, and this category is visible in the URL as shown below:
`web-security-academy.net/filter?category=Gifts`
To solve this lab, I will split it into 2 sections
	1. Finding the Number of Columns in the Original Query
	2. Finding a column compatible with string data
  
## Exploitation
I completed the first part of this lab by using the same methodology used in the  `sqli-union-column-count.md` lab. Refer to that document for further details.
Now, to solve the second part of the lab, I will inject a series of payloads similar to 
`' UNION SELECT NULL, NULL, NULL --`. 
To identify which column is compatible with string data, I replaced each `NULL` value one at a time with the string provided by the lab (`'bvlUaF'`) and observed the application's response.
#### First Payload
	web-security-academy.net/filter?category=Gifts' UNION SELECT 'bvlUaF', NULL, NULL --
	This generated an error, indicating that the first column is not compatible with string data.
#### Second Payload
	web-security-academy.net/filter?category=Gifts' UNION SELECT NULL, 'bvlUaF', NULL --
	This executed successfully without generating an error and displayed the string within the application's response.
  
## Conclusion
From the exploitation, we can conclude that the original query returns three columns and that the second column is compatible with string data.

## Key Learning
UNION-based SQL injection requires both the number of columns and their data types to be compatible with the original query.
By replacing `NULL` values with a string one column at a time, it is possible to identify which columns can be used to display text data during later stages of exploitation.
