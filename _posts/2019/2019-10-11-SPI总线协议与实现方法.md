---
layout: post
title: SPI 总线协议与实现方法
category: FPGA
tags: SPI FPGA
excerpt: SPI 总线协议与实现方法
---

> 原创
首发于我的个人博客 [www.upsame.com](https://www.upsame.com)

## SPI 总线协议与实现方法

### 知识储备---参看链接：
[https://www.cnblogs.com/deng-tao/p/6004280.html](https://www.cnblogs.com/deng-tao/p/6004280.html)

[https://blog.csdn.net/qq_42282258/article/details/81436882](https://blog.csdn.net/qq_42282258/article/details/81436882)


### 正在使用的模式3，如图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191011122423286.png)

- 发送端在时钟下降沿改变数据
- SCLK上升沿的阶段，数据保持稳定； 
- 接收端在时钟上升沿接受数据（对线上的数据进行读取）。


目前已经在FPGA K7平台上实现并验证了SPI通信协议。
代码可参看[FPGA实现SPI通信](https://blog.csdn.net/JustinLee2015/article/details/101925582)
