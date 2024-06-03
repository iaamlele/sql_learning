
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

