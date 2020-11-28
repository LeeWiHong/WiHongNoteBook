### 1、新建用户 
创建test用户，密码是1234。

```
mysql -u root -p 
CREATE USER “test”@”localhost” IDENTIFIED BY “1234”; #本地登录 
CREATE USER “test”@”%” IDENTIFIED BY “1234”; #远程登录 
quit 
mysql -utest -p #测试是否创建成功
```
###2、为用户授权

a.授权格式：grant 权限 on 数据库.* to 用户名@登录主机 identified by “密码”;　
b.登录MYSQL，这里以ROOT身份登录：
`mysql -u root -p`
c.为用户创建一个数据库(testDB)：

```
create database testDB; 
create database testDB default charset utf8 collate utf8_general_ci;
```
d.授权test用户拥有testDB数据库的所有权限：

```
grant all privileges on testDB.* to “test”@”localhost” identified by “1234”; 
flush privileges; #刷新系统权限表
```
e.指定部分权限给用户:

```
grant select,update on testDB.* to “test”@”localhost” identified by “1234”; 
flush privileges; #刷新系统权限表
```
f.授权test用户拥有所有数据库的某些权限： 　

```
grant select,delete,update,create,drop on . to test@”%” identified by “1234”; #”%” 表示对所有非本地主机授权，不包括localhost
```

###3、删除用户

```
mysql -u root -p 
Delete FROM mysql.user Where User=”test” and Host=”localhost”; 
flush privileges; 
drop database testDB;
```
删除账户及权限：

```
drop user 用户名@’%’; 
drop user 用户名@ localhost;
```
###4、修改指定用户密码

```
mysql -u root -p 
update mysql.user set authentication_string=password(“新密码”) where User=”test” and Host=”localhost”; 
flush privileges;
```



