# library-online
$make --version

$sudo apt-get install libpq-dev

$sudo apt-get install postgresql postgresql-contrib

$service postgresql

$service postgresql status

$creatdb mybd3

$dropdb mydb3

$sudo su postgres

$psql

postgresql=#\l

postgresql=#\du

USER CREATION,PASSWORD CHANGE,ATTRIBUTE,DROP:

postgresql=#ALTER USER postgres WITH PASSWORD 'test123';

postgresql=#CREATE USER hammad WITH PASSWORD 'test122';

postgresql=#ALTER USER hammad WITH SUPERUSER;

postgresql=#DROP USER hammad;

CREATE DATABASE,SCHEMA,DELETE,INSERT,DROP,TRUNCATE

postgresql=#CREATE DATABASE mydb3;

postgresql=#CREATE SCHEMA mydb3schema;

postgresql=#CREATE TABLE mydb3schema.table1(id integer,password char(10)); 

postgresql=#select * from pg_catalog_tables;

postgresql=#select * from pg_catalog_tables where schemaname='mydb3schema';

postgresql=#INSERT into mydb3schema.table1 values(1,'1');

postgresql=##TRUNCATE mydb3schema.table1;

postgresql=#DELETE FROM mydb3schema.table1;

DROP TABLE mydb3schema.table1;

Created Library_Management database

Then Created Tables

Library_Management=# \d
             List of relations
 Schema |     Name      |   Type   | Owner  
--------+---------------+----------+--------
 public | books         | table    | hammad
 public | departments   | table    | hammad
 public | employees     | table    | hammad
 public | issued        | table    | hammad
 public | issued_id_seq | sequence | hammad
 public | students      | table    | hammad
(6 rows)

Library_Management=# select * from books;
 id |             title             | cost 
----+-------------------------------+------
  1 | Essence of life               |  250
  2 | Life of Pie                   |  300
  3 | Peter Pan                     |  400
  4 | Thugs of Hindustan            |  200
  5 | No Mans Land                  |  420
  6 | Hamlet                        |  420
  7 | The Tempest                   |  500
  8 | The Great Gatsby              |  550
  9 | A Passage To India            |  480
 10 | To Kill A Mockingbird         |  600
 11 | Don Qiexote                   |  650
 12 | Anna Karenina                 |  520
 13 | One Hundred Years of Solitude |  900
(13 rows)

Library_Management=# select * from departments;
 id | name 
----+------
  1 | CSE
  2 | ME
  3 | EE
  4 | CE
  5 | ECE
  6 | NE
  7 | MEE
(7 rows)

Library_Management=# select * from employees;
 id |      name      | salary 
----+----------------+--------
  1 | bob            |  20000
  2 | frank          |  30000
  3 | zoro           |  25000
  4 | sanji          |  18000
  5 | robin          |  45000
  6 | edward newgate |  50000
  7 | shanks         |  32000
  8 | stella         |  22000
  9 | luffy          |  28000
(9 rows)

Library_Management=# create table issued(id int primary key,employee_id int references employees(id),student_id int references students(id),book_id int references books(id),date_of_issue DATE DEFAULT CURRENT_DATE,date_of_return DATE);
 id | employee_id | student_id | book_id | date_of_issue | date_of_return 
----+-------------+------------+---------+---------------+----------------
  1 |           2 |          4 |       2 | 2018-07-31    | 
  2 |           1 |          6 |       7 | 2018-07-31    | 
  3 |           5 |          4 |       2 | 2018-07-31    | 
  4 |           2 |          8 |       4 | 2018-07-31    | 
  5 |           1 |          2 |       1 | 2018-07-31    | 
(5 rows)

Library_Management=# select * from students;
 id |   name   | roll_no | department_id | class 
----+----------+---------+---------------+-------
  1 | nami     |    3017 |             1 | VIII
  2 | chopper  |    3018 |             2 | VI
  3 | franky   |    3019 |             4 | III
  4 | brook    |    1011 |             6 | v
  5 | buggy    |    4011 |             2 | I
  6 | marshall |    3001 |             1 | VIII
  7 | kaido    |    4012 |             2 | I
  8 | kakashi  |    3016 |             1 | VIII
(8 rows)


Library_Management=# select * from issued;
 id | employee_id | student_id | book_id | date_of_issue | date_of_return 
----+-------------+------------+---------+---------------+----------------
  1 |           2 |          4 |       2 | 2018-07-31    | 
  2 |           1 |          6 |       7 | 2018-07-31    | 
  3 |           5 |          4 |       2 | 2018-07-31    | 
  4 |           2 |          8 |       4 | 2018-07-31    | 
  5 |           1 |          2 |       1 | 2018-07-31    | 
(5 rows)

