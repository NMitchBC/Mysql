<!-- MySQL Cheat Sheet, via .MD document and uploaded to github in a web108 repo (or a mysql repo, whatever you would like). please link the file to me rocket chat -->

# MySQL Cheat Sheet

### How to login into mysql from terminal

- ssh into the server, sudo into mysql
- This command is used to log into the MySQL server from the terminal. Replace username with your MySQL username. The -p flag prompts for your password.

```
ssh into server
enter the password
sudo mysql -u [username] -p
enter the password
enter the password again
```

- ie:

```
ssh AD@12.34.56.78
somePassword!42
sudo mysql -u [root] -p
somePassword!42
somePassword!42
```

- If you are the admin for the ip use root as username, otherwise you would use the username

### How to SHOW USERS

- This query lists all users and their host in the MySQL database. It retrieves user information from the mysql.user system table.

```
SELECT * FROM mysql.user;
```

- could also use

```
SELECT User, Host FROM mysql.user;
```

### How to CREATE USERS

- This command creates a new user in MySQL. Replace username with the desired username and password with a secure password. The @'localhost' part specifies that this user can only connect from the local machine.

```
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
```

- ie:

```
CREATE USER 'library_user'@'localhost' IDENTIFIED BY 'password123';
```

### How to GRANT PRIVILEGES, Show granted privileges and remove.

#### Grant privileges

- This command grants all privileges to a user on a specified database with username & ip location. It's essential for a user to have necessary privileges to perform actions like creating tables and querying data.

```
GRANT ALL PRIVILEGES ON database.table TO 'username'@'localhost''
```

- ie:

```
GRANT ALL PRIVILEGES ON library.* TO 'library_user'@'localhost';
```

#### Show granted privileges.

- This command displays all the privileges granted to a specific user.

```
SHOW GRANTS FOR 'username'@'localhost';
```

- ie:

```
SHOW GRANTS FOR 'library_user'@'localhost';
```

#### Remove granted privileges

- This command revokes all privileges from a user on a specified database with username & ip location..

```
REVOKE ALL PRIVILEGES ON database.table FROM 'username'@'localhost';
```

- ie:

```
REVOKE ALL PRIVILEGES ON library.* FROM 'library_user'@'localhost';
```

### How to SHOW, DELETE & CREATE DATABASES & SELECT DATABASES

#### Show databases

- This command lists all databases on the MySQL server.

```
SHOW DATABASES;
```

#### Delete a database

- This command deletes an entire named database. Use it with caution as it removes all data and structures under the database.

```
DROP DATABASE database.name;
```

- ie:

```
DROP DATABASE database.world;
```

#### Create a new database

- This creates a new database by name

```
CREATE DATABASE database.name;
```

- ie:

```
CREATE DATABASE database.world;
```

### Select a database

- This selects a specific database by name(ie: world.country)

```
USE database.name;
```

- ie:

```
USE world.country;
```

```
USE world;
```

### How to CREATE a TABLE with Columns and their data types

- Creates a named table with columns 1,2,3 and then insert desired datatype (ie: INT, VARCHAR)

```
CREATE TABLE table_name (
column1 datatype,
column2 datatype,
column3 datatype
);
```

- ie:

```
CREATE TABLE library.NewBook (
id INT AUTO_INCREMENT PRIMARY KEY,
title VARCHAR(255) NOT NULL,
author VARCHAR(255),
isbn VARCHAR(13),
year_published INT
);

```

- id: An integer column that auto-increments and is the primary key.
- title: A string (VARCHAR) column that must be filled (NOT NULL).
- author: Another string column for the book's author.
- isbn: A string column for the book's ISBN, assumed to be 13 characters.
- year_published: An integer column for the year the book was published.

### How to SHOW, DELETE & DROP Tables

#### Show all tables

- This shows all Tables

```
USE world;
SHOW TABLES;
```

- USE world; selects the world database.
- SHOW TABLES; then lists all the tables in the world database.

```
SHOW TABLES in library;
```

- shows all tables in library

#### Delete a table by name

- This deletes a table by name

```
DELETE FROM table_name;
```

- ie:

```
DELETE FROM library.LendRecord;
```

- removes all data from LendRecord but leaves the empty table in place.

#### Drop a table by name

- This drops a table by name (permanent)

```
DROP TABLE table_name;
```

- ie:

```
DROP TABLE library.TempBooks;
```

- completely removes the TempBooks table and its data.

### How to Insert ROWS & RECORDS (single and multiple)

#### Insert a single row

- Inserts a single row by table name in columns with associated values

```
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);
```

- ie:

```
INSERT INTO library.Books (title, author, isbn, year_published)
VALUES ('To Kill a Mockingbird', 'Harper Lee', '9780061120084', 1960);
```

#### Insert multiple rows

- Inserts multiple rows by table name in columns with associated values

```
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3),
(value1, value2, value3);
```

- ie:

```
INSERT INTO library.Books (title, author, isbn, year_published)
VALUES
('1984', 'George Orwell', '9780451524935', 1949),
('The Great Gatsby', 'F. Scott Fitzgerald', '9780743273565', 1925),
('Pride and Prejudice', 'Jane Austen','9780679783268', 1813);
```

- This command will insert three new rows into the Books table.

### How to SELECT with the WHERE Clause

- Selects with the where clause. This command selects rows from a table that meet the specified condition.

