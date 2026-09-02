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
<img width="1375" height="591" alt="image" src="https://github.com/user-attachments/assets/9f3395c2-d923-4a42-8a02-f74ec26354d0" />

Use the above ip address to access the apache webserver of Metasploitable2 from kali/parrot linux. In Kali Linux use the ip address in a web browser.
##  OUTPUT
<img width="1622" height="876" alt="image" src="https://github.com/user-attachments/assets/bb618120-40d6-4fa1-83c4-58e512fbd56b" />


Select Multidae from the menu listed as shown above. The page is displayed as below:
##  OUTPUT

<img width="1482" height="1016" alt="image" src="https://github.com/user-attachments/assets/1c897ad6-7ecf-4b57-9224-fc28c4a16ba6" />


Click on the menu Login/Register and register for an account
##  OUTPUT
<img width="1482" height="871" alt="image" src="https://github.com/user-attachments/assets/b30feea8-089b-4e8d-976f-008a83cd1780" />



Click on the link “Please register here”
##  OUTPUT

<img width="1476" height="902" alt="image" src="https://github.com/user-attachments/assets/0efb23d9-074e-41b6-8a90-7dc4445ee8db" />


Click on “Create Account” to display the following page:
##  OUTPUT
<img width="1330" height="820" alt="image" src="https://github.com/user-attachments/assets/c4121dac-1d46-4178-810a-1afbdfcc5fed" />


The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

<img width="837" height="522" alt="image" src="https://github.com/user-attachments/assets/9ce81925-cf1a-4f53-82ac-b6fb767f62cc" />







If error faced in registration follow the following steps in metasploitable 2:


This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc
Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]:
cd /
sudo nano /var/www/mutillidae/config.inc
Type msfadmin when prompted for the root password. 


Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure
##  OUTPUT
<img width="1475" height="832" alt="image" src="https://github.com/user-attachments/assets/42775ab8-b847-41da-88d3-5c6c675be42c" />




Save and exit the config.inc
Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file
Restart the Apache server
To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM.
sudo /etc/init.d/apache2 reload
##  OUTPUT
<img width="1303" height="132" alt="image" src="https://github.com/user-attachments/assets/d3bb3565-abee-4747-8ed8-01b7a202fecc" />




# Reset Mutillidae database
Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.
##  OUTPUT

<img width="1356" height="831" alt="image" src="https://github.com/user-attachments/assets/85998ae3-a0fb-4593-8fc8-d88bf15e9761" />




# Test the new configuration
Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

 The Mutillidae database error no longer appears 
## OUTPUT
<img width="1373" height="893" alt="image" src="https://github.com/user-attachments/assets/9da33bfc-122d-42fc-a4cf-3dfa54f77849" />



Now after logging out you will see the login page. In the login page give ganesh’ # (myusername). You can see the page now enters into the administrator page as before when giving the password.
## OUTPUT

<img width="1377" height="902" alt="image" src="https://github.com/user-attachments/assets/ec200896-7280-4ac9-b1de-5594000bedf4" />

Click the login button and you will see it enter into the administrator page.
## OUTPUT
<img width="1002" height="621" alt="image" src="https://github.com/user-attachments/assets/875c5fdd-5470-4f7c-9935-42859fcc3f18" />



## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:
##  OUTPUT
<img width="1128" height="697" alt="image" src="https://github.com/user-attachments/assets/4012b75e-34be-4bcb-8411-2d910385139e" />



From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
##  OUTPUT
<img width="1215" height="772" alt="image" src="https://github.com/user-attachments/assets/a2b11077-a33c-47eb-a819-863d4251e3b5" />



Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:
##  OUTPUT
<img width="1170" height="742" alt="image" src="https://github.com/user-attachments/assets/8b0d9665-e183-4859-8d48-4ca1d131b003" />




After adding the order by 6 into the existing url , the following error statement will be obtained:
##  OUTPUT
<img width="1058" height="642" alt="image" src="https://github.com/user-attachments/assets/6a689fc4-ab88-47ac-9ad5-8350edd5920e" />




When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
#OUTPUT
<img width="1465" height="915" alt="image" src="https://github.com/user-attachments/assets/3b7e66f1-8084-4e21-ae35-e5cb1dad99a3" />




 As it is having 5 columns the query worked fine and it provides the correct result
##  OUTPUT

<img width="1278" height="777" alt="image" src="https://github.com/user-attachments/assets/ea3b056e-4f03-4d8d-98a1-e0eb0cd219b2" />



Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).
##  OUTPUT

<img width="1227" height="767" alt="image" src="https://github.com/user-attachments/assets/b8dc656a-4e05-4512-bc1e-4f96ddce039c" />





## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
