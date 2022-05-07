### Back up the database using the following command:
```bash
mysqldump --user=(username) -p(password){Qnf --databases db_amazon | gzip > /opt/db_amazon.gz
                      or  
mysqldump -u root -p userA > userA.sql                        
```
### Restore the data one database to another database
```bash
mysql -u [username] –p[password] [database_name] < [dump_file.sql]
                        or
mysql -u root -p userB < userA.sql
```
### scp (secure copy)  - Linux system is used to copy file(s) between servers in a secure way.
```bash
scp /home/ubuntu/Desktop/filename crash@192.168.193.83:/home/crash/Desktop/ashli-project
```
