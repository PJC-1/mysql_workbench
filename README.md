MySQL
===================

Notes
-------------
>**MySQL Location** (*default* location on *Mac*)
>`/usr/local/mysql/bin`
>
>**Add MySQL to your PATH**
>*Add it to your PATH for the Current Session*
>`export PATH=${PATH}:/usr/local/mysql/bin`
>
>*Add it to your PATH Permanently*
>`echo 'export PATH="/usr/local/mysql/bin:$PATH"' >> ~/.bash_profile`
>
>To confirm, open a new *terminal* and run the command `mysql --version`.
>The output should be the following:
>```
>$ mysql --version
>mysql  Ver 8.0.16 for macos10.14 on x86_64 (MySQL Community Server - GPL)
>```
>
>**MySQL Service** (*on Mac*)
>Run the following command to **start**/**stop** the *MySQL service*.
>```
>sudo /usr/local/mysql/support-files/mysql.server start
>sudo /usr/local/mysql/support-files/mysql.server stop
>```
>
>**MySQL Service** (*on Ubuntu 18.04 LTS*)
>`systemctl status mysql.service`
>

MySQL Workbench
-------------
>
>NOTE: *Remember to log out as the mysql user from the terminal before creating a MySQL Workbench connection*.
>
>**Set a database**
>Under *Schemas*, select a *Database*, *right-click*, and *select* the option `Set as Default Schema`.
>
>
>

COMMANDS
-------------
>**Create a user**
>*syntax*
>
>`CREATE USER '<USER_NAME>'@'<HOST>' IDENTIFIED BY '<PASSWORD>'`
>
>*example*
>
>`CREATE USER 'joe1996'@'localhost' IDENTIFIED BY 'examplePa$$w0rd'`
>
>**Display user and host**
>*syntax*
>
>`SELECT user, host FROM mysql.user;`
>
>**Grant all privileges for a user**
>*syntax*
>
>`GRANT ALL PRIVILEGES ON * . * TO 'joe1996'@'localhost';`
>
>**Reloads the privileges from the grant tables in the `mysql` system database.**
>*syntax*
>
>`FLUSH PRIVILEGES;`
>
>**Create database and display all databases**
>*syntax*
>
>```
>CREATE DATABASE <DB_NAME>;
>
>SHOW DATABASES;
>```
>
>**Use a specific database**
>
>*syntax*
>
>```
>USE <DB_NAME>;
>```
>
>**Display available Tables within a Database**
>
>```
>SHOW TABLES;
>```
>
>**Creating Tables**
>
>*syntax*
>
>```
>CREATE TABLE <TABLE_NAME> (
>    <FIELD_NAME> <FIELD_TYPE>,
>    PRIMARY KEY(<FIELD_NAME>)
>);
>```
>
>*example*
>
>```
>CREATE TABLE users(
>    id INT AUTO_INCREMENT,
>    first_name VARCHAR(100),
>    last_name VARCHAR(100),
>    PRIMARY KEY(id)
>);
>```
>
>**Remove a Table**
>
>*syntax*
>
>`DROP TABLE <TABLE_NAME>;`
>
>**Delete Database**
>
>*syntax*
>
>`DROP DATABASE <DATABASE_NAME>;`
>
>**Create a record**
>
>*example (adding a user to the users table)*
>
>```
>INSERT INTO users(first_name, last_name, email, password)
>values ('John', 'Doe', 'john@gmail.com', 123456);
>```
>
>**Inserting multiple rows**
>
>*example (adding multiple users for the users table)*
>
>```
>INSERT INTO users (first_name, last_name, email, password, location, dept,  is_admin, register_date)
>	values ('Fred', 'Smith', 'fred@gmail.com', '123456', 'New York', 'design', 0, now()),
>		('Sara', 'Watson', 'sara@gmail.com', '123456', 'New York', 'design', 0, now()),
>		('Will', 'Jackson', 'will@yahoo.com', '123456', 'Rhode Island', 'development', 1, now()),
>		('Paula', 'Johnson', 'paula@yahoo.com', '123456', 'Massachusetts', 'sales', 0, now()),
>		('Tom', 'Spears', 'tom@yahoo.com', '123456', 'Massachusetts', 'sales', 0, now());
>```
>
>**Return first name and last name where the first name is 'John'**
>
>*example*
>
>```
>SELECT first_name, last_name FROM users WHERE first_name = 'John';
>```
>
>**Return all columns for users that are located in Oakland and belong to the R&D department**
>
>*example*
>
>```
>SELECT * FROM users WHERE location="Oakland" AND dept="R&D";
>```
>
>**Return all users who are admins**
>
>*example*
>
>```
>SELECT * FROM users WHERE is_admin > 0;
>```
>**NOTE:** *The use of the greater than symbol.*
>
>**Return all users by Last Name in Ascending Order**
>
>*example*
>```
>SELECT * FROM users ORDER BY last_name ASC;
>```  
>
>**Return all users by Age in Descending Order**
>
>*example*
>
>```
>SELECT * FROM users ORDER BY age DESC;
>```
>
>**Return a new column containing Firstname and Lastname. Also include Department and Age**
>
>*example*
>
>```
>SELECT CONCAT(first_name, ' ', last_name) AS 'Name', dept, age FROM users;
>```
>**NOTE:** *`CONCAT()`will combine any columns together and return a single new column.*
>
>**Return all Cities from the Users Table, only unique values (no duplicates)**
>
>*example*
>
>```
>SELECT DISTINCT location FROM users;
>```
>
>**NOTE:** *`DISTINCT` will ensure that only unique values will be returned, with out it you'll receive duplicates in the returned output.*
>
>**Return all users that are with the age range of 22 - 24**
>
>*example*
>
>```
>SELECT * FROM users WHERE age BETWEEN 22 AND 25;
>```
>**NOTE:** *`BETWEEN` can be used to specify a range of values.*
>
>**Return all users who belong to a Department that contains the letter `p`**
>
>*example*
>
>```
>SELECT first_name FROM users WHERE dept LIKE '%p%';
>```
>**NOTE:** *The `%p%` syntax will search for any existance of the letter `p` in the Department column, i.e. returning Departments such as Su**pp**ort* or **P**roduct.
>
>**Return all users that belong to the `Product` and `Support` department**
>
>*example*
>```
>SELECT * FROM users WHERE dept IN('Product', 'Support');
>```
>
>**NOTE:** *The use of the `IN()` clause helps us avoid extensive use of the `AND` clause.*
>
>**Returning values from two tables**
>*example (Obtaining values from the `users` table and the `posts` table using `INNER JOIN` clause)
>
>```
>SELECT
>users.first_name,
>users.last_name,
>posts.user_id,
>posts.title
>FROM users
>INNER JOIN posts
>ON users.id = posts.user_id
>ORDER BY posts.title;
>```
>
>**Delete a user by id**
>
>*example*
>
>```
>DELETE FROM users WHERE id=6;
>```
>
>**Update a users email address**
>
>*example*
>
>```
>UPDATE users SET email="new.email@gmail" WHERE id=1;
>```
>**NOTE:** *It's best practice to always use a `WHERE` clause to avoid updating all users in a table.
>
>**Add a column to an existing Table**
>
>*example adding an Age column to the Users Table*
>
>```
>ALTER TABLE users ADD age VARCHAR(3);
>```
>
>**Set another column as an index to search by**
>
>*example (Setting the location column as an index from the users table)*
>
>```
>CREATE INDEX LIndex on users(location);
>```
>
>**Remove an existing index**
>
>*example*
>
>```
>DROP INDEX LIndex on users;
>```
>
>**Create new table with a Foreign Key**
>
>*example(Creating a Table of Posts that contains a Foreign Key of `user_id` from the Users Table's `id` property)*
>
>```
>CREATE TABLE posts(
>    id INT AUTO_INCREMENT,
>    user_id INT,
>    title VARCHAR(100),
>    body TEXT,
>    publish_date DATETIME DEFAULT CURRENT_TIMESTAMP,
>    PRIMARY KEY(id),
>    FOREIGN KEY(user_id) REFERENCES users(id)
>);
>```
>
>*example (Create Comments Table with references to the Posts and Users tables)*
>
>```
>CREATE TABLE comments(
>    id INT AUTO_INCREMENT,
>    post_id INT,
>    user_id INT,
>    body INT,
>    publish_data DATETIME DEFAULT CURRENT_TIMESTAMP,
>    PRIMARY KEY(id),
>    FOREIGN KEY(post_id) REFERENCES posts(id),
>    FOREIGN KEY(user_id) REFERENCES users(id)
>);
>```
>

Helpful Links
-------------
>[Official MySQL site](https://dev.mysql.com/)
>[MySQL Workbench](https://dev.mysql.com/downloads/workbench/)
>[Helpful Article on how to install and configure MySQL on ubuntu 18.04](https://vitux.com/how-to-install-and-configure-mysql-in-ubuntu-18-04-lts/)
>[Good reference for installing MySQL Workbench on ubuntu](https://ubuntu-mate.community/t/how-to-install-mysql-server-and-mysql-workbench-on-ubuntu-mate-18-04/17884)
