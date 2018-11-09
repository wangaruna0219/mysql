# mysql
一·全查询
mysql> select * from shoppiing8;
+----+--------+-----+----------+-------+----------------+----------+------+
| id | name   | num | discount | xihao | 11wish         | isDelete | isOK |
+----+--------+-----+----------+-------+----------------+----------+------+
|  1 | shoes  |   2 | 0        | yes   | buy shoes      |        0 |    0 |
|  2 | waitao |   1 | 1        | no    | none           |        0 |    0 |
|  3 | kuzi   |   3 | 1        | yes   | buy basketball |        1 |    0 |
+----+--------+-----+----------+-------+----------------+----------+------+
二·查询不重复的记录
mysql> select distinct discount from shopping8;
+----------+
| discount |
+----------+
| 0        |
| 1        |
+----------+
2 rows in set (0.00 sec)
三·多条件查询
mysql> select * from shopping8 where isDelete=1;
+----+------+-----+----------+-------+----------------+----------+------+
| id | name | num | discount | xihao | 11wish         | isDelete | isOK |
+----+------+-----+----------+-------+----------------+----------+------+
|  3 | kuzi |   3 | 1        | yes   | buy basketball |        1 |    0 |
+----+------+-----+----------+-------+----------------+----------+------+
1 row in set (0.00 sec)

mysql> select * from shopping8 where isDelete!=1;
+----+--------+-----+----------+-------+-----------+----------+------+
| id | name   | num | discount | xihao | 11wish    | isDelete | isOK |
+----+--------+-----+----------+-------+-----------+----------+------+
|  1 | shoes  |   2 | 0        | yes   | buy shoes |        0 |    0 |
|  2 | waitao |   1 | 1        | no    | none      |        0 |    0 |
+----+--------+-----+----------+-------+-----------+----------+------+
2 rows in set (0.00 sec)

mysql> select * from shopping8 where isDelete!=1 and isOK=0;
+----+--------+-----+----------+-------+-----------+----------+------+
| id | name   | num | discount | xihao | 11wish    | isDelete | isOK |
+----+--------+-----+----------+-------+-----------+----------+------+
|  1 | shoes  |   2 | 0        | yes   | buy shoes |        0 |    0 |
|  2 | waitao |   1 | 1        | no    | none      |        0 |    0 |
+----+--------+-----+----------+-------+-----------+----------+------+
2 rows in set (0.00 sec)
四·排序和限制
（1）升序
mysql> select num from shopping8 order by num;
+-----+
| num |
+-----+
|   1 |
|   2 |
|   3 |
+-----+
3 rows in set (0.00 sec)
（2）降序
mysql> select num from shopping8 order by num desc;
+-----+
| num |
+-----+
|   3 |
|   2 |
|   1 |
+-----+
3 rows in set (0.00 sec)
（3）限制
mysql> select num from shopping8 order by num limit 3;
+-----+
| num |
+-----+
|   1 |
|   2 |
|   3 |
+-----+
3 rows in set (0.00 sec)

mysql> select num from shopping8 order by num limit 1;
+-----+
| num |
+-----+
|   1 |
+-----+
1 row in set (0.00 sec)

mysql> select num from shopping8 order by num limit 2,1；
+-----+
| num |
+-----+
|   3 |
+-----+
1 row in set (0.00 sec)

mysql> select num from shopping8 order by num limit 1,2;
+-----+
| num |
+-----+
|   2 |
|   3 |
+-----+
2 rows in set (0.00 sec)
五·聚合
mysql> select sum(num) from shopping8;
+----------+
| sum(num) |
+----------+
|        6 |
+----------+
1 row in set (0.00 sec) 

mysql> select num,sum(num) from shopping8 group by num;
+-----+----------+
| num | sum(num) |
+-----+----------+
|   2 |        2 |
|   1 |        1 |
|   3 |        3 |
+-----+----------+
3 rows in set (0.00 sec)

mysql> select count(*) from shopping8;
+----------+
| count(*) |
+----------+
|        3 |
+----------+
1 row in set (0.00 sec)

