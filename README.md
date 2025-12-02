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

SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 
Identify IP address using ifconfig in Metasploitable2
#OUTPUT
<img width="1264" height="694" alt="Screenshot 2025-12-02 161355" src="https://github.com/user-attachments/assets/bdaf41c8-b85a-4cde-98fb-e3b730875322" />

Use the above ip address to access the apache webserver of Metasploitable2 from kali/parrot linux. In Kali Linux use the ip address in a web browser.
##  OUTPUT
<img width="1280" height="785" alt="Screenshot 2025-12-02 161752" src="https://github.com/user-attachments/assets/8734beef-86af-4c2b-9020-ae9f71ed8667" />


Select Multidae from the menu listed as shown above. The page is displayed as below:
##  OUTPUT
<img width="1270" height="800" alt="Screenshot 2025-12-02 161806" src="https://github.com/user-attachments/assets/a5463084-4761-432a-a730-df0e6179dc80" />



Click on the menu Login/Register and register for an account
##  OUTPUT

<img width="1304" height="799" alt="Screenshot 2025-12-02 161826" src="https://github.com/user-attachments/assets/0440579a-d342-4c08-bd46-c711df4ce0f0" />


Click on the link “Please register here”
##  OUTPUT

<img width="1285" height="779" alt="Screenshot 2025-12-02 161901" src="https://github.com/user-attachments/assets/a5d7888f-c91d-44b7-809d-5f57e608bc56" />


Click on “Create Account” to display the following page:
##  OUTPUT
<img width="1285" height="779" alt="Screenshot 2025-12-02 161901" src="https://github.com/user-attachments/assets/2583cde1-d029-4865-b869-61ac94a28c2a" />


The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:


($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
 Click “Login”. The logged in page will show as below:
##  OUTPUT

<img width="1278" height="822" alt="Screenshot 2025-12-02 161924" src="https://github.com/user-attachments/assets/2ba2ff0c-3b36-4809-bf49-34734bb965d1" />


If error faced in registration follow the following steps in metasploitable 2:


This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc
Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]:
cd /
sudo nano /var/www/mutillidae/config.inc
Type msfadmin when prompted for the root password. 
Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure  below:
##  OUTPUT

<img width="680" height="371" alt="image" src="https://github.com/user-attachments/assets/bf1b02bd-1a6f-40c4-ac06-11e5c1ca3789" />

Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure
##  OUTPUT

<img width="667" height="374" alt="image" src="https://github.com/user-attachments/assets/8a356e11-ede3-4402-8e1a-b58e2b26eba2" />



Save and exit the config.inc
Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file
Restart the Apache server
To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM.
sudo /etc/init.d/apache2 reload
##  OUTPUT


<img width="671" height="74" alt="image" src="https://github.com/user-attachments/assets/f3bdb28f-4bfe-4dc6-b369-767dbc0e6953" />


# Reset Mutillidae database
Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.
##  OUTPUT





# Test the new configuration
Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

 The Mutillidae database error no longer appears 
#OUTPUT

<img width="1272" height="803" alt="Screenshot 2025-12-02 162104" src="https://github.com/user-attachments/assets/608ba2fc-bec6-4cd7-84eb-7fba11887969" />


Now after logging out you will see the login page. In the login page give ganesh’ # (myusername). You can see the page now enters into the administrator page as before when giving the password.
#OUTPUT
<img width="1275" height="795" alt="Screenshot 2025-12-02 162201" src="https://github.com/user-attachments/assets/0a32782a-c4bc-44f9-9155-89af5a72d2c8" />


Click the login button and you will see it enter into the administrator page.
#OUTPUT

<img width="1272" height="803" alt="Screenshot 2025-12-02 162104" src="https://github.com/user-attachments/assets/3d8b6502-822a-4933-9c48-ce155749896b" />


## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:
##  OUTPUT



From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
##  OUTPUT



Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:
##  OUTPUT

<img width="1277" height="798" alt="image" src="https://github.com/user-attachments/assets/f419a0b5-4a21-4f16-94ce-9764fd9a5197" />



After adding the order by 6 into the existing url , the following error statement will be obtained:
##  OUTPUT


<img width="1279" height="797" alt="image" src="https://github.com/user-attachments/assets/8b1a9672-0c50-469b-ada5-713dc163744e" />


When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
#OUTPUT



 As it is having 5 columns the query worked fine and it provides the correct result
##  OUTPUT


<img width="1273" height="800" alt="image" src="https://github.com/user-attachments/assets/647ebe1c-58fb-4fb8-bfea-fd67d02167e8" />


Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).
##  OUTPUT
<img width="1275" height="772" alt="image" src="https://github.com/user-attachments/assets/d720739d-283a-4343-afc5-de9a50072b0c" />



As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
##  OUTPUT


<img width="1264" height="753" alt="image" src="https://github.com/user-attachments/assets/e4f24ceb-1a1d-4400-a79f-cd72e6137660" />




Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
##  OUTPUT
<img width="1267" height="806" alt="image" src="https://github.com/user-attachments/assets/2a684c32-8f4e-4ec1-9115-8f9aa43a9fa4" />



The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
##  OUTPUT

<img width="1266" height="794" alt="image" src="https://github.com/user-attachments/assets/3b7f9f37-0731-4cdc-a8f6-a0488fa4c004" />



The url once executed will  retrieve table names from the “owasp 10” database.
##Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
##  OUTPUT

<img width="1275" height="790" alt="image" src="https://github.com/user-attachments/assets/335e58dc-6a04-43a6-b390-4d3f77fc9cc3" />


The column names of the accounts is displayed below for the following url:


Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).
##  OUTPUT

<img width="1271" height="799" alt="image" src="https://github.com/user-attachments/assets/c40fe7f9-955f-459a-bff8-55128e64630d" />


## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).


##  OUTPUT
<img width="1271" height="752" alt="image" src="https://github.com/user-attachments/assets/52483f00-9de5-4995-bee8-13915e299024" />


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
