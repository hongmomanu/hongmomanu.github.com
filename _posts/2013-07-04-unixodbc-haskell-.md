---
layout: post
title: "unixodbc haskell 设置"
description: ""
category: linux 
tags: [linux,bash]
---

* unixodbc 配置


-> 丢弃的配置/**-export TWO_TASK=//address:1521/orcl
->   --这个环境变量必须的，我想也许是个bug


* 中文问题
标签： unixodbc it oracle	分类： SQL数据库
1，下载
   unixODBC-2.3.1，
   oracle-instantclient11.2-basic-11.2.0.3.0-1，
   oracle-instantclient11.2-odbc-11.2.0.3.0-1，
   oracle-instantclient11.2-sqlplus-11.2.0.3.0-1

2，假设oracle安装时选择了utf8字符集，或者客户端数据为UTF8字符集
   安装unixODBC：
   ./configure --sysconfdir=/etc --prefix=/usr --enable-iconv=yes --with-iconv-char-enc=UTF8
   make
   make install

  安装oracle客户端包
* 如果用connectstring 则
-> connectODBC ("Driver={/opt/instantclient/libsqora.so.11.1};Uid=user;Pwd=password;Dbq=host"))
* 如果用本地test ，则/etc/odbc.ini配置文件如下
[ORACLE]
Driver=/opt/instantclient/libsqora.so.11.1
ServerName =address:1521/orcl
UserID=username
password=password

* 测试命令 isql ORACLE
sudo ln -s libodbcinst.so.x  libodbcinst.so.1
   --如果你没有libodbcinst.so.1 ，可以用libodbcinst.so.x 做的软连接 /usr/lib64/ 下

* haskell demo

import Database.HDBC
import Database.HDBC.ODBC

getTestR :: Handler Html
getTestR = do
    liftIO $ print 123
    let connectionString =
            "Driver={/opt/instantclient/libsqora.so.11.1};Uid=username;Pwd=password;Dbq=host"
    let ioconn = connectODBC connectionString
    conn <- liftIO $ ioconn
    vals <- liftIO $ quickQuery conn "SELECT count(*) FROM tablename" []
    liftIO $ print vals
    error "Not yet implemented: getTestR"



{% include references.md %}
