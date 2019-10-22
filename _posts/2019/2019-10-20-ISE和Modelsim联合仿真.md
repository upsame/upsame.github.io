---
layout: post
title: ISE和Modelsim联合仿真
category: FPGA
tags: [FPGA]
excerpt: ISE和Modelsim联合仿真
---


# ISE和Modelsim联合仿真

相信很多人会遇到过这个问题，不知如何让ISE调用Modelsim进行仿真。我也迷糊了不少时间，查查找找，终于弄明白了，所以有了本文，和大家分享一下。我尽量讲得详细点儿，多多上图。

 **我的环境：**
 > Windows 7 64位，Xilinx ISE Design Suite 13.4（D:\Xilinx\13.4），ModelsimSE-64 10.1a（D:\modeltech64_10.1a， 哈，也是64位的）。不过32位的和64位的设置几乎没有什么区别。
 > 先安装好ISE和Modelsim， 网上看过一些文章总说先装ISE再装Modelsim，不过我整过一阵，其实二者的顺序是无关紧要的。
 > 安装过程不在本文的讨论范围内，就不多说了，不过一定要注意版本要合适，Modelsim的版本不要太低，这个可以自己到网上查一查，还有非常重要的一点是安装路径不能有中文或空格。

## 编译仿真库
由于我装的Modelsim SE是通用版的，只自带了少许的仿真库（Simulation Library），所以还要编译一下Xilinx的仿真库。只有XE才自带Xilinx的仿真库，如果装的是XE版便不必编译仿真库了。编译库可以用ISE带界面的工具，也可以用命令行下的，前者方便，先讲前者。
> 打开编译库工具“Simulation Library Compilation Wizard”：“开始—所有程序—Xilinx ISE Design Suite 13.4（版本不同就不同）—ISE Design Tools—64-bit Tools（32位的选32-bit Tools）—Simulation Library Compilation Wizard”。
> 注意，64位系统中默认安装了64位和32位的ISE，如果你想用32位的ISE，那你就得选32位的编译库工具，不能混着用的，而且Modelsim也得装上32位的版本，所以我建议64位系统的就用64位的ISE，而32位系统的没得选，只能用32位的。如图01所示。

