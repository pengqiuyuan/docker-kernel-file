# docker-kernel-file
Centos 6.5 kernel 2.6 升级到 kernel 4.4.7（longterm） 

## 环境：

```
　系统版本：Linux centos 2.6.32-573.12.1.el6.x86_64（Centos-6.5-x86_64-minimal.iso ）

　升级内核版本：longterm:4.4.7
```

## 查看系统内核版本：

```
[root@10 Dockerfiles]# uname -a
Linux 10.0.29.249 3.10.5-3.el6.x86_64 #1 SMP Tue Aug 20 14:10:49 UTC 2013 x86_64 x86_64 x86_64 GNU/Linux
[root@10 Dockerfiles]# cat /etc/redhat-release
CentOS release 6.5 (Final)
```

## 下载地址（kernel）：

```
[root@server-2 etc]# cd /usr/src/kernels/
[root@server-2 kernels]# wget https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.4.7.tar.xz
[root@server-2 kernels]# tar -xvf linux-4.4.7.tar.xz
[root@server-2 kernels]# cd linux-4.4.7
```
## 复制 .config文件：

```
[root@server-2 kernels]# git clone https://github.com/pengqiuyuan/docker-kernel-file.git
[root@server-2 linux-4.4.7]# cp ./docker-kernel-file/.config .
```

## 编译内核：
```
# make bzImage #生成内核文件
# make modules #编译模块
# make modules_install #安装模块
# make install #安装
 #编译并安装内核(j8代表8个线程同时编译，请根据你的机器情况设置）约30分钟
[root@server-2 linux-4.4.7]# make -j8 bzImage && make -j8 modules && make -j8 modules_install && make install

```
## 重启：
```
 reboot 
```

## 注意事项：
```
 # 重新编译内核请运行
 cd /usr/src/linux-3.12.17
 make mrproper
 make clean
```
