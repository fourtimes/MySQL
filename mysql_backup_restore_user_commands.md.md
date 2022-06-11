# Mysql backup, restore and etc
##### Back up the database and store the local machine using the following command:
```bash
mysqldump --user=(username) -p(password){Qnf --databases database_name | gzip > /opt/filename.gz
                      or  
mysqldump -u root -p [database_name] > target_file.sql                        
```
##### Restore the data backup file to database
```bash
mysql -u [username] –p[password] [database_name] < [dump_file.sql]
                        or
mysql -u root -p [database_name] < backup_file.sql
```
For more details - https://support.hostway.com/hc/en-us/articles/360000220190-How-to-backup-and-restore-MySQL-databases-on-Linux

#### Specific permission for users 
```bash
# create, insert,update,delete,alter,select
GRANT CREATE,
INSERT,
SELECT,
UPDATE,DELETE,DROP, ALTER ON database_name.* TO 'username' @'localhost';
```
#### Read only permission for users
```bash
# select - read only permission
GRANT SELECT ON database_name.* TO 'username' @'localhost';
```

# Transfer files
##### scp (secure copy)  - Linux system is used to copy file(s) between servers in a secure way.
```bash
scp /home/ubuntu/Desktop/filename crash@192.168.193.83:/home/crash/Desktop/ashli-project
```
