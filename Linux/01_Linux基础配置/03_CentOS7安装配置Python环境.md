### 安装Python环境
1. 安装编译相关工具
```
1. 安装开发库
yum -y groupinstall "Development tools"

2. 安装依赖环境
yum -y install zlib zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel

3. 安装libffi-devel
yum -y install libffi-devel
```

2. 创建Python文件夹下载包
```
1. 创建存放的文件夹
mkdir /usr/local/python3

2. 下载Python3.9安装包
cd /usr/local/python3 
wget https://www.python.org/ftp/python/3.9.0/Python-3.9.0.tgz

3. 解压
tar xf Python-3.9.0.tgz
```

3. 编译安装
```
1. 进入Python-3.9.0文件夹
cd /usr/local/python3/Python-3.9.0

2. 生成makefile文件
./configure prefix=/usr/local/python3 --with-ensurepip=install

3. 编译安装
make -j 4 && make install
```

4. 创建软链接
```
1. 将原有的python2链接备份
mv /usr/bin/python /usr/bin/python.bak

2. 添加python3软链接
ln -s /usr/local/python3/bin/python3.9 /usr/bin/python

3. 查看Python版本
python -V

4. 更改yum脚本的python依赖,因为其要用到python2才能执行,否则会导致yum不能正常使用
vim /usr/bin/yum 原：#!/usr/bin/python 改：#!/usr/bin/python2 
vim /usr/libexec/urlgrabber-ext-down 原：#! /usr/bin/python 改：#! /usr/bin/python2
```

5. 脚本一键安装
```
#!/bin/bash 
echo -e "\033[32m安装开发库,wait......\033[0m" 
yum -y groupinstall "Development tools" &> /dev/null 
echo ' ' 
echo -e "\033[32m安装依赖环境,wait......\033[0m" 
yum -y install zlib zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel wget &> /dev/null 
echo ' ' 
echo -e "\033[32m安装 libffi-devel,wait......\033[0m" 
yum -y install libffi-devel &> /dev/null 
echo ' ' 
mkdir -p /usr/local/python3 
echo -e "\033[32m下载 python3.9.0 源码包,wait......\033[0m" 
wget http://101.34.22.188/python/Python-3.9.0.tgz -P /usr/local/python3 &> /dev/null 
echo ' ' 
echo -e "\033[32m解压源码包,wait......\033[0m" tar xf /usr/local/python3/Python-3.9.0.tgz -C /usr/local/python3 &> /dev/null 
echo ' ' 
echo -e "\033[32m编译安装,wait......\033[0m" 
cd /usr/local/python3/Python-3.9.0 
./configure prefix=/usr/local/python3 --with-ensurepip=install &> /dev/null sleep 5 make &> /dev/null make install &> /dev/null sleep 5 
echo ' ' 
echo -e "\033[32m创建软连接,wait......\033[0m" 
mv /usr/bin/python /usr/bin/python.bak 
ln -s /usr/local/python3/bin/python3.9 /usr/bin/python 
echo ' ' 
echo -e "\033[32m更改 yum 脚本的 python 依赖,wait......\033[0m" 
sed -i 's/\#\!\/usr\/bin\/python/\#\!\/usr\/bin\/python2/' /usr/bin/yum 
sed -i 's/\#\! \/usr\/bin\/python/\#\! \/usr\/bin\/python2/' /usr/libexec/urlgrabber-ext-down 
echo ' ' 
echo -e "\033[33mPython3.9.0 安装成功\033[0m" 
echo -e "\033[32mPython3：python\033[0m" 
echo -e "\033[32mPython2：python2\033[0m"
```
### 配置Python虚拟环境
1. 安装虚拟环境支持包
```
yum install python-virtualenv -y  
pip3 install virtualenvwrapper
```

2. 修改系统环境变量
```
1. 编辑root目录下的 ‘.bashrc’ 文件
vim /root/.bashrc

2. 打开.bashrc文件添加内容如下
VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3  
export WORKON_HOME=$HOME/.virtualenvs  
source /usr/local/python3/bin/virtualenvwrapper.sh
```

3. 重新加载.bashrc文件
```
source /root/.bashrc
```
### Python虚拟环境操作
```
1. 创建虚拟环境
mkvirtualenv + 环境名称
mkvirtualenv cti_monitor  
指定虚拟环境python版本：mkvirtualenv --python=/usr/bin/python3 cti_monitor

2. 进入虚拟环境
workon + 环境名称
workon cti_monitor

3. 退出虚拟环境
deactivate

4. 删除虚拟环境
rmvirtualenv + 虚拟环境名称
rmvirtualenv cti_monitor

5. 复制虚拟环境  
cpvirtualenv + 虚拟环境名称
cpvirtualenv cti_monitor
```