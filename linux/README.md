# linux系统常用命令

## 一、常用目录

```shell
/ 根目录
/root root用户的家目录
/home/username 普通用户的家目录
/etc 配置文件目录
/bin 命令目录
/sbin 管理命令目录
/user/bin/usr/sbin 系统预装的其他命令
```

------



##  二、帮助命令

##### 1、man 是 manual 的缩写

演示：

```shell
# man ls
# man 章节（1-7） man 例如 # man 1 ls
```



##### 2、shell(命令解释器)自带的命令称为内部命令，其他的是外部命令

- 内部命令使用help帮助

```shell
# help cd
```

- 外部命令使用help帮助

```shell
# ls --help
```

注:可以使用 # type 别名 来判断是内部命令还是外部命令

```shell
# type ls
```



##### 3、info帮助比help更详细，作为help的补充

```shell
# info ls
```

------



## 三、文件管理

##### 1、pwd 显示当前的目录名称

```shell
# pwd
```



##### 2、cd 更改当前的操作目录

```shell
# cd /path/to/... 绝对路径
# cd ./path/to/... 相对路径
# cd ../path/to/... 相对路径
```



##### 3、ls 查看当前目录下的文件

```shell
# ls [选项,选项...] 参数...

常用参数：
· -l 长格式显示文件
· -a 显示隐藏文件
· -r 逆序显示
· -t 按照时间顺序显示
· -R 递归显示
· -h 显示内容大小（以M单位形式）
```



##### 4、mkdir 建立目录

```shell
# mkdir [选项] 参数

常用参数：
· -p 建立多级目录
```



##### 5、删除空目录

```shell
rmdir 删除空目录
rm -r 删除非空目录
```



##### 6、复制文件

cp 复制文件和目录

```shell
· cp [选项] 文件路径
· cp [选项] 文件... 路径

常用参数：
· -r 复制目录 
· -p 保留用户、权限、时间等文件属性
· -a 等同于 -dpR
```



##### 7、移动文件

mv 移动文件

```shell
· mv [选项] 源文件 目标文件
· mv [选项] 源文件 目录
```

 

##### 8、删除文件

rm 删除文件

```shell
常用参数：
· -r 删除目录（包括目录下的所有文件）
· -f 删除文件不进行提示
ps：rm命令可以删除多个目录，需谨慎使用
```



##### 9、查看文件权限的方法

- 查看文件权限

  ```shell
  · -rw------1 root root 1523 sep 28 12:25 anaconda-ks.cfg
   _ ________ ___________                 _______________
  类型   权限   所属用户和组                       文件名
  
  · -rw-r-xr--1 username groupname mtime filename
  	· rw-  文件属主的权限
  	· r-x  文件属组的权限
  	· r--  其他用户的权限
  · 创建新文件有默认权限，根据umask值计算，属主和属组根据当前进程的用户来设定
  ```

- 文件类型

  ```shell
  · - 普通文件
  · d 目录文件
  · b 块特殊文件
  · c 字符特殊文件
  · l 符号链接
  · f 命名管道
  · s 套接字文件
  ```

- 文件权限的表示方式

  ```shell
  · 字符权限表示方法
  	· r 读
  	· w 写
  	· x 执行
  
  · 数字权限的表示方法
  	· r=4
  	· w=2
  	· x=1
  ```

- 目录权限的表示方法

  ```shell
  · x   进入目录
  · rx  显示目录内的文件名
  · wx  修改目录内的文件名
  ```



##### 10、修改权限命令

- chmod 修改文件、目录权限

  ```shell
  # chmod u+x /tmp/testfile
  # chmod 755 /tmp/estfile
  ```

  ```shell
  chmod u g o a
  · u 修改属主权限
  # chmod u+x file // 增加权限
  · g 修改属组权限
  # chmod g-r file // 删除权限
  · o 修改其他用户权限
  # chmod o=w file // 赋予权限
  · a 修改全部权限
  # chmod a+x file
  ```

  

- chown 更改属主、属组

  ```shell
  · 修改属主
  	# chown user1 /test
  · 修改属组
  	# chown :group /test
  ```

- chgrp   可以单独更改属组，不常用

  ```shell
  # chgrp group /test
  ```



##### 11、特殊权限

