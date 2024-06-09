# 前提紧要
col：代表列
SELECT：找什么
FROM：从哪个table找
WHERE：col条件是什么
# 条件：数字(where)
当查找条件是数字
SELECT * FROM table WHERE col=1;

| Operator | Condition | SQL Example | Explain |
| --- | --- | --- | --- |
| =,!=,>,>=,<,<= | Standard numerical operators | col!=4 | 等于，大于，小于 |
| BETWEEN.. AND .. | Number is within range of two values(inclusive) | col BETWEEN 1 AND 10 | 在x和y之间 |
| NOT BETWEEN.. AND .. | Number is not within range of two values(inclusive) | col NOT BETWEEN 1 AND 10 | 不在x和y之间 |
| IN(...) | Number exists in a list | col IN(1,3,5) | 在x集合 |
| NOT IN(...) | Number does not exists in a list | col NOT IN (1,3,5) | 不在x集合 |


# 条件：文本(where)
当查找条件是文本
SELECT * FROM table WHERE col like '%you';

| Operator | Condition | SQL Example | Explain |
| --- | --- | --- | --- |
| = | Case sensitive exact string comparison (notice the single equals) | col="abc" | 等于 |
| != or <> | Case sensitive exact string inequality comparison | col!="abc" | 不等于 |
| LIKE | Case insensitive exact string comparison  | col LIKE "ABC" | 等于 |
| NOT LIKE | Case insensitive exact string inequality comparison | col NOT LIKE "ABC" | 不等于 |
| % | Used anywhere in a string to match a sequence of zero or more characters (only with LIKE or NOT LIKE) | col LIKE "%AT%" (matches "AT", "ATTIC", "CAT" or even "BATS") | 模糊匹配 |
| _ | Used anywhere in a string to match a single character (only with LIKE or NOT LIKE) | col LIKE "AN_" (matches "AND", but not "AN") | 模糊匹配单字符 |
| IN(...) | String exists in a list | col IN ("A", "B", "C") | 在集合 |
| NOT IN(...) | String does not exist in a list | co NOT IN ("D", "E", "F") | 不在集合 |


# 排序(rows)
| Operator | Condition | SQL Example | xplain |
| --- | --- | --- | --- |
| ORDER BY | - | ORDER BY col ASC/DESC | 按col排序 |
| ASC | - | ORDER BY col ASC/DESC | 升序 |
| DESC | - | ORDER BY col ASC/DESC | 降序 |
| LIMIT OFFSET | - | LIMIT num_limit OFFSET num_offset | 从offset取limit |
| ORDER BY | - | ORDER BY col1 ASC,col2 DESC | 多列排序 |


# join:连表(table)
当查找的数据在多张关联table里
SELECT * FROM table1 left join table2 on table1.id=table2.id where col>1

| Operator | Condition | SQL Example | Explain |
| --- | --- | --- | --- |
| JOIN..ON | - | t1 JOIN t2 ON t1.id=t2.id | 按ID连成一个表 |
| INNER JOIN | - | t1 INNER JOIN t2 ON t1.id=t2.id | 只保留id相等的row |
| LEFT JOIN | - | t1 LEFT JOIN t2 ON t1.id=t2.id | 保留t1的所有row |
| RIGHT JOIN | - | t1 RIGHT JOIN t2 ON t1.id=t2.id | 保留t2的所有row |
| IS/IS NOT NULL | - | col IS/IS NOT NULL | col是不是为null |


# 算式(select/where)
当需要对select的col或where条件的col经过一定计算后才能使用
SELECT *,col*2 from table where col/2>1

| Operator | Condition | SQL Example | Explain |
| --- | --- | --- | --- |
| +-*/% | - | col1+col2 | col加减乘除 |
| substr | - | substr(col,0,4) | 字符串截取 |
| AS | - | col * 2 AS col_new | col取别名 |
| ... | 
 | 
 | 还有很多 |

# 其他小知识+遇到的问题
## 1.workbench连接mysql
> 1.本地操作：
> a.登录mysql：sudo mysql -u root -p
> 密码为123
> b.创建账户,注意，每个语句后面要有分号，密码都是1352963880Cl@：
> -- 创建一个新用户 'newuser' 并允许从任何主机连接
> CREATE USER 'newuser'@'%' IDENTIFIED BY 'newpassword';
> -- 赋予新用户所有权限
> GRANT ALL PRIVILEGES ON *.* TO 'newuser'@'%' WITH GRANT OPTION;
> -- 刷新权限
> FLUSH PRIVILEGES;
> c.重启mysql服务
> sudo systemctl restart mysql
> 2.workbench


## 2.编译与链接：
> 有mysql编译和链接时，要添加库选项：gcc -o a a.c -lmysqlclient

## 3.建表时 PK NN UQ B UN ZF AI G的含义
> PK:作为主键
> NN:非空
> UQ: 不能重复
> BIN: 存放二进制数据的列
> UN:无符号数据类型
> ZF: 填充0位（例如指定3位小数，整数18就会变成18.000）
> AI: 自增长
> G:数据库中这一列由其他列计算而得

## 4.sql语句中数据库和表名引用是符号``
> UPDATE `new_schema`.`book` SET `Bcount` = `Bcount`+'%d' WHERE (`ISBN` = '123')
> 输入法让我打不出这个符号。。

## 5.mysql_query()
> int mysql_query(MYSQL *mysql, const char *query)
> 正常情况下，字符串必须包含1条SQL语句，而且不应为语句添加终结分号（‘;’）或“\g”
> 如果查询成功，返回0。如果出现错误，返回非0值


## 6.Mysql错误：Commands out of sync; you can't run this command now
> 常发生在使用 MySQL C API 时。当你在执行新的查询之前，前一个查询的结果集没有被正确处理或者释放时，就会出现这个错误。
> 正确流程：
> 1.mysql_query(con, query1)
> 2.MYSQL_RES *result = mysql_store_result(con);
> 3.MYSQL_ROW row;
>     int num_rows = mysql_num_rows(result);
>     row = mysql_fetch_row(result) //获取结果集的每一行
> 4.mysql_free_result(result);


## 7.浮点数的存储和比较
> 浮点数在数据库中存储时可能会有精度误差，直接进行等值比较会失败，使用近似比较方法：
> ABS(Price-32.3)


## 8.段错误 (核心已转储)--代码检查思路
> 1.检查是否没有free malloc/mysql_free_result(result)/mysql_close(con);
> 2.检查是否有情况导致以上语句不执行

