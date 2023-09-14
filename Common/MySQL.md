# MySQL

## 安装

```shell
sudo apt update
sudo apt install mysql-server
```

## 配置基本设置

```shell
sudo mysql
```

设置密码

```mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';
FLUSH PRIVILEGES;
```

接下来登录方式即为

```shell
sudo mysql -u root -p
```

## 配置远程连接

```bash
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
```

找到以`bind-address`开头的行，并将其值设置为MySQL服务器应监听的IP地址。默认情况下，该值设置为`127.0.0.1`即仅在本地主机中监听。

在此示例中，我们将值更改为`0.0.0.0`，将MySQL服务器设置为监听所有IPv4地址。

```mysql
CREATE USER 'root'@'%' IDENTIFIED BY 'some_pass';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';
FLUSH PRIVILEGES;
```

重启

```shell
sudo systemctl restart mysql
```

## 修改密码

本地和远程

```
ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';
ALTER USER 'root'@'%' IDENTIFIED BY 'new_password';
```

