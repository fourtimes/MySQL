# Mysql backup, restore and etc
##### Back up the database using the following command:
```bash
mysqldump --user=(username) -p(password){Qnf --databases database_name | gzip > /opt/filename.gz
                      or  
mysqldump -u root -p [database_name] > userA.sql                        
```
##### Restore the data one database to another database
```bash
mysql -u [username] –p[password] [database_name] < [dump_file.sql]
                        or
mysql -u root -p [another_database_name] < userA.sql
```
For more details - https://support.hostway.com/hc/en-us/articles/360000220190-How-to-backup-and-restore-MySQL-databases-on-Linux
# Transfer files
##### scp (secure copy)  - Linux system is used to copy file(s) between servers in a secure way.
```bash
scp /home/ubuntu/Desktop/filename crash@192.168.193.83:/home/crash/Desktop/ashli-project
```