![图01](https://bc2.net/assets/image/2019/ISE-Modelsim-pic1.png)

> 打开工具之后，在“Select Simulator”下面选中你所装好的Modelsim版本，我这儿选“Modelsim SE”，在“Simulator Executable Location”下面填入Modelsim.exe的所在的文件夹，点“Browse…”按钮添加也行，我这儿是“D:\modeltech64_10.1a\win64”（不含双引号，下同，除非有特别的说明），如图02，然后Next。
![图02](https://s2.ax1x.com/2019/10/21/K1ygMQ.png)

> 之后是选择需要编译的语言，选“Both VHDL and Verilog”，一般两种都要用，如图03，然后Next。
![图03](https://s2.ax1x.com/2019/10/21/K1yIiV.png)


> 接下来是选择设备，默认是全选，如果有一些你实在用不上就不选吧，这样可以省点时间和硬盘空间，全选时挺大条的，如图04，还是Next。

![04](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni0zNjgwNTBhODMxYzFkZTkx?x-oss-process=image/format,png)

> 下一步默认就行，全选上，下面的两行东东留空即可，那是添加额外库的，第一行是路径，第二行是命令参数，无视之。如图05，Next。

![05](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1lZmNlYTU4ODMwNGEyZTNj?x-oss-process=image/format,png)

> 这一步比较关键，在“Output directory for compiled libraries”下面填入输出已编译库的路径，默认也行。个人建议新建一个单独的文件夹，好管理，只要版本一样的，下次直接拿来用，重装也不怕。不过文件夹的名字和整个路径中绝对不能有中文或空格，切记、切记！！！我这儿是“D:\modeltech64_10.1a\Xilinx_lib”。其他的选项默认便可，之后点“Launch Compiled Process”，如图06。之后就开始编译了，如图07。其实这一页是很有用处的，详情请点下面的那个“More Info”按键，不过帮助是英文的。

![06](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1lOTQyNTNhMTQwZTM1OWZj?x-oss-process=image/format,png)

![07](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1iNDk3Zjc4NjFhYzY0MTY1?x-oss-process=image/format,png)

> 等待……编译完后就会出现一些编译日志，图08，Next，图09，Finish。只要没有Err就成，Warn无视。若有Err，就回顾下版本对不对，路径有没有中文或空格。
![08](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1lNzllMWQwYjBkOGJjZmUw?x-oss-process=image/format,png)
![09](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1mNzI5OTdkN2RhMDczZTMx?x-oss-process=image/format,png)

## 设置ISE和Modelsim的关联。
在“D:\Xilinx\13.4\ISE_DS\ISE”文件夹中找到“modelsim.ini”，“D:\Xilinx\13.4”这个是你的ISE安装目录，后半路径是一样的，实在不行就进入安装目录然后搜索“modelsim.ini”，如图2.1。

![2.1](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1lMWI5ZjI0YTNkM2EzYjEy?x-oss-process=image/format,png)

>  打开“modelsim.ini”，用记事本打开时不要用自动换行功能，菜单中“格式—自动换行”把勾去掉。个人不建议用记事本，写字板那就更不行了，有的文件用写字板改了会出现问题，搞编程类的总得有个好点儿的文本编辑工具吧，我用的是EmEditor，到网上搜一下吧，有不少呢。在第九行左右（可能是）找到“[Library]”，下面一行的“others = $MODEL_TECH/../modelsim.ini”和行的开头的分号（；）的全部都无视。那些行开头没有分号的，格式一般是“X···X = 路径”，一直到“[vcom]”之上的都要，选的仿真库多时可有好长的一段，全部复制。见图12、图13和图14。

![12](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1iZWEwMmM1YWNkNTQ1OGU4?x-oss-process=image/format,png)
![13](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1mMzU2NzIxMjAwYTMzOWI2?x-oss-process=image/format,png)
![14](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni0wMTAyZDU5YTAwYTc3MDc0?x-oss-process=image/format,png)
> 然后在Modelsim的安装目录下，我这儿是“D:\modeltech64_10.1a”，找到“modelsim.ini”，名字一样。先去换个文本编辑工具吧，用记事本打开它会是乱糟糟的一片，没法改。打开后，同样是找到“[Library]”，在它的下面粘贴上刚刚复制的那一大段东西，注意，行开头不要有分号（；），而且人家原有的就别动它，别删掉了。只要在“[Library]”和“[vcom]”之间粘贴就行，然后保存。如图15、图16和图17。

![15](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni02ZGZkYWZjZGQyMDlhNjg3?x-oss-process=image/format,png)
![16](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1lMThkZTI4YjQ2NDEwOTAwLnBuZw?x-oss-process=image/format,png)

![17](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1iNjM1ZmU1OTI0NTg0Y2Q4?x-oss-process=image/format,png)
> 打开ISE，“开始—所有程序—Xilinx ISE Design Suite 13.4（版本不同就不同）—ISE Design Tools—64-bit Project Navigator（32位的就开32-bit Project Navigator）”，图18。
![18](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni02Mjk4MGU3ZGVhODI4Njc5?x-oss-process=image/format,png)

> 然后在ISE的菜单上“Edit—Preferences…”调出Preferences设置窗口，在左边的“Category”下选中“ISE General—Integrated Tools”。在Integrated Tools项设置中，右边的“Model Tech Simulator：”下面填入Modelsim.exe的文件路径，点旁边的“..”按键选中Modelsim.exe也行，我这儿是“D:\modeltech64_10.1a\win64\modelsim.exe”（不要双引号）。32位的可能是“D:\modeltech32_10.1a\win32\modelsim.exe”。如图19和图20。
![image](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1kOTdjNjAwMGE2ZDliNmQw?x-oss-process=image/format,png)
![image](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni03N2NjMTQ3ODA1NDE0ZTEx?x-oss-process=image/format,png)
![image](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni04MTU1YjlmZDEyMjAxMWZl?x-oss-process=image/format,png)

> 到现在已经把家伙准备好了，接下来就是使用它了。新建一个工程，图21，这步不多说，Next。
![image](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1jZDMxZjMyYzA4ZWYxZGY5?x-oss-process=image/format,png)
> 接下来这一步在“Simulator”一项选“Modelsim-SE Mixed”，“Mixed”支持两语言，“SE”是版本，选你自己对应的就成，其它项不讨论，如图22，Next，Finish。忘了选或想重新选的看图23。
![image](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1lYzFiNTUwMWM1M2IxM2Nm?x-oss-process=image/format,png)
![image](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1mMjEyNTg2MWMwNzNlM2Qz?x-oss-process=image/format,png)

> 新建你的VHDL或Verilog文件，这个不多说。
> 完成之后，切换到仿真模式，就是点工程上面的“Simulation”，可能不同版本会不一样，ISE9.1i 是在“Source for”的下拉菜单中选择Behavioral simulation，不过意思明白就行。建立Test Bench文件，若是VHDL的，也按上面说的处理一下，就是把那两个库声明一下。在“Hierarchy”框选中Test Bench文件，在下面的那个框中点“Modelsim Simulator”前的加号。展开得到“Simulate Behavioral Model”，在它上面点右键，选“Process Properties…”，如图27。
![image](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1jMWExMWEzZjc4YmJiOGEx?x-oss-process=image/format,png)

> 在“Simulate Behavioral Model”上点右键，选“Run”就可以调用Modelsim进行仿真了，如图30。另外提一点，在ISE上也可以编译库的。在仿真模式中，在“Hierarchy”框中选中FPGA名，我这儿是“xc7a8-3csg324”（下面就是仿真文件）。然后在下面的框中点“Design Utilities”前面加号。展开后得到“Compile HDL Simulation Libraries”，在其上点右键，选“Run”，这样就会编译你的工程中所需的仿真库了 。

## 成功案例
如下图，没有报错，ISE调用Modelsim正常。
![image](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTM4MzE4Ni1lMGFmNDVlOGE3OWY4NGM3?x-oss-process=image/format,png)