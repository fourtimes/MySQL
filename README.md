 # MySQL_Docs

### What is MySQL?
```bash
- MySQL is currently the most popular database management system software used for managing the relational database. 
- MySQL follows the working of a client/server architecture.
- MySQL supports many Operating Systems like Windows, Linux.
```
_MySQL Installation_
  
```bash
sudo apt update
sudo apt install mysql-server -y
```
_Secure installation_

```bash
sudo mysql_secure_installtion
```

_MySQL login_
```bash
sudo mysql -u root -p
```
   
_How to exit the database_

```bash
exit (or) \q
```
    


_Create a MySQL New User_

![image](https://user-images.githubusercontent.com/91359308/164618635-021aae64-c33b-4996-bdc0-df0b4e04e03d.png)

_To grant all privileges to MySQL User on all databases_

![image](https://user-images.githubusercontent.com/91359308/164618698-e43771d2-1ed5-4471-9a3e-327452a9aecf.png)

_To grant insert privileges to a MySQL user_

![image](https://user-images.githubusercontent.com/91359308/164619089-96d53733-976d-4be5-9b3b-143ab81622a0.png)

_To show all the privileges in a specified user_

![image](https://user-images.githubusercontent.com/91359308/164619150-fa0ccbad-0241-4c82-b1fd-357a572f5f6a.png)

_List out the details of users_

![image](https://user-images.githubusercontent.com/91359308/164619600-2d0a46a7-303a-4764-9a51-2ec690af9005.png)



_Create a Database_

![image](https://user-images.githubusercontent.com/98270930/164432767-f103370c-7ba6-42c6-9d05-5f881fb1b58e.png)

_Show the Created Database_

 ![image](https://user-images.githubusercontent.com/98270930/164433044-e189e893-5549-4b81-8f05-42d63a4506a6.png)

_Enter into the specified Database_

 ![image](https://user-images.githubusercontent.com/98270930/164433288-a061e2e5-26aa-4b93-90fe-cdb70cd822ec.png)
 
 _Delete the Database_
 
 ![image](https://user-images.githubusercontent.com/98270930/164434562-50e2d6f2-6e5f-4de9-9bb2-522124a8d163.png)


_Database Table Creation Syntax_
```bash
    CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
    ....
    );
```
_MySQL ALTER TABLE Statement_

ALTER TABLE - :-
 ```bash
# ADD Column
  ALTER TABLE table_name
    ADD column_name datatype; 

# DROP COLUMN:-
  ALTER TABLE table_name
    DROP COLUMN column_name;  
    
# MODIFY COLUMN:-
  ALTER TABLE table_name
    MODIFY COLUMN column_name datatype;   
```
_MySQL Copy/Clone/Duplicate Table_
 ```bash
    CREATE TABLE new_table_name  
      SELECT column1, column2, column3   
        FROM existing_table_name;    
```

_MySQL INSERT INTO Statement_
 ```bash
    INSERT INTO table_name (column1, column2, column3, ...) VALUES (value1, value2, value3, ...); 
                                            [or]
    INSERT INTO table_name VALUES (value1, value2,...valueN),( value1, value2,...valueN ),...........,( value1, value2,...valueN );                                      
```

_MySQL UPDATE Statement_
 ```bash
    UPDATE table_name  
        SET column1 = value1, column2 = value2, ...
            WHERE condition;                                               
```

_MySQL ORDER BY_
```bash
    SELECT column1, column2, ...
        FROM table_name
            ORDER BY column1, column2, ... ASC|DESC; 
```

_LIMIT - The LIMIT clause is used to specify the number of records to return._
```bash
    SELECT column_name(s)
        FROM table_name
            WHERE condition
                LIMIT number; 
```
_Basic Syntax of MySQL_

|S.NO|SYNTAX|DESCRIPTION|
|---|----|-----|
|1.|CREATE DATABASE [db-name];  |To create a new database.|
|2.|SHOW DATABASES;|List out the databases.|
|3.|USE [db-name];|Enter into the specified database.|
|4.|DROP DATABASE [db_name];|To delete the specified database.|
|5.|CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';| Create a new user|
|6.|GRANT permission_type ON database.table TO 'username'@'localhost';| To grant privileges to a user account |
|7.|GRANT INSERT ON * . * TO 'username'@'localhost';|To grant insert privileges to a MySQL user|
|8.|SHOW GRANTS FOR username;|To display all the current privileges held by a user|
|9.|GRANT ALL PRIVILEGES ON * . * TO 'database_user'@'localhost';|To grant all privileges to MySQL User on all databases|
|10.|GRANT ALL PRIVILEGES ON database_name.* TO 'database_user'@'localhost';|To grant all privileges to a user account on a specific database|
|11.|GRANT ALL PRIVILEGES ON database_name.table_name TO 'database_user'@'localhost';|To grant all privileges to a user account over a specific table from a database |
|12.|REVOKE permission_type ON database.table TO 'username'@'localhost';|Revoke Privileges MySQL User Account|
|13.|DROP USER 'username'@'localhost';|Remove an Entire User Account|
|14.|TRUNCATE TABLE table_name;|It is used to delete the data inside a table.|
|15.|SHOW TABLES; | List out all the tables in specified database.|
|16.|RENAME old_table TO new_table;| To rename the name of the table|
|17.|DESC table_name|Describe the specified table details.|
|18.|DROP TABLE  table_name;|It is used to delete complete the data in the table.|
|19.|DELETE FROM table_name WHERE condition; |To delete the row of the table using where condition.|
|20.|SELECT column1, column2, ...FROM table_name; |To view the specified colums details in specified table.|
|21.|SELECT * FROM table_name; |To view a details of the entire specified table.|
|22.|SELECT SUM(TABLE_ROWS) FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA = 'YOUR_DATABASE_NAME';| Calculate the database total data.|

### Reference:-

For more details visit this page - https://www.javatpoint.com/mysql-tutorial

