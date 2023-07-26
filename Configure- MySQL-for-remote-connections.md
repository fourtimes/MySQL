1. Configure MySQL for remote connections
---------------------------------------------
The first thing we must do is configure MySQL for remote connections. To do this:

1. Log into your MySQL database server and open the configuration file with the command:

`sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf`

2. In that file, look for the line:

`bind-address = 127.0.0.1`

3. Change that line to:

`bind-address = 0.0.0.0`

4. Save and close the file.

5. Restart the MySQL service with:

`sudo systemctl restart mysql`
