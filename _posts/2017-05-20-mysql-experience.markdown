---
layout: post
title:  "MySQL experience!"
date:   2017-05-20
categories: database MySQL
---

* 目录
{:toc}

***

# 集群

## 主从复制

### 主从复制配置
0.环境
| 软件 | 信息 |
|:-----|:-----|
| OS | ubuntu server 16.04 |
| MySQL | 5.7.18-0ubuntu0.16.04.1-log |
| master | ip:192.168.73.129 |
| slave | ip:192.168.73.132 |

1.修改master配置
{% highlight shell %}
# /etc/mysql/my.cnf
# 配置组
[mysqld]
# 将mysql二进制日志取名为mysql-bin
log-bin=mysql-bin
# 二进制日志的格式，有三种：statement/row/mixed
binlog_format=mixed
# 为服务器设置一个独一无二的id便于区分，这里使用ip地址的最后一段充当server-id
server-id=129
{% endhighlight %}
重启MySQL
{% highlight shell %}
/etc/init.d/mysql restart
{% endhighlight %}
*此步骤出现的错误*   
**[ERROR] Found option without preceding group in config file /etc/mysql/my.cnf**  
因为没有配置组导致MySQL重启时报错 

2.修改slave配置
{% highlight shell %}
# /etc/mysql/my.cnf
# 配置组
[mysqld]
# 非必须
log-bin=mysql-bin
# 非必须
binlog_format=mixed
# 为服务器设置一个独一无二的id便于区分，这里使用ip地址的最后一段充当server-id
server-id=132
{% endhighlight %}
重启MySQL

3.在主服务器上建立帐户并授权slave
{% highlight shell %}
mysql>GRANT REPLICATION SLAVE ON *.* to 'root'@'%' identified by '123456';
# 一般不用root帐号，%表示所有客户端都可能连，只要帐号，密码正确，  
# 此处可用具体客户端IP代替，如192.168.73.132，加强安全。
{% endhighlight %}

4.登录master的mysql，查询master的状态
{% highlight shell %}
mysql>show master status;
+------------------+----------+--------------+------------------+-------------------+
| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
+------------------+----------+--------------+------------------+-------------------+
| mysql-bin.000001 |      450 |              |                  |                   |
+------------------+----------+--------------+------------------+-------------------+
1 row in set (0.00 sec)
{% endhighlight %}
执行完此步骤后不要再操作主服务器MYSQL，防止主服务器状态值变化

5.配置slave
{% highlight shell %}
mysql>change master to master_host='192.168.73.129',master_user='root',master_password='123456',master_log_file='mysql-bin.000001',master_log_pos=450; 

# 开启slave
mysql>start slave; 

# 检查slave复制功能状态
mysql> show slave status\G;
# 主要看下面这两行信息
...
Slave_IO_Running: Yes
Slave_SQL_Running: Yes
...
{% endhighlight %}
*此步骤出现的问题*  
**master连接不上**  
此时状态信息为  
Slave_IO_Running: Connecting  
检查是执行命令change master to master_host...时，IP设置错误，重新执行change master to master_host...，报错ERROR 3021 (HY000): This operation cannot be performed with a running slave io thread; run STOP SLAVE IO_THREAD FOR CHANNEL '' first.  
需要先停止slave复制，待重新执行命令后再开启  
mysql> stop slave;  
执行change master to master_host...  
mysql> start slave; 
  
**然后发现master仍旧是连接不上，运行命令关闭防火墙**  
{% highlight shell %}
ufw disable
{% endhighlight %}
然后在slave运行命令测试连接
{% highlight shell %}
mysql -h 192.168.73.129 -uroot -p
{% endhighlight %}
  
**报错mysql Access denied for user \'root\'**   
注释掉vim mysql.conf.d/mysqld.cnf文件的下面一行  
bind-address            = 127.0.0.1  
上面这句话限制只接受本机连接  
**之后报错The slave I/O thread stops because master and slave have equal MySQL server UUIDs**  
因为虚拟机是直接复制的，导致UUID一样，删除master的/var/lib/mysql/auto.cnf文件(重启MySQL会自动生成)  
在/var/lib/mysql目录下是因为在/etc/mysql/mysql.conf.d/mysqld.cnf中配置了  
datadir         = /var/lib/mysql  
重启后正常
