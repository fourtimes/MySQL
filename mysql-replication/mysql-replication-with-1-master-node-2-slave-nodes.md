# MySQL Replication using 1 Master Node 2 Slave Node
## Step 1: Creating Master Node
Update and Install the mysql service
```cmd
sudo apt update && sudo apt install -y mysql-server
sudo systemctl start mysql && sudo systemctl enable mysql && sudo systemctl status mysql 
```
Configure Master Server
```cnf
# sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
server-id=1
log_bin=/var/log/mysql/mysql-bin.log
relay-log=/var/log/mysql/mysql-relay-bin.log
binlog_do_db=erpdata # your db name
```
Restart the mysql service
```cmd
sudo systemctl restart mysql
```
Create database
```mysql
CREATE DATABASE erpdata;
```
Create Replication User
```mysql
CREATE USER 'repl'@'%' IDENTIFIED WITH mysql_native_password BY 'Password@123';
GRANT REPLICATION SLAVE ON *.* TO 'repl'@'%';
FLUSH PRIVILEGES;

FLUSH TABLES WITH READ LOCK;
SHOW MASTER STATUS;
```
If You Want to Replicate Existing Data
```cmd
sudo mysqldump -u root erpdata > erpdata.sql
```
Unlock the tables
```mysql
sudo mysql
UNLOCK TABLES;
```
## Step 2: Adding Slave Node 1
Update and Install the mysql service
```cmd
sudo apt update && sudo apt install -y mysql-server
sudo systemctl start mysql && sudo systemctl enable mysql && sudo systemctl status mysql 
```
Copy and Transfer the mysql db backup file from master node to slave node 2
```cmd
scp [file_path] [username]@[ip_address]:~
```
Create the same database name in slave node 2
```mysql
CREATE DATABASE erpdata;
```
Restore the mysql backup file in slave node 2
```cmd
sudo mysql -u root erpdata < erpdata.sql
```
Configure Slave Server
```cnf
# sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
server-id=2
log_bin=/var/log/mysql/mysql-bin.log
binlog_do_db=mysql
relay-log= /var/log/mysql/mysql-relay-bin.log
```
Restart the mysql service
```cmd
sudo systemctl restart mysql
```
Start Replication
```mysql
sudo mysql
```
```mysql
CHANGE REPLICATION SOURCE TO
SOURCE_HOST='172.31.33.246',
SOURCE_USER='repl',
SOURCE_PASSWORD='Password@123',
SOURCE_LOG_FILE='mysql-bin.000001',  # refer the log file from master node
SOURCE_LOG_POS=1766; # refer the log position from master node
```
```mysql
START REPLICA;
SHOW REPLICA STATUS\G;
```

## Step 3: Adding Slave Node 2
Update and Install the mysql service
```cmd
sudo apt update && sudo apt install -y mysql-server
sudo systemctl start mysql && sudo systemctl enable mysql && sudo systemctl status mysql 
```
Transfer the mysql db backup file from master node to slave node 2
```cmd
scp [file_path] [username]@[ip_address]:~
```
Create the same database name in slave node 2
```mysql
CREATE DATABASE erpdata;
```
Restore the mysql backup file in slave node 2
```cmd
sudo mysql -u root erpdata < erpdata.sql
```
Configure Slave Server
```cnf
# sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
server-id=3
log_bin=/var/log/mysql/mysql-bin.log
binlog_do_db=mysql
relay-log= /var/log/mysql/mysql-relay-bin.log
```
Restart the mysql service
```cmd
sudo systemctl restart mysql
```
Start Replication
```mysql
sudo mysql
```
```mysql
CHANGE REPLICATION SOURCE TO
SOURCE_HOST='172.31.33.246',
SOURCE_USER='repl',
SOURCE_PASSWORD='Password@123',
SOURCE_LOG_FILE='mysql-bin.000001',  # refer the log file from master node
SOURCE_LOG_POS=1766; # refer the log position from master node
```
```mysql
START REPLICA;
SHOW REPLICA STATUS\G;
```

Reference - https://phoenixnap.com/kb/mysql-master-slave-replication
