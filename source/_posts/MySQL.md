title: MySQL Notes
date: 2014-08-15
categories: MySQL
tags: [MySQL]
---
MySQL 备忘，已经用到的一些命令，方式信马游缰。一句话总结：那些我用到的MySQL语句。

## MySQL
``` SQL shell登录，‘-u’用户‘root’；‘-p’需要密码。
$ mysql -u root -p
```

### New db
* Create database
```sql
create database db_name;
```

* Add user
```mysql
insert into mysql.user(Host,User,Password) \
values("localhost","user_name",password("user_password"));
```

* Show user
```mysql
select user,host,password from mysql.user; 
```

* Add permission
```mysql
grant all privileges on db_name.* to \
user_name@localhost identified by 'user_password';
flush privileges;
```

* Show permission
```mysql
show grants for user_name@'localhost';
```

* Alter character (utf-8)
```mysql
alter database db_name default character set = utf8;
```

* Recommend create
```mysql
CREATE database db_name DEFAULT CHARACTER SET utf8;
```

## Other

* foreign_key_checks
```mysql 一对好基友
set foreign_key_checks = 0;
$_do_some_command;
set foreign_key_checks = 1;
```

* show databases
```mysql
show databases;
```

* use databases
```mysql
use db_name;
```

* truncate table
```mysql 清空表中所有内容，结构不变化:
truncate table table_name;
```

* drop table
```mysql 销毁表，结构不复存在:
drop table table_name;
```

* update
```mysql
update db_name.table_name set column_name = new_value where id>0 and your_where
```
id>0 我是被那个safe update逼的。

## End: 本文仅总结了我用到的一些语句。
注：代码命令中含有`_`的，很多时候是需要你修改的。但也有不是的，如`set xx_xx = 0`，你需要修改`0 or 1`。
