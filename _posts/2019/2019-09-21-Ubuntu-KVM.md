---
layout: post
title: Ubuntu18.04中使用KVM
category: linux
tags: [linux]
excerpt: Ubuntu18.04中使用KVM
---

# Ubuntu18.04中使用KVM

首先，ubuntu本身就是一个虚拟机，是我在教研室的Windows 10电脑使用VMware Workstation创建的虚拟机，分配的内存为4G和双处理器+双核（一共应该是4个线程）。

我在这个Ubuntu虚拟机中又使用KVM创建了一个虚拟机，安装`Lite`操作系统。
按照网上的教材走，最开始鼠标不同步的问题，似乎有解决方案，但是应用后没有直接生效，可能是要重启虚拟机吧。之后第二天我来的时候开启虚拟机重装KVM 虚拟机时鼠标问题就没有了。然后安装正常。

KVM分配了10GB空间，分配了Ubuntu的两个核，1G内存。安装后使用了59%，运行还比较流畅。
感觉界面比Ubuntu更好用呢，很有windows的风格。如下：
![Lite 桌面截图](https://img-blog.csdnimg.cn/20190929105123493.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0p1c3RpbkxlZTIwMTU=,size_16,color_FFFFFF,t_70)
需要明确的是默认KVM中虚拟机和宿主机不能直接复制粘贴，需要一定的增强工具，但是不管了。

默认使用NAT方式联网，可以联网成功（打开了百度），网桥连接似乎有点问题，以后用到了再说吧。

所以要体验Lite linux，就可以再这个虚拟机下体验。（虚拟机中的虚拟机）。

对于KVM，基本的虚拟机功能都有，但是似乎没有VMware tool这样的好工具可以用。KVM只能运行于linux系统上，Virtualbox和VMware都可以跨平台。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190929105340136.png)

=================================================================================

KVM是一个集成的Linux解决方案，我发现用它创建的虚拟机响应速度不错，唯一的缺陷是少针对桌面解决方案的功能，如3D图形加速，或GUI管理工具，**所以用来搭服务器应该比较适用**。