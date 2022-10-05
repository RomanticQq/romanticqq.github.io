---
title: Linux环境下搭建LAMP
tags:
  - Linux
  - LAMP
  - 服务器
  - php
categories: 后端
abbrlink: 8665
date: 2021-06-03 22:22:38
---
#### 安装Apache

1. 安装Apache

    ``` 
    yum install httpd -y
    ```

2. 启动服务

   ```
   service httpd restart
   ```

3. Apache服务开机启动

    ```
    chkconfig httpd on
    ```

4. Apache的配置文件

    ```
    /etc/httpd/conf/httpd.conf
    ```

5. 网站根目录

    ```
    /var/www/html/
    ```


#### 安装mysql

1. 安装mysql

   ```
   wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
   rpm -ivh mysql-community-release-el7-5.noarch.rpm
   yum install mysql-server
   ```

2. 启动mysql

    ```
    service mysqld restart
    ```

3. 首次登录mysql

    ```
    mysql 
    ```

4. 设置密码

    ```
    show databases;
    use mysql;
    select user,password from user;
    update user set password=password('root') where user='root';
    ```

5. mysql刷新权限命令

   ```
   flush privileges;
   ```

6. 再次登录mysql

    ```
    mysql -u root(用户名) -p
    root（密码）
    ```


#### 安装php

1. 安装php和连接php、mysql工具

    ```
    yum install php php-mysql
    ```

2. 启动Apache和mysql

    ```
    service httpd restart
    service mysqld restart
    ```

3. 测试php和mysql是否连接成功

    ```
    $link = mysql_connect('localhost','root','root');
    if($link){
    echo "successful";
    }else{
    echo "fail";
    }
    ```



#### 常见问题         

1. 报错Cannot find a valid baseurl for repo： base/7/86-64

    解决方案：
    ```
	cd /etc/sysconfig/network-scriptsls
	vim ifcfg-ens33
    ONBOOT=yes //修改,保存退出即可
   ```