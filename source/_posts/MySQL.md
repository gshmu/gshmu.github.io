title: MySQL Notes
date: 2014-08-15
categories: MySQL
tags: [MySQL]
---
MySQL 备忘，已经用到的一些，方式信马游缰。一句话总结：那些我用到的MySQL语句。

## MySQL
`$ mysql -u root -p` shell登录，‘-u’用户‘root’；‘-p’需要密码。

## new db
代码命令中含有`_`的，很多时候是需要你修改的。但也有不是的，如`set xx_xx = 0`，你需要修改`0 or 1`。

### create database
`create database db_name;`

### New user
`insert into mysql.user(Host,User,Password) values("localhost","user_name",password("user_password"));`

### add permission
`grant all privileges on db_name.* to user_name@localhost identified by 'user_password';`

### alter character (utf-8)
`alter database db_name default character set = utf8;`

### recommend create
`CREATE database db_name DEFAULT CHARACTER SET utf8;`


## Other

### foreign_key_checks
`set foreign_key_checks = 0;` & `set foreign_key_checks = 1;`

### show databases
`show databases;`

### use databases
`use db_name;`

### truncate table
`truncate table table_name;`
清空表中所有内容，结构不变化。

### drop table
`drop table table_name;`
销毁表，结构不复存在。

### update
`update db_name.table_name set column_name = new_value where id>0 and your_where`
id>0 我是被那个safe update逼的。

## End: 本文仅总结了我用到的一些语句。
