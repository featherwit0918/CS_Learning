1. 下载CentOS7资源
	阿里云: https://mirrors.aliyun.com/centos/

2. 检测虚拟机网络是否可用
```
ping www.baidu.com
如果出现 Name or service not known 证明网络不可用
```

3. 配置虚拟机网络
```
vi /etc/sysconfig/network-scripts/ifcfg-ens33
```

```
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static    # 改成static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
UUID=4a989729-a4e5-473d-b691-91e3c513e2a2
DEVICE=ens33

ONBOOT=yes             # 设置yes打开网关
IPADDR=192.168.38.20   # 设置ip地址
GATEWAY=192.168.38.1   # 设置网关
NETMASK=255.255.255.0  # 设置子网掩码
DNS1=8.8.8.8           # 设置DNS地址
```

4. 重启网络
```
systemctl restart network
```


> 说明: Mac端获取子网掩码与网关
> ```
> 1. 获取子网掩码
> cat /Library/Preferences/VMware\ Fusion/vmnet8/nat.conf | grep netmask
   netmask = 255.255.255.0
> 2. 获取网关
> cat /Library/Preferences/VMware\ Fusion/vmnet8/nat.conf | grep "ip =" -B 1
   ip = 192.168.38.1
```