- SUID  用于二进制可执行文件，执行命令时取得文件属主权限
  -  如 /usr/bin/passwd
- SGID 用于目录，在该目录下创建新的文件和目录，权限自动更改为该目录的属组
- SBIT  用于目录，该目录下新建的文件和目录，仅 root 和自己可以删除
  -  如 /tmp

------



## 四、文本查看命令

##### 1、常用文本查看命令 

- cat 文本内容显示到终端

- head 查看文件开头

- tail 查看文件结尾

  ·常用参数 -f 文件内容更新后，显示信息同步更新

- wc 统计文件内容信息



## 五、打包与压缩

##### 1、 tar 打包与压缩命令

```shell
常用参数：
· c 打包
· x 解包
· f 指定操作类型为文件
· z gzip格式（压缩快、压缩率低）
· j bzip2格式（压缩慢、压缩率高）

例：
# tar czf 源文件（/tmp/etc-backup.tar.gz） 目标文件（/etc）
# tar cjf 源文件（/tmp/etc-backup.tar.bz2） 目标文件（/etc）
```



## 六、多模式文本编辑器

##### 1、四种模式

- 正常模式（Normal-mode）
- 插入模式（Insert-mode）
- 命令模式（Command-mode）
- 可视模式（Visual-mode）



##### 2、正常模式常用命令集合

```shell
· hjkl 左上下右
· a 在光标后一位开始插入
· A 在当前行最后一位开始插入
· o 在当前行下一行插入
· O 在当前行上一行插入
· r 替换光标所在字符
· dd 删除当前光标所在行
· x 删除光标后一位
· d + 上下左右 可删除上下行或左右单个字符
· u 撤销
· ctrl + r 重做（撤回撤销）
· shift + ^ 跳到光标当前行首
· shift + $ 跳到光标当前行尾
· yy 复制当前行
· 数字 + yy 复制当前光标所在位置及往下n行（# 3 yy 复制当前光标所在行开始往下三行）
· y + $ 复制光标当前位置至最后位置
· dd 剪切当前行
· 数字 + dd 剪切当前光标所在位置及往下n行（# 3 dd 剪切当前光标所在行开始往下三行）
· d + $ 剪切光标当前位置至最后位置
· p 粘贴
· gg 回到第一行
· GG 回到最后一行
· 数字 + gg 回到数字所在行（23 + gg 回到23行）
```



##### 3、命令模式常用命令集合

```shell
· ?查找字符 可查找需要查找的字符（# ?test 查找文本中含有test字符位置)
· n 向下查询查找的字符
· N 向上查询查找的字符
· s/old/new 替换当前行old字符更换为new字符（#s/test/test1 将当前行test字符更换为test1字符）
· %s/old/new 替换当前文本中第一个old字符更换为new字符（# %s/test/test1/g 将当前文本中第一个test字符更换为test1字符）
· %s/old/new/g 替换当前文本中所有old字符更换为new字符（# %s/test/test1/g 将当前文本中所有test字符更换为test1字符）
· 数字,数字/old/new 替换当前文本指定行数第一个old字符更换为new字符（# 3,5s/test/test1 将当前文本中第三行到第五行中第一个test字符替换成test1） 
· 数字,数字/old/new/g 替换当前文本指定行数所有old字符更换为new字符（# 3,5s/test/test1/g 将当前文本中第三行到第五行中所有test字符替换成test1） 
· set nu 显示行数
· set nonu 不显示行数
```



##### 4、可视模式

- 三种进入可视模式的方法

  ```shell
  · v 字符可视模式
  · V 行可视模式
  · ctrl + v 块可视模式
  	·配合d和I命令可以进行块的便利操作
  ```

------



## 七、用户与权限管理

##### 1、用户管理常用命令

- useradd [用户名]  新建用户

  ```shell
  # useradd username 新建username用户
  
  注:可使用 -g 在新建用户时直接分组
  	# useradd -g group1 user1 新建user1用户并加入group1组中
  ```

- id [用户名]  查询该用户是否存在以及所在组

  ```shell
  # id username 查询username是否存在以及所在组
  ```

- passwd [用户名]  修改用户密码

  ```shell
  # passwd username 修改username密码
  ```

- userdel [用户名] 删除用户

  ```shell
  # userdel username 删除username用户
  
  注：
   · -r 删除用户并删除用户家目录等数据
  # userdel -r username 删除username账户所有信息包括路径
  ```

