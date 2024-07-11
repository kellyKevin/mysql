# MySQL Cheatsheet

## Browsing and Inspecting
```sql
SHOW DATABASES;
SHOW TABLES;
SHOW FIELDS FROM table; -- or DESCRIBE table;
SHOW CREATE TABLE table;
SHOW PROCESSLIST;
KILL process_number;


SELECT Statements
sql
Copy code
SELECT * FROM table;
SELECT field1, field2 FROM table;
SELECT ... FROM ... WHERE condition;
SELECT ... FROM ... WHERE condition GROUP BY field;
SELECT ... FROM ... WHERE condition GROUP BY field HAVING condition2;
SELECT ... FROM ... WHERE condition ORDER BY field1, field2;
SELECT ... FROM ... WHERE condition ORDER BY field1, field2 DESC;
SELECT ... FROM ... WHERE condition LIMIT 10;
SELECT DISTINCT field1 FROM table;
SELECT DISTINCT field1, field2 FROM table;


Select - Joins
sql
Copy code
SELECT ... FROM t1 JOIN t2 ON t1.id1 = t2.id2 WHERE condition;
SELECT ... FROM t1 LEFT JOIN t2 ON t1.id1 = t2.id2 WHERE condition;
SELECT ... FROM t1 JOIN (t2 JOIN t3 ON ...) ON ...;


Conditions
sql
Copy code
field1 = value1;
field1 <> value1;
field1 LIKE 'value _ %';
field1 IS NULL;
field1 IS NOT NULL;
field1 IS IN (value1, value2);
field1 IS NOT IN (value1, value2);
condition1 AND condition2;
condition1 OR condition2;


Database Operations
sql
Copy code
CREATE DATABASE DatabaseName;
CREATE DATABASE DatabaseName CHARACTER SET utf8;
USE DatabaseName;
DROP DATABASE DatabaseName;
ALTER DATABASE DatabaseName CHARACTER SET utf8;


Backup and Restore
sh
Copy code
mysqldump -u Username -p dbNameYouWant > databasename_backup.sql;
mysql -u Username -p dbNameYouWant < databasename_backup.sql;


Repair Tables
sh
Copy code
mysqlcheck --all-databases;
mysqlcheck --all-databases --fast;


Insert Data
sql
Copy code
INSERT INTO table1 (field1, field2) VALUES (value1, value2);


Delete Data
sql
Copy code
DELETE FROM table1;
DELETE FROM table1 WHERE condition;
DELETE FROM table1, table2 WHERE table1.id1 = table2.id2 AND condition;
TRUNCATE table1;


Update Data
sql
Copy code
UPDATE table1 SET field1 = new_value1 WHERE condition;
UPDATE table1, table2 SET field1 = new_value1, field2 = new_value2 WHERE table1.id1 = table2.id2 AND condition;


Table Operations
sql
Copy code
CREATE TABLE table (field1 type1, field2 type2);
CREATE TABLE table (field1 type1, field2 type2, INDEX (field));
CREATE TABLE table (field1 type1, field2 type2, PRIMARY KEY (field1));
CREATE TABLE table IF NOT EXISTS;
CREATE TEMPORARY TABLE table;
DROP TABLE table;
DROP TABLE IF EXISTS table;
DROP TABLE table1, table2;
ALTER TABLE table MODIFY field1 type1;
ALTER TABLE table CHANGE old_name_field1 new_name_field1 type1;
ALTER TABLE table ADD new_name_field1 type1;
ALTER TABLE table DROP field1;
ALTER TABLE table ADD INDEX (field);
ALTER TABLE table ADD new_name_field1 type1 AFTER another_field;


Keys and Constraints
sql
Copy code
CREATE TABLE table (..., PRIMARY KEY (field1, field2));
CREATE TABLE table (..., FOREIGN KEY (field1, field2) REFERENCES table2 (t2_field1, t2_field2));


Users and Privileges
sql
Copy code
CREATE USER 'user'@'localhost';
GRANT ALL PRIVILEGES ON base.* TO 'user'@'localhost' IDENTIFIED BY 'password';
REVOKE ALL PRIVILEGES ON base.* FROM 'user'@'host';
FLUSH PRIVILEGES;
SET PASSWORD FOR 'user'@'host' = PASSWORD('new_pass');
DROP USER 'user'@'host';


Main Data Types
sql
Copy code
TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT;
FLOAT(M,D), DOUBLE(M,D);
TIME, YEAR, DATE, DATETIME, TIMESTAMP;
VARCHAR(size), TEXT, BLOB, ENUM('value1', 'value2', ...);


Reset Root Password
sh
Copy code
/etc/init.d/mysql stop;
mysqld_safe --skip-grant-tables;
mysql -u root;
UPDATE mysql.user SET password=PASSWORD('new_pass') WHERE user='root';
/etc/init.d/mysql start;