# VMware安装CentOS7



 <br/>

## 一.创建虚拟机

<br/>

第1步：首先安装VMware Workstation，只需点下一步即可，安装过程在另一篇中有

<br/>

第2步：文件 → 新建虚拟机 或 直接点击 创建新的虚拟机 图标

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent11.jpg)

 <br/><br/><br/>

第3步：选择 典型（推荐）→ 下一步

<br/>

 ![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent10.jpg)

 <br/><br/><br/>

第4步：稍后安装操作系统

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent7.tmp.jpg) 

<br/><br/><br/>

第5步：选择操作系统和版本

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent4.jpg) 

 <br/><br/><br/>

第6步：输入虚拟机名称和安装路径

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent3.jpg) 

 <br/><br/><br/>

第7步：设置磁盘大小

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent1.jpg) 

<br/><br/><br/>

第8步：自定义硬件

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent2.jpg) 

<br/><br/><br/>

第9步：选择CentOS安装镜像文件

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent14.jpg) 

<br/><br/><br/>

第10步：点击完成

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent6.jpg) 

<br/><br/><br/>

第11步：启动虚拟机，如果出现服务启动失败的提示，

在桌面右击我的电脑，点击管理，进入服务，找到VMmare Authorization Service右击，点重新启动或启动，

再重新启动虚拟机

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent8.jpg) 

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent16.png" alt="image-20211001210331268" style="zoom:80%;" />



<br/><br/><br/><br/><br/><br/><br/><br/>





## 二.配置CentOS7

<br/>

CentOS7与centOS6安装不同，但配置界面为大同小异，只是将原来一个一个的窗口集合到了一起，方便配置。

<br/>

1.选择**Install CentOS 7**,就是亮的地方，上下键可以调整

<br/>

![image-20211001210623173](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent17.png)

<br/><br/><br/>

2.进入配置界面

注：我们其实配一个界面，一个网络就可以了，后面的一些软件在需要什么的时候直接在网上找一下就可以找到，输入几行代码就可以下载。

相对于CentOS6来说，CentOS7简单了很多，我们根据中文就可以知道他们都是做什么的，

这里面的配置的可以根据自身需求进行安装，

<br/>

（1）选择需要安装的软件

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent25)

<br/><br/><br/>



选择 Server with Gui，然后点击Done

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent24.jpg)

<br/>

<br/>

<br/>

（2）点击网络和主机，将以太网打开

<br/>

![image-20211001211011026](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent18.png)



<br/>

![image-20211001211114178](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent19.png)

<br/><br/><br/>

3.弄完后点击开始安装，进入root配置界面

<br/>

4.配置root和创建用户

<br/>



![image-20211001211511017](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent21.png)

![image-20211001211220090](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcnet20.png)

![image-20211001211555910](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent22.png)

<br/><br/><br/><br/>

5.配置完成后重启即可

<br/><br/><br/><br/><br/><br/><br/><br/>

## 三.创建虚拟机（和上面一样）

<br/>

第1步：首先安装VMware Workstation，只需点下一步即可，安装过程略

<br/>

第2步：文件 → 新建虚拟机 或 直接点击 创建新的虚拟机 图标

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent62.jpg)

 

<br/><br/><br/>

第3步：选择 典型（推荐）→ 下一步

<br/>

 ![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent61.jpg)

 <br/><br/><br/>

第4步：稍后安装操作系统

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent60.jpg) 

<br/><br/><br/>

第5步：选择操作系统和版本

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent59.jpg) 

 <br/><br/><br/>

第6步：输入虚拟机名称和安装路径

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent58.jpg) 

 <br/><br/><br/>

第7步：设置磁盘大小

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent30.jpg) 

<br/><br/><br/>

第8步：自定义硬件

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent31.jpg) 

<br/><br/><br/>

第9步：选择CentOS安装镜像文件

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent32.jpg) 

<br/><br/><br/>

第10步：点击完成

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent33.jpg) 

<br/><br/><br/>

第11步：启动虚拟机

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent34.jpg) 

<br/><br/><br/>

<br/><br/><br/><br/><br/><br/>

## 四.配置CentOS6

第12步：选择第一项，安装全新操作系统或升级现有操作系统

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent35.jpg) 

<br/><br/><br/>

第13步：Tab键进行选择，选择Skip，退出检测

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent36.jpg) 

<br/><br/><br/>

第14步：点击Next

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent37.jpg) 

 

 <br/><br/><br/>

 

第15步：选择语言，这里选择的是中文简体

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent38.jpg) 

<br/><br/><br/>

第16步：选择键盘样式

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent39.jpg) 

<br/><br/><br/>

第17步：选择存储设备

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent53.jpg) 

<br/><br/><br/>

如果以前安装过虚拟机，会出现这个警告，选择是，忽略所有数据

<br/><br/><br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent55.jpg) 

<br/><br/><br/>

第18步：输入主机名

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent63.jpg) 

<br/><br/><br/>

第19步：配置网络

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent56.jpg) 

<br/><br/><br/>

第20步：设置时区，勾选使用UTC时间

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent40.jpg) 

<br/><br/><br/>

第21步：输入根用户（root）的密码

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent68.jpg) 

<br/><br/><br/>

如果密码过于简单会出现提示，点击无论如何都使用

<br/><br/><br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent41.jpg) 

<br/><br/><br/>

第22步：根据此Linux具体功能，选择不同的方式

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent42.jpg) 

<br/><br/><br/>

第23步：选择现在自定义，自定义安装需要的软件，如桌面配置

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent43.jpg) 

<br/><br/><br/>

可以根据具体的情况来配置，如可安Eclipse

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent44.jpg) 

<br/><br/><br/>

还可以安装Java平台、Perl支持等

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent45.jpg) 

<br/><br/><br/>

选择语言支持

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent46.jpg) 

<br/><br/><br/>

第24步：点击下一步，开始安装

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent47.jpg) 

<br/><br/><br/>

第25步：安装完成后，点击重新导引

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent48.jpg) 

<br/><br/><br/>

第26步：点击前进按钮

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent49.jpg) 

<br/><br/><br/>

第27步：点击是，同意许可，再点击前进按钮

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent50.jpg) 

<br/><br/><br/>

 

 

 

 

第28步：创建用户

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent51.jpg) 

<br/><br/><br/>

第29步：设置日期和时间，如果可以上网，勾选在网上同步日期和时间

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/vmcent52.jpg) 

<br/><br/><br/>

最后点击前进，完成安装！

