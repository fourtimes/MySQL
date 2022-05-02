# MySQL 

### 1. Login the mysql:

```bash
sudo mysql -u root -p
```
![image](https://user-images.githubusercontent.com/91359308/166200070-6cdb533c-d431-48c2-8b8a-a6136963252a.png)

### 2. Show the database list:

```bash
SHOW DATABASES;
```
![image](https://user-images.githubusercontent.com/91359308/166200240-b095852f-cedb-48d7-b80b-fadae6389b85.png)

### 3. How to create a user:

```bash
CREATE USER 'your_username'@'localhost' IDENTIFIED BY 'your_password';
```
![image](https://user-images.githubusercontent.com/91359308/166200589-dbbde4d8-8e1b-4651-b69f-f001dd5d705c.png)

### 4. Granting a User Permissions in specified database:

```bash
GRANT PRIVILEGE ON database.* TO 'username'@'localhost';
```
![image](https://user-images.githubusercontent.com/91359308/166200907-37ede882-956b-4e31-83f2-b9366f6a0774.png)

### 5. Show the user permission:
```bash
SHOW GRANTS FOR 'username'@'localhost';
```
![image](https://user-images.githubusercontent.com/91359308/166201052-5d33ad7c-275f-411c-9718-b8d0e01033b8.png)
