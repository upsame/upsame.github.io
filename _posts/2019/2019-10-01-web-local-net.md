---
layout: post
title: 内网web服务器搭建以及访问方式
category: it
tags: [it]
excerpt: 内网web服务器搭建以及访问方式
---

> 原创
## 内网服务器搭建
> 系统环境：windows 7 sp1 x86

> 局域网IP：192.168.0.203

> 配置环境：使用软件 phpstudy pro 小皮系统（包含了 php 环境和 Apache 等环境）；
> 使用开源私有云系统 KodExplorer 。

搭建方法：
1. 打开 phpstudy pro，开启 Apache或Nginx 功能，使用默认端口80，最好设置为开机自启；
2. 将KodExplorer解压缩，文件拷贝到D:/phpstudy_pro/www/文件夹下，在Phpstudy_pro软件中设置网站的物理路径为D:/phpstudy_pro/WWW/kodexplorer ，其他设置为默认不变。
3. 在另一台局域网内主机使用浏览器访问192.168.0.203，可以登陆KodExplorer 系统。

**Ps:** 可以注意到phpstudy pro平台中还可以开启FTP服务、MySQL服务，需要设置为其他端口。


## 内网服务映射到公网
1、最简单的方式是将192.168.0.203对应的主机设置为DMZ主机，一般路由器都有这个功能。

2、路由器上进行端口映射，比第一种方式更安全且更灵活；

3、花生壳软件，首先在官网注册账号，然后在局域网某台电脑（比如192.168.0.203）上安装花生壳软件并运行后登陆花生壳官网注册的账号即可。不需要进行后续的映射配置。

**本次使用的是方法1，将192.168.0.203设置DMZ主机**

DMZ主机相当于拥有路由器的公网IP，因此访问公网IP就等于访问DMZ主机。而对于内网，DMZ主机的IP仍然是192.168.0.203 ，内网主机可以通过192.168.0.203访问DMZ，也可以通过公网IP访问DMZ。
![image0](http://openshare.zicp.vip/index.php?explorer/fileProxy&accessToken=d21ejVGD4gVXnx9KOxMeoXMdBvlFXNZSol2GZBISu5b4HW80T2IsZGSoVDI0vRZOkqjv6ts8yQ&path=%2Fdocument%2Fupsame.com%2Fimages%2F2019%2Fdmz-setting.JPG)


## 直接使用IP访问
内网访问：http://192.168.0.203 	或	外网访问：http://139.48.164.169	
> 后者是路由器获得的公网IP。由于DMZ主机默认开放了所有端口，所以远程桌面、NAS文件夹分享都可以通过公网IP进行访问。

## 使用域名访问
两种方式，
- 一种是进行域名注册和DNS解析，将域名与绑定IP实现访问；
- 另一种是使用花生壳的壳域名在路由器或电脑端进行设置即可访问。

### 域名注册和DNS解析方式
1. 腾讯云或者在新网上购买 yourname.xyz 的域名一年使用权，需要实名认证；`截至到目前2019年10月这两个网站都在搞活动，域名可以几乎免费使用1年`。
2. 添加DNS解析，腾讯云或者新网平台上设置域名解析，将域名解析到公网IP上 。
3. 使用域名搭建网站需要进行备案，目前没有备案。主要是指连接使用国内云服务器需要备案，内网搭建的服务器有自己的IP，不用备案。

### 花生壳的壳域名实现DDNS解析
通常路由器都可以进行DDNS的配置，如图是路由器 padawan 系统下的设置方法，其余路由器类似：
![image1](http://kdyun.upsame.com/data/User/admin/home/document/upsame.com/images/2019/web-local-net2.png )

在路由器上设置的花生壳账号并登陆后，所以可以通过使用壳域名进行访问，如使用 http://openshare.zicp.vip 访问服务。

**需要注意：**
1、路由器的端口映射与DMZ主机不冲突，端口映射的优先级更高，即优先对映射的端口进行转发，然后剩余的（没有设置端口映射）的端口都自动转发到DMZ主机上。

2、当设置的端口不是浏览器默认的80端口时，访问需要加上对应的端口号
比如：139.48.164.169:8080

## 知识梳理

路由器端口交互图：
![image2](http://kdyun.upsame.com/data/User/admin/home/document/upsame.com/images/2019/web-local-net1.png )
