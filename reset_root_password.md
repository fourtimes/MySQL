## How to set root password for MySQL root user in Ubuntu 20.04 LTS:

#### 1. We have check the mysql version and the status of mysql

 ```bash
 mysql --version
 sudo systemctl status mysql.service
 ```
 ![image](https://user-images.githubusercontent.com/91359308/166138918-cacf2890-a7e8-4a1c-ad89-227c7a48518b.png)

 
 #### 2. Enter into mysql without password:

 ```bash
 sudo mysql
 ```
 ![image](https://user-images.githubusercontent.com/91359308/166138993-54153ae9-4d2b-462b-b149-794d61669c89.png)

#### 3. we have to change mysql database
 ```bash
 USE mysql;
 ```
![image](https://user-images.githubusercontent.com/91359308/166139023-9d79602a-2f7e-4e15-b856-ea9a603ade3a.png)

#### 4.  Set the root password:
 ```bash
 ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
 ```
![image](https://user-images.githubusercontent.com/91359308/166139074-bcb64de1-9a0c-44c3-ae4c-9eb959b404b9.png)

#### 5. Login to mysql using currently reseted password:
 ```bash
 sudo mysql -u root -p
 ```
![image](https://user-images.githubusercontent.com/91359308/166139117-42c7ebba-d76f-4834-a715-0a45f3fe9eb2.png)