- usermod [选项] [用户名]  修改用户属性

  ```shell
  常用参数：
  · -a 将用户增加到附件组。只能和 -G 选项一起使用。
  · -c 用户密码文件中注释字段的新值。
  · -d 用户的新登录目录（修改新的用户家目录地址）。
  	· usermod -d [路径] [用户名]
  	# usermode -d /home/w1 w
  · -e 用户账户将被禁用的日期。
  · -g 将用户修改进某个用户组
  	· usermod -g [用户组名] [用户名]
  	# usermod -g group1 user1
  ```

-  chage [选项] [用户名]  修改用户属性



##### 2、组管理命令

-  groupadd [用户组名]  新建用户组

  ```shell
  # groupadd group1 新增group1用户组
  ```

- groupdel [用户组名]  删除用户组

  ```shell
  # groupdel group1 删除group1用户组
  ```



##### 3、用户切换

- su 切换用户

  - su - username 使用 login shell 方式切换用户

- sudo 以其他用户身份执行命令

  - visudo 设置需要使用sudo的用户（组）

    ```shell
    # visudo 根据提示修改需要增加的用户以及授权特殊命令
    ```



##### 4、常用配置路径

-  /etc/passwd  用户配置信息文件（登录是否需要密码、uid、guid、家目录路径等配置）
-  /etc/shadow  用户配置信息文件（加密后的密码、权限等）
-  /etc/group 用户组配置信息文件

------



## 八、网络管理

##### 1、网络状态查看工具

1. net-tools

   - ifconfig

     ```shell
     · eth0 第一块网卡 （网络接口）
     · 你的第一个网络接口可能叫做下面的名字
     	· eno1 板载网卡
     	· ens33 PCI-E网卡
     	· enp0s3 无法获取物理信息的PCI-E网卡
     	· CentOS 7 使用了一致性网络设备命名，以上都不匹配则使用eth0
     ```

   - route

   - netstat

2. iproute2

   - ip
   - ss

##### 2、网络接口命名修改

- 网卡命名规则受biosdevname和net.ifnames两个参数影响

- 编辑 /etc/default/grub 文件，增加 biosdevname=0 net.ifnames=0

- 更新 grub

  ```shell
  # grub2-mkconfig -o /boot/grub2/grub.cfg
  ```

- 重启

  \# reboot

|       | biosdevname | net.ifnames | 网卡名 |
| :---: | :---------: | :---------: | :----: |
| 默认  |      0      |      1      | ens33  |
| 组合1 |      1      |      0      |  em1   |
| 组合2 |      0      |      0      |  eth0  |



##### 3、查看网络情况

- 查看网卡物理连接情况

  ```shell
  # mii-tool eth0
  ```

- 查看网关

  ```shell
  # route -n
  · 使用 -n 参数不解析主机名
  ```



##### 4、网络配置命令

-  ifconfig <接口>  <IP地址> [ netmask 子网掩码 ]

-  ifup <接口>

-  ifdown <接口>

  

##### 5、网关配置命令

-  route add default gw <网关ip>
- route add -host <指定ip> gw<网关ip>
- route add -net <指定网段> netmask <子网掩码> gw <网关ip>



##### 6、网络命令集合：ip命令

- ip addr ls
  - ifconfig
- ip link set dev eth0 up
  - ifup eth0
- ip addr add 10.0.0.1/24 dev eth1
  - ifconfig eth1 10.0.0.1 netmask 255.255.255.0
- ip route add 10.0.0/24 via 192.168.0.1
  - route add -net 10.0.0.0 netmask 255.255.255.0 gw 192.168.0.1



##### 7、网络故障排除命令

-  ping
-  traceroute
-  mtr
-  nslookup
-  telnet
-  tcpdump
-  netstat
-  ss



##### 8、网络服务管理

- 网络服务管理程序分为两种，分别为SysV和systemd
  - service network start|stop|restart
  - chkconfig-list network
  - systemctl list-unit-files NetworkMannager.service
  - systemctl start|stop|restart NetworkManger
  - systemctl enable|disable NetworkManger



##### 9、网络配置文件

- ifcfg-eth0   //网卡配置文件
- /etc/hosts  //主机配置文件
