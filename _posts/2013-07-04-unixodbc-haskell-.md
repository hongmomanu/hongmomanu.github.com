---
layout: post
title: "unixodbc haskell 设置"
description: ""
category: linux 
tags: [linux,bash]
---

* unixodbc 配置
{% highlight bash %}
/**-export TWO_TASK=//address:1521/orcl
->   --这个环境变量必须的，我想也许是个bug
**/
如果用connectstring 则 connectODBC ("Driver={/opt/instantclient/libsqora.so.11.1};Uid=" ++ T.unpack(user) ++ ";Pwd=" ++ T.unpack(password) ++";Dbq=" ++ T.unpack(host)))
如果用本地test ，则/etc/odbc.ini配置文件如下
[ORACLE]
Driver=/opt/instantclient/libsqora.so.11.1
ServerName =192.168.2.141:1521/orcl
UserID=CIVILAFFAIRS_MZ_TZ_MATCH
password=hvit

测试命令 isql ORACLE

sudo ln -s libodbcinst.so.x  libodbcinst.so.1
>   --如果你没有libodbcinst.so.1 ，可以用libodbcinst.so.x 做的软连接 /usr/lib64/ 下
{% endhighlight %}

* haskell demo
{% highlight haskell %}
import Database.HDBC
import Database.HDBC.ODBC

getTestR :: Handler Html
getTestR = do
    liftIO $ print 123
    let connectionString = "Driver={/opt/instantclient/libsqora.so.11.1};Uid=username;Pwd=password"
    let ioconn = connectODBC connectionString
    conn <- liftIO $ ioconn
    vals <- liftIO $ quickQuery conn "SELECT count(*) FROM tablename" []
    liftIO $ print vals
    error "Not yet implemented: getTestR"

{% endhighlight %}


{% include references.md %}