mysql> select count(num) from shopping8;
+------------+
| count(num) |
+------------+
|          3 |
+------------+
1 row in set (0.00 sec)



mysql> select count(distinct num) from shopping8;
+---------------------+
| count(distinct num) |
+---------------------+
|                   3 |
+---------------------+
1 row in set (0.00 sec)

mysql> select num,isOK,sum(num),count(isOK) from shopping8 group by num,isOK having num>1;
+-----+------+----------+-------------+
| num | isOK | sum(num) | count(isOK) |
+-----+------+----------+-------------+
|   2 |    0 |        2 |           1 |
|   3 |    0 |        3 |           1 |
+-----+------+----------+-------------+
2 rows in set (0.00 sec)

mysql> select num,isOK,sum(num),count(isOK) from shopping8 where num>1 group by num,isOK with rollup;
+-----+------+----------+-------------+
| num | isOK | sum(num) | count(isOK) |
+-----+------+----------+-------------+
|   2 |    0 |        2 |           1 |
|   2 | NULL |        2 |           1 |
|   3 |    0 |        3 |           1 |
|   3 | NULL |        3 |           1 |
| NULL | NULL |        5 |           2 |
+-----+------+----------+-------------+
5 rows in set (0.00 sec)
六·表连接
（1）内连接
mysql> select * from shopping;
+----+---------+------+
| id | name    | isOK |
+----+---------+------+
|  6 | warn    |    0 |
|  7 | warn100 |    0 |
|  8 | warn200 |    0 |
+----+---------+------+
3 rows in set (0.01 sec)
mysql> select * from shopping8;
+----+--------+-----+----------+-------+----------------+----------+------+
| id | name   | num | discount | xihao | 11wish         | isDelete | isOK |
+----+--------+-----+----------+-------+----------------+----------+------+
|  1 | shoes  |   2 | 0        | yes   | buy shoes      |        0 |    0 |
|  2 | waitao |   1 | 1        | no    | none           |        0 |    0 |
|  3 | kuzi   |   3 | 1        | yes   | buy basketball |        1 |    0 |
+----+--------+-----+----------+-------+----------------+----------+------+
3 rows in set (0.00 sec)
mysql> select * from shopping8,shopping where shopping8.isOK=shopping.isOK;
+----+--------+-----+----------+-------+----------------+----------+------+----+---------+------+
| id | name   | num | discount | xihao | 11wish         | isDelete | isOK | id | name    | isOK |
+----+--------+-----+----------+-------+----------------+----------+------+----+---------+------+
|  1 | shoes  |   2 | 0        | yes   | buy shoes      |        0 |    0 |  6 | warn    |    0 |
|  2 | waitao |   1 | 1        | no    | none           |        0 |    0 |  6 | warn    |    0 |
|  3 | kuzi   |   3 | 1        | yes   | buy basketball |        1 |    0 |  6 | warn    |    0 |
|  1 | shoes  |   2 | 0        | yes   | buy shoes      |        0 |    0 |  7 | warn100 |    0 |
|  2 | waitao |   1 | 1        | no    | none           |        0 |    0 |  7 | warn100 |    0 |
|  3 | kuzi   |   3 | 1        | yes   | buy basketball |        1 |    0 |  7 | warn100 |    0 |
|  1 | shoes  |   2 | 0        | yes   | buy shoes      |        0 |    0 |  8 | warn200 |    0 |
|  2 | waitao |   1 | 1        | no    | none           |        0 |    0 |  8 | warn200 |    0 |
|  3 | kuzi   |   3 | 1        | yes   | buy basketball |        1 |    0 |  8 | warn200 |    0 |
+----+--------+-----+----------+-------+----------------+----------+------+----+---------+------+
9 rows in set (0.00 sec)
（2）左连接
mysql> select * from shopping8 left join shopping on shopping8.id=shopping.id;
+----+--------+-----+----------+-------+----------------+----------+------+------+------+------+
| id | name   | num | discount | xihao | 11wish         | isDelete | isOK | id   | name | isOK |
+----+--------+-----+----------+-------+----------------+----------+------+------+------+------+
|  1 | shoes  |   2 | 0        | yes   | buy shoes      |        0 |    0 | NULL | NULL | NULL |
|  2 | waitao |   1 | 1        | no    | none           |        0 |    0 | NULL | NULL | NULL |
|  3 | kuzi   |   3 | 1        | yes   | buy basketball |        1 |    0 | NULL | NULL | NULL |
+----+--------+-----+----------+-------+----------------+----------+------+------+------+------+
3 rows in set (0.00 sec)
（3）右连接
mysql> select * from shopping8 right join shopping on shopping8.id=shopping.id;
+------+------+------+----------+-------+--------+----------+------+----+---------+------+
| id   | name | num  | discount | xihao | 11wish | isDelete | isOK | id | name    | isOK |
+------+------+------+----------+-------+--------+----------+------+----+---------+------+
| NULL | NULL | NULL | NULL     | NULL  | NULL   |     NULL | NULL |  6 | warn    |    0 |
| NULL | NULL | NULL | NULL     | NULL  | NULL   |     NULL | NULL |  7 | warn100 |    0 |
| NULL | NULL | NULL | NULL     | NULL  | NULL   |     NULL | NULL |  8 | warn200 |    0 |
+------+------+------+----------+-------+--------+----------+------+----+---------+------+
3 rows in set (0.00 sec)
mysql> select * from shopping right join shopping8 on shopping.id=shopping8.id;
+------+------+------+----+--------+-----+----------+-------+----------------+----------+------+
| id   | name | isOK | id | name   | num | discount | xihao | 11wish         | isDelete | isOK |
+------+------+------+----+--------+-----+----------+-------+----------------+----------+------+
| NULL | NULL | NULL |  1 | shoes  |   2 | 0        | yes   | buy shoes      |        0 |    0 |
| NULL | NULL | NULL |  2 | waitao |   1 | 1        | no    | none           |        0 |    0 |
| NULL | NULL | NULL |  3 | kuzi   |   3 | 1        | yes   | buy basketball |        1 |    0 |
+------+------+------+----+--------+-----+----------+-------+----------------+----------+------+
（4）子查询
(1)IN
mysql> select * from shopping;
+----+---------+------+
| id | name    | isOK |
+----+---------+------+
|  6 | warn    |    0 |
|  7 | warn100 |    0 |
|  8 | warn200 |    0 |
+----+---------+------+
3 rows in set (0.01 sec)
mysql> select * from shopping8;
+----+--------+-----+----------+-------+----------------+----------+------+
| id | name   | num | discount | xihao | 11wish         | isDelete | isOK |
+----+--------+-----+----------+-------+----------------+----------+------+
|  1 | shoes  |   2 | 0        | yes   | buy shoes      |        0 |    0 |
|  2 | waitao |   1 | 1        | no    | none           |        0 |    0 |
|  3 | kuzi   |   3 | 1        | yes   | buy basketball |        1 |    0 |
+----+--------+-----+----------+-------+----------------+----------+------+
select * from shopping where shopping.isOK in (select isOK from shopping8);
+----+---------+------+
| id | name    | isOK |
+----+---------+------+
|  6 | warn    |    0 |
|  7 | warn100 |    0 |
|  8 | warn200 |    0 |
+----+---------+------+
3 rows in set (0.00 sec)
（2）EXISTS
mysql> select * from shopping where exists(select isOK from shopping8 where isOK=0);
+----+---------+------+
| id | name    | isOK |
+----+---------+------+
|  6 | warn    |    0 |
|  7 | warn100 |    0 |
|  8 | warn200 |    0 |
+----+---------+------+
3 rows in set (0.00 sec)
七·合并两个不同的字段（也可以是不同表的相同字段)
mysql> select id from shopping union all select name from shopping8;
+--------+
| id     |
+--------+
| 6      |
| 7      |
| 8      |
| kuzi   |
| shoes  |
| waitao |
+--------+
6 rows in set (0.00 sec)

mysql> select name from shopping union all select name from shopping8;
+---------+
| name    |
+---------+
| warn    |
| warn100 |
| warn200 |
| kuzi    |
| shoes   |
| waitao  |
+---------+
6 rows in set (0.00 sec)
   ————GOOD LUCK!
