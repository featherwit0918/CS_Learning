1. 检查当前系统是否自带MySQL相关程序文件
```
1. 检测已经安装的mariadb列表(rpm命令是RPM软件包的管理工具)
rpm -qa | grep mariadb

2. 然后执行删除
rpm -e --nodeps mariadb-libs-5.5.56-2.el7.x86_64 
```

2. 安装MySQL
```
1. 更新yum源
yum update

2. 下载wget命令
yum -y install wget

3. 在线下载MySQL安装包
wget https://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm

4. 安装MySQL
rpm -ivh mysql57-community-release-el7-8.noarch.rpm

5. 安装MySQL服务
yum -y install mysql-server

```
> 说明: 安装中可能会出现的问题
>   失败的软件包是：mysql-community-libs-compat-5.7.39-1.el7.x86_64  
>   GPG  密钥配置为：file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
>   解决方案:
>   rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
>   然后再重新安装


3. 启动MySQL
```
1. 启动MySQL
systemctl start mysqld

2. 获取临时密码
grep 'temporary password' /var/log/mysqld.log

3. 登录MySQL
mysql -uroot -p

4. 修改MySQL的密码校验强度改为低风险(不修改密码必须有特殊字符)
set global validate_password_policy=LOW;

5. 修改MySQL的密码长度(默认是12位)
set global validate_password_length=6;

6. 修改MySQL密码
ALTER USER 'root'@'localhost' IDENTIFIED BY '123456'; 
```

4. MySQL开启允许远程访问
```
1. 关闭防火墙
sudo systemctl disable firewalld

2. 在Linux系统中的防护火墙放行端口
firewall-cmd --add-port=3306/tcp --zone=public --permanent

3. 重启防火墙
systemctl restart firewalld

4. 查看端口是否被放行
firewall-cmd --list-port

5. 登录MySQL
mysql -uroot -p

6. 切换到MySQL数据库
use mysql;

7. 查看user表
select Host,User from user;

8. 修改root用户权限为允许任何地址访问
update user set HOST="%" where User="root";

9. 刷新权限
flush privileges;
```