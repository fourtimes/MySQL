# MySQL Replications
Replication enables data from one MySQL database server (Master Node) to be copied to one or more MySQL database servers (Slave Node). Replication is asynchronous by default; replicas do not need to be connected permanently to receive updates from the source. Depending on the configuration, you can replicate all databases, selected databases, or even selected tables within a database.

_**Let's create two server's**_
```sh
Master IP - 10.0.0.10
Slave IP  - 10.0.0.13
```
## Replication for Master Node

_1. Install mysql package_
```bash
sudo apt install mysql-server
```
_2. add the configurations as per the below instruction._
```sh
# sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address = 10.0.0.10

server-id = 1

log_bin = /var/log/mysql/mysql-bin.log
log_bin_index =/var/log/mysql/mysql-bin.log.index
relay_log = /var/log/mysql/mysql-relay-bin
relay_log_index = /var/log/mysql/mysql-relay-bin.index

binlog-do-db = hello # your-database-name
```
_3. Restart the mysql service & check the status of the service_
```mysql
sudo service mysql restart
sudo service mysql status
```
_4. Login to the Database_
```mysql
sudo mysql -u root
```
```mysql
# Create a New User for Replication on Master Node
CREATE USER 'repl'@'10.0.0.13' IDENTIFIED BY 'replica_password';  # this user allow only 10.0.0.13 user.

# grant the permission for the specified user.
GRANT REPLICATION SLAVE ON *.* TO 'repl'@'10.0.0.13' ;

# Lock the Master Database and Get Log Position
FLUSH TABLES WITH READ LOCK;
SHOW MASTER STATUS;

SHOW MASTER STATUS\G;
```
5. Backup the Master Database: While the tables are locked, take a backup of the master database:
```mysql
mysqldump -u root -p --all-databases --master-data > hello.sql
```
6. Unlock the Master Tables:
       After the backup is complete, unlock the tables:
```mysql
UNLOCK TABLES;
```

## Replication for Slave Node

_1. Transfer the Backup to the Slave Server:_
_2. Install mysql package_
```bash
sudo apt install mysql-server
```
_3. Add the configurations as per the below instruction._
```sh
# sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address = 10.0.0.13

server-id = 2

log_bin = /var/log/mysql/mysql-bin.log
log_bin_index =/var/log/mysql/mysql-bin.log.index
relay_log = /var/log/mysql/mysql-relay-bin
relay_log_index = /var/log/mysql/mysql-relay-bin.index
binlog-do-db = hello # your-database-name

```
_4. Restart the mysql service & check the status of the service_

```mysql
sudo service mysql restart
sudo service mysql status
```
_5. Restore the Backup on the Slave:_
```mysql
sudo mysql -u root -p < hello.sql
```
_6. Login to the Database_
```sh
sudo mysql -u root
```
_7. stop the slave node_
```bash
STOP SLAVE;
```
_8. To allow the slave server to replicate the Master server, run the command._
```mysql
CHANGE MASTER TO MASTER_HOST='10.0.0.10', MASTER_USER='repl', MASTER_PASSWORD='replica_password', MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=6257;
```
**Note:**
- MASTER_LOG_FILE and MASTER_LOG_POS refer the Master Node using this `SHOW MASTER STATUS\G;`command

_9. start the slave node_
```mysql
START SLAVE;
```
_10. Check the slave replication status_
```mysql
SHOW SLAVE STATUS\G;
[OR]
SHOW REPLICA STATUS\G;
```
If it is running, it will reflect the `yes`  keyword. So, the meaning is that replication has started.![image](https://github.com/fourtimes/MySQL_Docs/assets/91359308/c91ef5e6-a2be-459e-a345-8dd0c9fdfc91)

## Testing the MySQL Master-Slave Replication

_Log into MySQL in the Master server_
```bash
sudo mysql -u root -p
```
_Let’s create a test database. In this case, we will create a database called **hello**_
```mysql
CREATE DATABASE hello;
```

![image](https://github.com/fourtimes/MySQL_Docs/assets/91359308/ac587299-3e5c-46bb-ac53-cf2424577d6d)
![image](https://github.com/fourtimes/MySQL_Docs/assets/91359308/0e8ad2fa-78fb-44cf-af6f-3dcddc3f376b)

_Now, log in to your MySQL instance in the slave server_

```mysql
sudo mysql -u root -p
```
```mysql
SHOW DATABASES;
```
![image](https://github.com/fourtimes/MySQL_Docs/assets/91359308/607e3a1b-c194-4302-bfea-51d01ea32626)

![image](https://github.com/fourtimes/MySQL_Docs/assets/91359308/4bff30ca-f55d-49a4-89ef-c89646f4f6f7)


_Reference_ 
- https://snapshooter.com/learn/mysql/MySQL-replication
- https://www.tecmint.com/setup-mysql-master-slave-replication-on-ubuntu/

Replication to the specific database
- https://www.digitalocean.com/community/tutorials/how-to-set-up-replication-in-mysql

