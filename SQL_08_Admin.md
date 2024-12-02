# SQL REVISION SHEET 08
## ADMIN
<br>

________
### 01.00 ACCESS CONTROL
__________

to control different users abilities to perform tasks (enable and disable) we use ```DATA CONTROL LANGUAGE``` or ```DCL```

<br>

#### 01.01 PRIVILEGES

There are different kind of privileges in a database system

the four basic ones for computer files are :
* Read (R)
* Write (W)
* Delete (D)
* Execute (X) *does not apply to data entities*


and there is two types of privileges

* System privileges
* Object privileges

| PRIVILEGE | | |
|-----------|-|-|
| SYSTEM | ALTER <br> DROP <br> CREATE <br> |
| OBJECT | SELECT <br> INSERT <br> DELETE | UPDATE <br> EXECUTE <br> REFERENCES | 

<br>

#### 01.02 SYSTEM ADMIN

the default admin of MS Access is called ```SYSTEM ADMINISTRATOR``` or ```SA``` : it has all the rights of the database (it owns it)

the ```SA``` account is very dangerous : it can overwrite or delete anything in the DBMS

<br>

#### 01.02 PUBLIC

the keyword ```PUBLIC``` means all the users of the databse (if everyone can see a table, instead of applying the permission to each group, you grant it to ```PUBLIC```)

<br>
<br>

________
### 02.00 LOGIN
__________

to create a new user, we need to create a login, then the user

the ```LOGIN``` is for the ```SERVER```
the ```USER``` is for the ```DATABASE```


```SQL
CREATE LOGIN login01 WITH PASSWORD = 'password01';

CREATE USER user01 FOR LOGIN login01;
```
<br>

to display the login and user name we can use : 
```SQL
SELECT SUSER_NAME(), USER_NAME();
```

<br>
to display all the users in the database :

```SQL
SELECT * FROM sys.database_principals
    WHERE TYPE = 'S';
```

<br>
<br>

________
### 03.00 APPLYING PERMISSIONS
__________

in databases there is 3 ways to apply permissions :
* ```GRANT``` 
* ```DENY```
* ```REVOKE```

**the ```DENY``` will always override the ```GRANT``` even in inheritance**

we can give permissions on 
* tables
* specific columns
* views
* procedures *execute*


<br>

#### 03.01 GRANT

this command gives a privilege

it can be a combination of ```SELECT```, ```INSERT```, ```UPDATE```, ```DELETE```, ```REFERENCES```, ```ALTER```

if you want to give all the permissions you can also write ```ALL```

```SQL
GRANT privilege01, privilege02 
    ON object01
    TO user01;
```

<br>
granting the permission to a specific column

```SQL
GRANT privilege01, privilege02 (column01, column02)
    ON object01
    TO user01;
```

<br>

if we also want the user to be able to give this permission to other users we can add the ```WITH GRANT OPTION```

```SQL
GRANT privilege01, privilege02 
    ON object01 
    TO PUBLIC
    WITH GRANT OPTION;
```

<br>

#### 03.02 DENY

<br>

#### 03.03 REVOKE

it cancels a ```GRANT``` or a ```DENY``` permission

```SQL
REVOKE privilege01, privilege02
    ON object01
    FROM user01;
```
```SQL
REVOKE ALL PRIVILEGES
    ON object01
    FROM PUBLIC;
```

<br>
<br>

________
### 04.00 ROLES
__________

```ROLES``` are to simplify the process of granting and managing permissions to different users and groups

```SQL
CREATE ROLE role01 AUTHORIZATION owner01;
```
<br>
to add a user to the role 

```SQL
ALTER ROLE role01 ADD MEMBER user01;
```

<br>

#### 04.01 SYSTEM ROLES

MS Access has built-in roles

https://learn.microsoft.com/en-us/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-ver16

| ROLE | DESC |
|------|------|
| db_owner | perform all configuration and maintenance activities on the database, and can also ```DROP``` the database in SQL Server <br> (In SQL Database and Azure Synapse, some maintenance activities require server-level permissions and can't be performed by db_owners) |
| db_securityadmin | modify role membership for custom roles only and manage permissions. Members of this role can potentially elevate their privileges and their actions should be monitored |
| db_accessadmin | add or remove access to the database for Windows logins, Windows groups, and SQL Server logins |
| db_backupoperator | back up the database |
| db_ddladmin | run any Data Definition Language (DDL) command in a database. Members of this role can potentially elevate their privileges by manipulating code that might get executed under high privileges and their actions should be monitored |
| db_datawriter | add, delete, or change data in all user tables. In most use cases, this role is combined with **db_datareader** membership to allow reading the data that is to be modified |
| db_datareader | read all data from all user tables and views. User objects can exist in any schema except ```sys``` and ```INFORMATION_SCHEMA``` |
| db_denydatawriter | can't add, modify, or delete any data in the user tables within a database |
| db_denydatareader | can't read any data from the user tables and views within a database |

