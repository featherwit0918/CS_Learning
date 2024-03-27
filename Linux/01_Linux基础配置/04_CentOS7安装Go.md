1. 下载Golang二进制包

首先, 到Golang官网([https://golang.org/dl/](https://golang.org/dl/))下载适用于Linux系统的二进制包。选择适合CentOS7操作系统的版本例如 "go1.22.1.linux-amd64.tar.gz"。  
打开终端界面, 使用wget命令下载Golang的二进制包:
```
wget https://dl.google.com/go/go1.22.1.linux-amd64.tar.gz
```

2. 解压Golang二进制包

下载完成后, 使用以下命令进行解压缩:
```
tar -C /usr/local -xzf go1.22.1.linux-amd64.tar.gz
```
解压完成后, Golang目录将位于 /usr/local/go 中

3. 设置Golang环境变量

在系统中设置Golang的环境变量。打开“/etc/profile”文件并添加以下行:
```
export PATH=$PATH:/usr/local/go/bin
```
在文件末尾加上这行命令, 该命令将/usr/local/go/bin目录添加到环境变量中
保存并退出“/etc/profile”文件。然后, 运行以下命令使其生效: 
```
source /etc/profile
```

4. 测试Golang的安装

运行以下命令来测试Goland安装是否成功
```
go version
```