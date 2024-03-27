# Database in laravel

### 1.use mysql

to use mysql in laravel, you should go to `xampp/mysql/bin` copy the path and search in windows for `enviroment variables` locate `path` double click it or select edit, add new and paste the path in it, apply and close.

### 2.connet to database and create one

#### 1.Login

open your therminal type:
```
mysql -u root

```
now you're connected to mysql.

#### 2.create

open therminal type:
```
create database DBname;

```
now your DB is created.

### 3.Connect

go to your laravel root directory, locate `.env`. find "DB_database" at line 12, change the value to your database name.

