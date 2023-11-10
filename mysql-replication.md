# MySQL Replications

_**1. Let's create two server's with the same VPC.**_
```sh
Master IP - 10.0.0.10
Slave IP  - 10.0.0.13
```
_**2.Replication for Master Node**_

_Install mysql package_
```bash
sudo apt install mysql-server
```
_add the configurations as per the below instruction._
```sh
# sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address = 10.0.0.10 [or] bind-address = 0.0.0.0    #  0.0.0.0 -  allow all the ip's to the master node replication server

server-id = 1

log_bin = /var/log/mysql/mysql-bin.log
log_bin_index =/var/log/mysql/mysql-bin.log.index
relay_log = /var/log/mysql/mysql-relay-bin
relay_log_index = /var/log/mysql/mysql-relay-bin.index
```
_Restart the mysql service & check the status of the service_
```mysql
sudo service mysql restart
sudo service mysql status
```
_Login to the Database_
```mysql
sudo mysql -u root
```
```mysql
# Create a New User for Replication on Master Node
CREATE USER 'repl'@'10.0.0.13' IDENTIFIED BY 'replica_password';  # this user allow only 10.0.0.13 user.
[or]
CREATE USER 'repl'@'%' IDENTIFIED BY 'replica_password';    # this user allow all mysql remote user's
```
```mysql
# grant the permission for the specified user.
GRANT REPLICATION SLAVE ON *.* TO 'repl'@'10.0.0.13' ;
[OR]
GRANT REPLICATION SLAVE ON *.* TO 'repl'@'%' ;
```
```mysql
FLUSH PRIVILEGES;
```
```mysql
SHOW MASTER STATUS\G;
```

_**3.Replication for Slave Node**_

_Install mysql package_
```bash
sudo apt install mysql-server
```
_add the configurations as per the below instruction._
```sh
# sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address = 10.0.0.13 [or] bind-address = 0.0.0.0    #  0.0.0.0 -  allow all the ip's to the master node replication server

server-id = 2

log_bin = /var/log/mysql/mysql-bin.log
log_bin_index =/var/log/mysql/mysql-bin.log.index
relay_log = /var/log/mysql/mysql-relay-bin
relay_log_index = /var/log/mysql/mysql-relay-bin.index
```
_Restart the mysql service & check the status of the service_

```mysql
sudo service mysql restart
sudo service mysql status
```
_Login to the Database_
```sh
sudo mysql -u root
```
_stop the slave node_
```bash
STOP SLAVE;
```
_To allow the slave server to replicate the Master server, run the command._
```mysql
CHANGE MASTER TO MASTER_HOST='10.0.0.10', MASTER_USER='repl', MASTER_PASSWORD='.', MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=6257;
```
Note:
- MASTER_LOG_FILE and MASTER_LOG_POS refer the Master Node using this `SHOW MASTER STATUS\G;`command

_start the slave node_
```mysql
START SLAVE;
```
_**4.Verify the MySQL Master-Slave Replication**_

_Log into MySQL in the Master server_
```bash
sudo mysql -u root -p
```
_Let’s create a test database. In this case, we will create a database called **hello**_
```mysql
CREATE DATABASE hello;
```
![image](https://github.com/fourtimes/MySQL_Docs/assets/91359308/ac587299-3e5c-46bb-ac53-cf2424577d6d)

_Now, log in to your MySQL instance in the slave server_

```mysql
sudo mysql -u root -p
```
```mysql
SHOW DATABASES;
```
![image](https://github.com/fourtimes/MySQL_Docs/assets/91359308/607e3a1b-c194-4302-bfea-51d01ea32626)

Reference 
- https://snapshooter.com/learn/mysql/MySQL-replication
- https://www.tecmint.com/setup-mysql-master-slave-replication-on-ubuntu/

