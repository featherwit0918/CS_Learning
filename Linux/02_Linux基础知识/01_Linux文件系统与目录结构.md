### Linux文件
Linux中一切皆文件
### Linux目录结构
![[../../Image/2592ebe6-ab15-4f0c-ad53-ee2724d0e984.jpeg]]

```
/bin
   这个目录存放着最常用的命令
   
/sbin
   这里存放的是系统管理员使用的系统管理程序
   
/boot
   这里存放的是启动Linux时使用的一些文件, 包括一些连接文件以及镜像文件
   
/dev
   该目录下存放的是Linux的外部设备,在Linux中访问设备的方式和访问文件的方式是相同的
   
/etc
   这个目录用来存放所有的系统管理所需要的配置文件和子目录
   
/home
   用户的主目录, 在Linux中, 每个用户都有一个自己的目录, 一般该目录名是以用户的账号命名的
   
/lib
   这个目录里存放着系统最基本的动态连接共享库, 其作用类似于Windows里的DLL文件。几乎所有的应用程序都需要用到这些共享库
   
/lib64
   64位相关的库会放在这
   
/media
   linux系统会自动识别一些设备, 例如U盘、光驱等等, 当识别后, Linux会把识别的设备挂载到这个目录下
   
/mnt
   系统提供该目录是为了让用户临时挂载别的文件系统的
   
/opt
   这是给主机额外安装软件所摆放的目录
   
/proc
   是一种伪文件系统(也即虚拟文件系统), 存储的是当前内核运行状态的一系列特殊文件, 这个目录是一个虚拟的目录, 它是系统内存的映射, 可以通过直接访问这个目录来获取系统信息。这个目录的内容不在硬盘上而是在内存里
   
/root
   该目录为系统管理员, 也称作超级权限者的用户主目录

/run
   运行目录

/srv
   该目录存放一些服务启动之后需要提取的数据

/sys
   虚拟文件系统, 和/proc/目录相似,该目录中的数据都保存在内存中,主要保存与内核相关的信息

/tmp
   这个目录是用来存放一些临时文件的

/usr
   用于存储系统软件资源

/var 
   用于存储动态数据，例如缓存、日志文件、软件运行过程中产生的文件等
```