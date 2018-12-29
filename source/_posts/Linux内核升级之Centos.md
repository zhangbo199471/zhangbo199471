---
title: Linux内核升级之Centos
date: 2018-12-29 17:33:58
tags:
---

在工作或者学习中，很多时候我们需要用新的`linux`内核来验证一些前沿的技术或者功能，这个时候我们所用的`linux`内核太低的话，就需要升级内核了。以下整理了`Centos7`升级内核的过程。

到http://www.kernel.org下载需要升级的内核源码。最好选择稳定版本或者长期支持版。

##解压到`/usr/src`路径下

```bash
	tar -xvf linux-4.19.6.tar.xz -C /usr/src/
```
##切换路径

```bash
	cd /usr/src
```

##创建软连接

```bash
	ln -sv linux-4.19.6 linux
	cd linux
```

> **注意**:通常有很多应用程序比如额外编译驱动时都会到`/usr/src`下找，而且会到`/usr/src`下找`linux`的目录，而不是去找`linux-3.18.60`，因此我们需要去建立软连接。

##配置和编译内核

```bash
yum install ncurses-devel -y
yum install bison -y
make menuconfig     //配置内核 
make -j  20        //编译内核
make modules_install  //安装内核
make install
```

编译新内核完成后，系统默认启动的还是之前的内核，除非在系统启动的时候手动的选择。当然我们如果常用新的内核，也可以更改默认启动项。

##查看默认启动内核

```bash
grub2-editenv list
```

##查看所有内核

```bash
cat /boot/grub2/grub.cfg | grep menuentry
```
 
##修改默认内核

```bash
grub2-set-default 'CentOS Linux (4.19.6) 7 (Core)'
```

##验证默认启动内核

```bash
grub2-editenv list
```
