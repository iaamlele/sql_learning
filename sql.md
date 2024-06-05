
# 其他小知识
## workbench连接mysql
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


## 编译与链接：
> 有mysql编译和链接时，要添加库选项：gcc -o a a.c -lmysqlclient


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