```
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

- ie:

```
SELECT title, author, year_published
FROM library.Books
WHERE year_published > 2000;
```

### How to SELECT with the WHERE Clause using a range

- This command selects rows where the value of a column falls within a specified range.

```
SELECT * FROM table.name WHERE column_name BETWEEN vale1 AND value2;
```

- ie:

```
SELECT * FROM country.city WHERE Population BETWEEN 670000 AND 700000;
```

### How to DELETE an individual ROW

- This command deletes rows from a table that satisfy the specified condition.

```
DELETE FROM table_name WHERE condition;
```

- ie:

```
DELETE FROM library.Lenders
WHERE lender_id = 123;
```

- This command deletes the row in the Lenders table where the lender_id equals 123.

### How to UPDATE a ROW

- This command updates specific columns of rows in a table that meet the given condition.

```
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```

- ie:

```
UPDATE library.Books
SET author = 'New Author', year_published = 2021
WHERE isbn = '1234567890';
```

### How to add a new column and modify it

#### Add a new Column:

- This command adds a new column to an existing table.

```
ALTER TABLE table_name ADD column_name datatype;
```

- ie:

```
ALTER TABLE library.Books ADD COLUMN genre VARCHAR(100);

```

- Adds a new column named genre to the Books table.

#### Modify the column:

- This command changes the data type of an existing column.

```
ALTER TABLE table_name MODIFY column_name new_datatype;
```

- ie:

```
ALTER TABLE library.Books MODIFY COLUMN genre VARCHAR(150);
```

- Changes the genre column's data type or size

### How to Order by and use Distinct

#### Order by

- This command sorts the result set in ascending (ASC) or descending (DESC) order.

```
SELECT * FROM table_name ORDER BY column_name ASC|DESC;
```

- ie:

```
SELECT * FROM library.Books ORDER BY year_published DESC;
```

- Orders books by year_published in descending order.

#### Use Distinct

- This command is used to return unique values from a column, eliminating duplicates.

```
SELECT DISTINCT column_name FROM table_name;
```

- ie:

```
SELECT DISTINCT author FROM library.Books;
```

- Selects unique authors from the Books table.

### How to Concatenate Columns

- This command concatenates two or more columns in a table.

```
SELECT CONCAT(column1, ' ', column2) AS new_column FROM table_name;
```

- ie:

```
SELECT CONCAT(title, ' - ', author) AS full_details FROM library.Books;
```

- Concatenates the title and author columns, separated by ' - '

### How to Select Distinct Rows

- This command selects unique rows from a table.

```
SELECT DISTINCT * FROM table_name;
```

- ie:

```
SELECT DISTINCT * FROM library.Users;
```

- Selects distinct rows from the Users table.

### How to use LIKE to Search

- This command is used for pattern matching. % represents zero or more characters, and \_ represents a single character.

```
SELECT * FROM table_name WHERE column_name LIKE pattern;
```

- ie:

```
SELECT * FROM library.Books WHERE title LIKE '%World%';
```

- Finds books whose titles contain 'World'.

### How to Select using IN

- This command is used to filter the result set to include rows where the column value matches any value in the list.

```
SELECT * FROM table_name WHERE column_name IN (value1, value2);
```

- ie:

```
SELECT * FROM library.Books WHERE author IN ('George Orwell', 'Aldous Huxley');
```

- Selects books written by George Orwell or Aldous Huxley.

### How to Create & Remove Index

#### Create Index:

- This command creates an index on a table column, which can improve the speed of data retrieval.

```
CREATE INDEX index_name ON table_name (column_name);
```

- ie:

```
CREATE INDEX idx_title ON library.Books (title);
```

- Creates an index idx_title on the title column in the Books table

#### Remove Index:

- This command removes an index from a table.

```
DROP INDEX index_name ON table_name;
```

- ie:

```
DROP INDEX idx_title ON library.Books;
```

- Drops the idx_title index from the Books table.

### Create Two Tables - demonstrating a one to many relationship that shows a PrimaryKey & ForeignKey

- These commands create two tables demonstrating a one-to-many relationship. parent_table is the parent table, and child_table contains a foreign key that references the primary key of parent_table.

```
CREATE TABLE parent_table (
parent_id INT AUTO_INCREMENT PRIMARY KEY,
data VARCHAR(100)
);

CREATE TABLE child_table (
child_id INT AUTO_INCREMENT PRIMARY KEY,
parent_id INT,
data VARCHAR(100),
FOREIGN KEY (parent_id) REFERENCES parent_table(parent_id)
);
```

- ie:

```
CREATE TABLE library.Authors (
author_id INT AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(100)
);

CREATE TABLE library.Books (
book_id INT AUTO_INCREMENT PRIMARY KEY,
title VARCHAR(255),
author_id INT,
FOREIGN KEY (author_id) REFERENCES library.Authors(author_id)
);
```

- Creates an Authors table and a Books table with a foreign key author_id referencing Authors.

### How to use Inner Join

- This command joins two tables based on a common field, returning rows where there is a match in both tables.

```
SELECT * FROM table1
INNER JOIN table2
ON table1.common_field = table2.common_field;
```

- ie:

```
SELECT Books.title, Authors.name
FROM library.Books
INNER JOIN library.Authors ON Books.author_id = Authors.author_id;
```

- Joins Books and Authors tables on author_id

### How to JOIN Multiple Tables -->

- This command joins multiple tables based on common fields. It's useful for combining data from various tables into a single query result set.

```
SELECT * FROM table1
JOIN table2 ON table1.common_field = table2.common_field
JOIN table3 ON table1.other_common_field = table3.other_common_field;
```

- ie:

```
SELECT Books.title, Authors.name, LendRecord.due_date
FROM library.Books
JOIN library.Authors ON Books.author_id = Authors.author_id
JOIN library.LendRecord ON Books.book_id = LendRecord.book_id;
```

- Joins Books, Authors, and LendRecord tables to display book titles, author names, and due dates