Library_Management=# select * from issued join employees on issued.employee_id = employees.id;
 id | employee_id | student_id | book_id | date_of_issue | date_of_return | id | name  | salary 
----+-------------+------------+---------+---------------+----------------+----+-------+--------
  1 |           2 |          4 |       2 | 2018-07-31    |                |  2 | frank |  30000
  2 |           1 |          6 |       7 | 2018-07-31    |                |  1 | bob   |  20000
  3 |           5 |          4 |       2 | 2018-07-31    |                |  5 | robin |  45000
  4 |           2 |          8 |       4 | 2018-07-31    |                |  2 | frank |  30000
  5 |           1 |          2 |       1 | 2018-07-31    |                |  1 | bob   |  20000
(5 rows)

Library_Management=# select * from issued join employees on issued.employee_id = employees.id join books on issued.book_id = books.id;
 id | employee_id | student_id | book_id | date_of_issue | date_of_return | id | name  | salary | id |       title        | cost 
----+-------------+------------+---------+---------------+----------------+----+-------+--------+----+--------------------+------
  1 |           2 |          4 |       2 | 2018-07-31    |                |  2 | frank |  30000 |  2 | Life of Pie        |  300
  2 |           1 |          6 |       7 | 2018-07-31    |                |  1 | bob   |  20000 |  7 | The Tempest        |  500
  3 |           5 |          4 |       2 | 2018-07-31    |                |  5 | robin |  45000 |  2 | Life of Pie        |  300
  4 |           2 |          8 |       4 | 2018-07-31    |                |  2 | frank |  30000 |  4 | Thugs of Hindustan |  200
  5 |           1 |          2 |       1 | 2018-07-31    |                |  1 | bob   |  20000 |  1 | Essence of life    |  250
(5 rows)

Library_Management=# select * from issued join employees on issued.employee_id = employees.id join books on issued.book_id = books.id join students on issued.student_id = students.id;
 id | employee_id | student_id | book_id | date_of_issue | date_of_return | id | name  | salary | id |       title        | cost | id |   name   | roll_no | department_id | class 
----+-------------+------------+---------+---------------+----------------+----+-------+--------+----+--------------------+------+----+----------+---------+---------------+-------
  1 |           2 |          4 |       2 | 2018-07-31    |                |  2 | frank |  30000 |  2 | Life of Pie        |  300 |  4 | brook    |    1011 |             6 | v
  2 |           1 |          6 |       7 | 2018-07-31    |                |  1 | bob   |  20000 |  7 | The Tempest        |  500 |  6 | marshall |    3001 |             1 | VIII
  3 |           5 |          4 |       2 | 2018-07-31    |                |  5 | robin |  45000 |  2 | Life of Pie        |  300 |  4 | brook    |    1011 |             6 | v
  4 |           2 |          8 |       4 | 2018-07-31    |                |  2 | frank |  30000 |  4 | Thugs of Hindustan |  200 |  8 | kakashi  |    3016 |             1 | VIII
  5 |           1 |          2 |       1 | 2018-07-31    |                |  1 | bob   |  20000 |  1 | Essence of life    |  250 |  2 | chopper  |    3018 |             2 | VI
(5 rows)

Library_Management=# select * from issued join employees on issued.employee_id = employees.id join books on issued.book_id = books.id join students on issued.student_id = students.id where students.id=8;
 id | employee_id | student_id | book_id | date_of_issue | date_of_return | id | name  | salary | id |       title        | cost | id |  name   | roll_no | department_id | class 
----+-------------+------------+---------+---------------+----------------+----+-------+--------+----+--------------------+------+----+---------+---------+---------------+-------
  4 |           2 |          8 |       4 | 2018-07-31    |                |  2 | frank |  30000 |  4 | Thugs of Hindustan |  200 |  8 | kakashi |    3016 |             1 | VIII
(1 row)


Library_Management=# select * from students order by case when name in('nami','chopper') THEN 1 ELSE 0 END ASC;
 id |   name   | roll_no | department_id | class 
----+----------+---------+---------------+-------
  8 | kakashi  |    3016 |             1 | VIII
  6 | marshall |    3001 |             1 | VIII
  7 | kaido    |    4012 |             2 | I
  3 | franky   |    3019 |             4 | III
  4 | brook    |    1011 |             6 | v
  5 | buggy    |    4011 |             2 | I
  2 | chopper  |    3018 |             2 | VI
  1 | nami     |    3017 |             1 | VIII
(8 rows)

Library_Management=# select title,(100*cost)/1000 AS "Greater" from books where (100*cost)/1000 >50;
             title             | Greater 
-------------------------------+---------
 The Great Gatsby              |      55
 To Kill A Mockingbird         |      60
 Don Qiexote                   |      65
 Anna Karenina                 |      52
 One Hundred Years of Solitude |      90
(5 rows)







