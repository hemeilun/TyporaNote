# 一.Linux

<br/>

## （一）目录管理

<br/>

BIn:全称binary（二进制）,该目录中存储的是一些二进制文件，文件是可以被直接运行的。

<br/>

Dev:该目录主要存放的是外部设备。例如盘，光盘等，在其中外界的设备是不能被直接使用的，需要挂载（mnt下）。

<br/>

Etc:该目录主要存放一些配置文件。

<br/>

Home:表示除了root用户以外，其他用户的家，例如由用户aaa，就会有一个aaa文件夹。

<br/>

Proc:process表示进程，用来存储Linux现在在运行的进程。

<br/>

Root:root用户自己的家目录。

<br/>

Sbin:全称super binary,该目录和bin目录一样，但需要root用户才能执行。

<br/>

Timp:表示临时的，存储系统运行时产生的临时文件。

<br/>

Usr:存放的是用户自己安装的软件。

<br/>

Var:存放的程序/系统的日志文件。

<br/>

Mint:当设备需要挂在时，就需要挂载在此目录下。

<br/>

关机：shutdown -h now

<br/><br/><br/><br/><br/><br/><br/><br/>

## （二）指令

<br/>

### 1.指令和选项

<br/>

只要是在命令行中输入的信息就是指令

<br/>

指令格式：

**指令主体   【选项】【操作对象】**

一个指令可以包含多个选项，也可以包含多个操作对象

选项可以叠加，比如：ls -la，其中-a为一个单独的选项，-l为一个单独的选项

【】：表示可写可不写

<br/>

**注：指令如果不加路径就是当前文件夹**

<br/><br/><br/><br/>

<br/><br/><br/><br/>

### 2.基础指令

<br/>

#### （1）  ls

<br>

用法一：# ls

作用：列出当前目录下所有文件的名称

<br/>

用法二：# ls 路径名称

作用：列出指定目录下所有文件的名称

<br/>

用法三：# ls 选项  路径

- ls -l（可以简化为“ ll ”）

  作用：列出当前目录下所有文件的详细信息

- ls -a

  作用：列出当前目录下的所有文件（包含隐藏文件)

  

- ls -lh(使用时必须加上 l  )

  作用：使文件的大小具有较高的可读性

<br/><br/><br/>

#### （2） pwd

<br/>

作用：显示当前文件夹路径

<br/><br/><br/>

#### （3） cd 

<br/>

作用：切换路径

   用法：

- cd 相对或绝对路径

- cd ./【文件】

  作用：切换到当前目录下的文件   

- cd ../【文件】

  作用：切换到上一级目录下的文件

- cd /

  作用：切换到根目录

- cd ~

  作用：切换到当前用户的家目录

  

<br/><br/><br/><br/>

#### （4）mkdir

<br/>

用法一：# mkdir 文件夹名/路径文件夹名

作用：创建文件夹在指定路径下

<br/>

用法二：# mkdir -p  文件夹名/路径文件夹名

作用：递归创建文件夹，会将输入路径中所有文件夹都创建出来

<br/>

用法三：# mkdir 【-p】 文件名1 文件名2 ......

作用：一次性创建多个文件夹

<br/><br/><br/><br/>

#### （5）touch

<br/>

用法：# touch 文件名/路径文件名

作用：创建指定的文件

创建多个文件也是加空格就行

<br/><br/><br/><br/>

#### （6）cp

<br/>

作用：复制文件/文件夹

<br/>

用法一：# cp 被复制的文件名  要复制到的文件路径【修改后的文件名】

作用：将文件复制到指定的路径

<br/>

用法二：# cp -r  被复制的文件名/文件夹名  要复制到的文件夹路径【修改后的文件名】

作用：将文件夹中的所有文件（包括这个文件夹）复制到指定路径

<br/><br/><br/><br/>

#### （7）mv

<br/>

作用：移动文件/文件夹

<br/>

用法一：# mv 被移动的文件名  要移动到的文件路径【修改后的文件名】

作用：将文件移动到指定的路径

<br/>

用法二：# mv 文件名1/文件夹名1  文件名2/文件夹名2

作用：将文件1的名字改为文件2的名字

<br/><br/><br/><br/>

#### （8）rm

<br/>

用法：# rm 【选项】 文件名/文件夹名

作用：删除文件/文件夹

选项可为：

- rm -f  文件名

  作用：不询问，直接删除文件

- rm -r 文件夹名/文件名

  作用：删除文件夹时必须添加此选项

  

一般用法：# rm -rf 文件夹名/文件名

<br/><br/><br/><br/>

#### （9）vim

<br/>

用法：# vim 文件名

作用：打开文件

后面会有更具体的讲解

<br/><br/><br/><br/>

#### （10）输出重定向

<br/>

一般命令的输出都显示在命令行中，有时需要将一些命令的执行结果保存到文件中，用来后续的分析\统计，这个时候就需要使用重定向技术。

用法：# 正常查询  >  文件名称（文件不存在会自动创建）

例：# ll > usr/a.txt

" > "：覆盖输出，会覆盖掉原来的内容

” >> “：追加输出，会在原来数据的末尾进行添加

<br/><br/><br/><br/>

#### （11）cat

<br/>

用法一：# cat 文件名

作用：打开文件

<br/>

用法二：# cat 文件1 文件2 .... >  文件名

作用：将全面的几个文件合并到一个文件（本质就是把前面几个读出来，然后重定向到后面的那个文件里面）

<br/><br/><br/><br/>

#### （12）基础命令的小补充

<br/>

- ctrl+u：删除光标之前的内容

  ctrl+k：删除光标之后的内容

- 

<br/><br/><br/><br/><br/><br/><br/><br/>



### 3.进阶命令

<br/>

#### （1）df

<br/>

用法：# df -h

作用：查看磁盘空间，根据实际情况系统自动分配单位

如果不使用 -h 会以k为单位显示

要找到具体的文件系统，就到挂载点的文件夹中去找

<br/>

![image-20211002214216517](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux3.png)

<br/><br/><br/><br/>

#### （2）free

<br/>

用法：# free 【 -单位】

功能：查看内存使用情况

例：# free -m ，即以M为单位

<br/>

![image-20211002214133036](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux2.png)

<br/><br/>

swap是：用于系统的临时内存，当内存不够用的时候，就要用临时磁盘空间来充当内存

<br/><br/><br/><br/>

#### （3）head

<br/>

用法：# head 【-n】 文件名                   

【n为数字】

作用：显示一个文件的前n行数据，如果不指定行数，默认为10行

<br/><br/><br/><br/>

#### （4）tail

<br/>

用法：# tail 【选项】 文件名           

- -n【n为数字】

  作用：显示一个文件的末n行数据，如果不指定行数，默认为10行

- -f

  作用：通过tail来查看文件的动态变化（**变化的内容是不能手动添加的**）

  ​         此命令一般是用来查看系统日志。

退出只需按 q 即可

<br/><br/><br/><br/>

#### （5）less

用法：# less 文件名

作用：对文件进行查看，与cat有点类似

操作：下方“ ： ”是可以输入数字的。数字+回车：跳转到指定行。空格：翻页。上下键：调整当前行

​           按 q 退出

<br/>

![image-20211002222629236](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux4.png)

<br/><br/><br/><br/>

#### （6）wc

用法：# wc 【选项】 文件名

作用：不加选项会把行数，单词数，字节数依次输出

<br>

![image-20211002223418787](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux5.png)

<br/>

- -l

  作用：只输出行数

- -w

  作用：只输出单词数，单词以空格为区分，对汉字这个命令没有用。

- -c

  作用：只输出字节数

<br/><br/><br/><br/>

#### （7）date

<br/>

用法一：# date 

作用：显示日期，类似于 xxxx年  xx月  xx日  星期x  HH:MM:SS  CST    (CST表示当前地区时间)

<br/>

用法二：# date +%字母

作用：显示指定类型的时间（如年，分等）

- F：日期，xxxx-xx-xx类型的日期
- T：时间，HH:MM:SS类型的时间
- Y：年，四位数
- m：月，带前导0
- d：日，带前导0
- H：小时，带前导0
- M：分，带前导0
- S：秒，带前导0

<br/>

用法三：# date "+%字母（%中间的字符号任意指定，比如空格，-等）%字母....."

作用：显示指定类型的时间

注：双引号之间的内容为一个整体，可以任意输入

例：# date "+%Y-%m-%d %H:%M:%S"

<br/>

用法四：# date -d    “+/-n day/month/year”   "+%字母（%中间的字符号任意指定，比如空格，-等）%字母....."       【n为具体数字】

作用：以指定格式显示前/后 n  天/月/年   的这个时间

<br/>

![image-20211003144915167](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux6.png)

<br/><br/><br/><br/>

#### （8）cal

<br/>

用法：# cal 【-n/m】【n为具体数字】

作用：显示日历

- -1 ：显示当前月的日历
- -3：显示前一个月，当月，后一个月的日历
- -y：显示当前年的日历
- -m:日历以星期一开头，不加-m默认以星期日开头

<br/><br/><br/><br/>

#### （9）clear/Ctrl+L

<br/>

作用：清屏（不会删除前面的内容，只是将页面上移）

<br/><br/><br/><br/>

#### （10）管道 “ | ” *

<br/>

用法一：# 查询命令 | grep  过滤条件

作用：用来过滤查询后，符合条件的内容，其实就是将前面的输出当作后面的输入

例：ls -a \  |  grep a    （查询根目录下文件名包含a字符的文件）

<br/>

用法二：# 打开文件命令  |   less

作用：和less 文件名 作用一弄一样（不用记）

<br/>

用法三：# 查询命令 | wc -l

作用：查询查询的结果有多少行（比实际行数多一）

<br/><br/><br/><br/><br/><br/><br/><br/>

### 4.高级指令

<br/>

#### （1）hostname

<br/>

用法一：# hostname

作用：输出完整的主机名

例：localhost.localdomain

<br/>

用法二：# hostname -f

作用：输出当前主机名中的FQDN（全限定域名）

例：localhost

<br/><br/><br/><br/>

#### （2）id

<br/>

作用：查看一些用户的基本信息（包含用户id，用户组id，附加组id）

<br/>

用法一：# id

作用：如果不指定用户，默认为当前用户

<br/>

用法二：# id 用户名

作用：输出指定用户的id类信息

<br/>

验证这些信息是否正确？

验证用户信息：文件 etc/passwd

验证用户组信息：文件/etc/group

<br/><br/><br/><br/>

#### （3）whoami

<br/>

作用：查看当前用户是谁

<br/><br/><br/><br/>

#### （4）ps -ef

<br/>

用法一：#ps -ef

- -e ：表示列出全部进程
- -f ： 表示列出详细信息

作用：查看当前所有进程

<br/>

![image-20211003175527425](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux7.png)

<br/>

<br/>

UID：执行该进程的用户

PID：进程的id

PPID：父类的id，如果没有父类id，就称为僵尸进程

C：cpu的占用率，其形式是百分数

STIME：进行的启动时间

TTY：终端设备，发起该进程的设备识别符号，如果显示” ？ “，则表示该进程不是由终端设备发起。

TIME：进程的执行时间

CMD：该进程的名称或对应的路径

<br/>

**用法二：ps -ef  |  grep  进程名称**（很重要）

作用：对要查找的进程进行过滤

<br/><br/><br/><br/>

#### （5）top

<br/>

语法：# top

作用：查看服务进程占的资源，退出按 q 。

按 M 按内存使用从多到少排序，按 P 按CPU使用情况从高到低排序

<br/>

![image-20211003184010665](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux8.png)

<br/><br/>

PID：进程id

USER：使用者

PR：进程权重（优先级）

VIRT：虚拟内存

RES：常驻内存

SHR：共享内存

例：加入进程运行需要先申请500M，结果用来320M，那实际各类内存用了多少？

虚拟内存，申请多少就是多少。常驻内存，用了多少就是多少。共享内存，用了的内存减去共享的。

S：进程的状态。S 表示sleep，R 表示 run

%CPU：内存的占用百分比

%MEM：内存的占用百分比

TIME+：执行的时间

COMMAND：进程的名称后者占用的路径

<br/><br/><br/><br/>

#### （6）du -sh

<br/>

语法：# du -sh 文件名/文件夹名

作用：统计文件大小，如果不加文件名，会将当前文件中所有文件的大小和名字都列出来

-  -s：summary，统计总数
-  -h：以可读性较高的形式展示

<br/><br/><br/><br/>

#### （7）find

<br/>

语法：find 目录名 -name/type 文件名

不支持模糊搜索

作用：

- -name：在目录中查找所有包含此文件名的文件

- type：在目录中查找所有为此类型的文件 

  ​            “ f ”，表示文件，“ d ”，文件夹

<br/><br/><br/><br/>

#### （8）service*

<br/>

语法：service 服务类型 start/stop/restart

作用：用于控制一些软件服务的启动/停止/重启

<br/>

例如：Apache服务的启动，

下载Apache：yum install httpd

<br/><br/><br/><br/>

#### （9）kill

<br/>

语法一：# killl PID

作用：关闭指定进程PID的服务

<br/>

语法二：# killall 进程名称

作用：关闭所有此名称的进程

<br/><br/><br/><br/>

#### （10）ifconfig

<br/>

语法：# ifconfig

作用：查看电脑的IP地址，inet后面的

<br/><br/><br/><br/>

#### （11）reboot

<br/>

语法一：# reboot

作用：重启服务器

<br/>

语法二：# reboot -w

作用：只改启动类文件，不做重启，主要用来模拟重启

<br/><br/><br/><br/>

#### （12）shutdown

<br/>

语法：#shutdown -h 时间 【 “关闭通知” 】

​           #shutdown -h now【 “关闭通知” 】

作用：在指定时间关闭服务器

<br/>

关闭关机计划：

- 7.x之前的版本：Ctrl+C
- 7.x之后的版本：# shutdown -c

<br/><br/><br/><br/>

#### （13）uptime

<br/>

语法：# uptime

作用：输出计算机从开机到现在的运行时间

<br/><br/><br/><br/>

#### （14）uname

<br/>

语法一：# uanme

作用：输出当前系统的名称

<br/>

语法：# uname -a

作用：输出当前计算机全部系统信息（包括类型，主机名全称，内核版本，发布时间，开源计划）

<br/><br/><br/><br/>

#### （15）netstat -tnlp

语法：# netstat -tnlp

作用：查看网络连接状态

<br/>

![image-20211003224557552](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux9.png)

<br/>

- -t：表示只列出tcp协议的连接
- -n：表示将字母组合转化为为ip地址，将协议名转化为端口号
- -l：表示过滤处“state（状态）”，为LISTEN的连接
- -p：表示显示发起连接的进程名称

例：如果不加 n

<br/>

![image-20211003225021193](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux.png)

<br/><br/><br/><br/>

#### （16）man指令

用法：# man 命令

作用：manual 手册（包含linux全部命令的手册）

<br/><br/><br/><br/><br/><br/><br/><br/>

## （三）vim编辑器

<br/>

### 1.vim三种模式

<br/>

vim中存在三种模式：命令模式，编辑模式，末行模式

<br/>

模式中的切换：

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/linux10.png" alt="image-20211004205427819" style="zoom:80%;" />

<br/><br/><br/>

- 命令模式：在该模式下，不能直接对文件进行编辑，但可以输入一些快捷键进行一些操作（删除行，复制行，移动光标，粘贴等）【在打开文件之后默认进入命令模式】

- 编辑模式：在该模式下，能够直接对文件进行编辑

- 末行模式：可以在末行输入命令来对文件进行操作（搜索，替换，保存，退出，撤销，高亮等）

  <br/><br/><br/><br/>

### 2.vim打开文件的方式

用法一：# vim 文件名

作用：打开指定的文件

<br/>

用法二：# vim +数字  文件名

作用：打开指定的文件，并让光标移动到指定的行

<br/>

用法三：vim +/关键字  文件的路径

作用：打开指定的文件，并且高亮显示关键词

<br/>

用法四：# vim 文件名1 文件名2 文件名3

作用：同时打开多个文件

<br/><br/><br/><br/>

### 3.命令模式

<br/>

#### （1）光标移动

<br/>

快捷键一：（shift+6） 或者  ^

作用：光标移动到行首

<br/>

快捷键二： （shift+4） 或者 $

作用：光标移动到行尾

<br/>

快捷键三： gg

作用：光标移动到首行

<br/>

快捷键四：G

作用：光标移动到尾行

<br/>

快捷键五：数字 + G

作用：光标快速移动到指定行

<br/>

快捷键六：Ctrl+b  或者  PgUp

作用：向上翻页 或者 PgDn

<br/>

快捷键七：Ctrl+f

作用：向下翻页

<br/>

快捷键八：数字+↑/↓/←/→

作用：光标以当前行/列为标准，向上/下/左/右 移动 n  行/列

<br/>

快捷键九：:+数字

作用：移动到指定行

<br/><br/><br/><br/>

#### （2）复制

<br/>

快捷键一：yy  + (找到指定行后) p

作用：复制当前行，并在指定行下一行粘贴

<br/>

快捷键二：数字+yy  + （找到指定行后）p

作用：复制以当前行为开始的后几行，并在指定行的下一行粘贴

<br/>

快捷键三：Ctrl+v +↑/↓/←/→（找到指定行后）p

作用：可视化复制（对centos7似乎有问题）

<br/><br/><br/><br/>

#### （3）删除/剪切

<br/>

快捷键一：dd

作用：删除/剪切当行，当按 p 就是剪切，在光标的下一行粘贴

<br/>

快捷键二：数字+dd

作用：删除/剪切以当前行开始的后几行，当按 p 就是剪切，在光标的下一行粘贴

<br/>

快捷键三：D

作用：删除/剪切当前行，但下一行不上移

<br/><br/><br/><br/>

#### （4）撤销和恢复

<br/>

撤销：u  或  :u

恢复：Ctrl+r    ，恢复之前的撤销操作

<br/><br/><br/><br/><br/><br/><br/><br/>

### 4.末行模式

<br/>

进入方式：由命令模式进入，按下“ ：”即可进入

退出方式：

- 按下esc

- 连按两下esc

- 删除末行全部输入的字符

<br/><br/><br/><br/>

#### （1）保存

<br/>

输入：“:w”           保存文件

输入：“:w 文件名”      将文件用此文件名另存为当前目录，且原文件不变

<br/><br/><br/><br/>

#### （2）退出

<br/>

输入：“ :q ”           退出文件

<br/><br/><br/><br/>

#### （3）保存并退出

<br/>

输入：“ :wq ”          强制退出

<br/><br/><br/><br/>

#### （4）强制退出(!)

<br/>

输入：“ :q! ”             强制退出并且修改的内容不做保存

<br/><br/><br/><br/>

#### （5）调用外部命令

<br/>

输入：“ :!外部命令 ”          在末行模式中调用外部命令，按任意键返回文件

<br/><br/><br/><br/>

#### （6）搜索

<br/>

输入：“ :关键词 ”              将文件中的关键词设置为高亮

在搜索结果中切换上/下一个结果，输入“ N/n ”

取消搜索结果的高亮，输入：“ :nohl ”

<br/><br/><br/><br/>

#### （7）替换

<br/>

- :s/搜索的关键词/新的内容

  替换光标所在行的第一处符合条件的内容

- :s/搜索的关键词/新的内容/g

  替换光标所在行的所有符合条件的内容

- :%s/搜索的关键词/新的内容

  替换整个文档中每行第一处符合条件的内容

- :%s/搜索的关键词/新的内容/g

  替换整个文档中所有符合条件的内容

<br/>

%：表示整个文件

g：表示全局

<br/><br/><br/><br/>

#### （8）显示行号

<br/>

输入：“ :set nu ”

如果逍遥取消，则输入：“ set nonu”

<br/><br/><br/><br/>

#### （9）切换文件

<br/>

使用vim同时打开多个文件，在末行模式中进行切换文件

查看当前已经打开的文件名称：“ :files ”

<br/>

![image-20211004225523868](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux11.png)

<br/>

在 %a 的位置有两种显示可能：

- %a：（active），表示当前正在打开的文件
- #：表示上一个打开的文件

<br/>

切换文件的方式：

- 输入：“ :open 文件名 ”

  切换当前文件到指定文件

- 可以通过命令切换到上一个文件或下一个文件

  输入：“ :bn ”  ,切换到下一个文件

  输入：“ :bp ”  ,切换到上一个文件

<br/><br/><br/><br/>

### 5.编辑模式

<br/>

进入：输入“ :i   或者  :a ”

<br/><br/><br/><br/><br/><br/><br/><br/>

### 6.扩展

<br/>

#### （1）代码着色

<br/>

- 输入：“ :syntax on ”                 使文本有颜色
- 输入：“ :syntax off ”                 使文本没有颜色

<br/><br/><br/><br/>

#### （2）vim的配置

<br/>

vim是一款编辑器，编辑器也是有配置文件的。

vim配置有三种情况：

- 在文件打开的时候在末行模式下输入的配置（临时的）
- 个人配置文件（~/.vimrc,没有的话可以自己创建）
- 全局配置文件（vim自带，/etc/vimrc）

<br/>

进入到配置文件中，直接写入后，保存退出就可生效

<br/>

![image-20211003184010665](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux12.png)

<br/>

如果某个配置项个人配置文件与全局配置文件发生冲突时，以个人配置文件为准

<br/><br/><br/><br/>

#### （3）异常退出

<br/>

定义：当编辑文件后没有保存，但直接关闭终端后者发生断电，就会发生异常退出。

出现一下情况：

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/linux13.png" alt="image-20211003184010665" style="zoom:80%;" />

<br/>

纠正错误：在发生异常退出后会在该文件下产生一个隐藏文件，删除后即可恢复正常。

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/linux14.png" alt="image-20211003184010665" />

<br/><br/><br/><br/>

#### （4）别名机制

<br/>

作用：相当于创建了一些属于自己的自定义命令。

别名机制依靠一个别名映射文件：~/.bashrc

只需在文件中加入：alias 别名='要起别名的命令'

注意：如果想要创造的命令生效，必须重新登陆当前用户

<br/><br/><br/><br/>

#### （5）退出

<br/>

输入：“ :x ”

作用：当文件未修改时，为退出；当文件修改后，为保存并退出。

与vim之间的区别：

- :x        当未修改时不改变文件的编辑时间
- :wq      当未修改时改变文件的编辑时间

<br/><br/><br/><br/><br/><br/><br/><br/>

## （四）自有服务

<br/>

### 1.运行模式

<br/>

运行模式也可以称之为运行级别。

在linux中存在一个进程：init（initialize，初始化），进程的id是1.

该进程存在一个对应的配置文件：inittab（系统运行级别配置文件，位置：/etc/inittab）

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/linux15.png" alt="image-20211003184010665" style="zoom: 67%;" />

<br/>

运行级别一共有7种：

- 0：表示关机级别（不要将默认的运行级别设置成这个值）
- 1：单用户模式
- 2：多用户模式，不带NTF（Network File Syetem）
- 3：完整的多用户模式
- 4：没有被使用的模式（被保留模式）
- 5：X11：完整的图形化界面模式
- 7：表示重启级别

<br/>

与级别相关的几个命令：

- #init 0       表示关机
- #init 3       表示切换到不带桌面的模式
- #init 5       表示切换到图形界面
- #init 6        重启电脑

<br/>

将系统默认模式修改：

两种常用进行级别:

multi-user.target  表示   runlevel 3

graphical.target   表示  runlevel 5

<br/>

查看当前运行级别：


 systemctl  get-default

设置级别为3

systemctl set-default  multi-user.target

<br/>

注：init类命令只有管理员才能够执行，普通用户无法执行

这些命令其实都是调用的init进程，将数字（运行级别）传递给进程，让进程去读取配置文件执行相应的操作。

<br/><br/><br/><br/><br/><br/><br/><br/>

### 2.用户与用户组管理

<br/>

注意三个文件：

- /etc/passwd                存储用户信息
- /etc/group                   存储用户组的关键信息
- /etc/shadow                存储用户的密码信息

<br/><br/><br/><br/>

#### （1）用户管理

<br/>

##### ① 添加用户

<br>

常用语法：#useradd  选项  用户名

常用选项：

- -g：表示指定用户的用户主组，选项的值可以是用户组的id，也可以是组名
- -G：表示指定用户的用户附加组，选项的值可以是用户组的id，也可以是组名
- -u：uid，用户的id，系统会默认从1000之后按顺序分配uid，如果不想使用系统分配的，也可以通过选项自定义
- -c：comment，添加注释

例：# useradd -g 501 -G 500 -u 666 -c zheshiyigecomment zhangsan

<br/>

![image-20211005235833042](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux17.png)

<br/>

验证是否成功：

a.验证/etc/passwd的最后一行，查看是否有新添加用户的信息；

b.验证是否存在其家目录（在Centos下创建好用户之后随之产生一个同名家目录）

<br/>

查看附加组，在etc/group中：

![image-20211006000731193](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux18.png)

<br/>

如果不添加选项时，执行useradd后会执行：

a.创建同名的家目录

b.创建同名的用户组

<br/>

扩展：认识passwd文件

<br/>

![](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux16.png)

<br/>

用户名：密码：用户id：用户组id：注释：家目录：解析器shell

<br/>

- 用户名：创建新用户名称，后期登录时需要输入
- 密码：此密码位置一般情况下都是  “x”，表示密码的占位
- 用户id：用户的表示符
- 用户组id：该用户所属的主组id
- 注释：解释该用户是做什么用的
- 家目录：用户灯枯进入系统之后的默认位置
- 解释器shell：等待用户进入系统之后，用户输入指令之后，该解释器会收集用户输入的指令，传递给内核处理

<br/><br/><br/>

##### ② 修改用户

<br/>

常用语法：#usermod  选项  用户名

常用选项：

- -g：表示指定用户的用户主组，选项的值可以是用户组的id，也可以是组名
- -G：表示指定用户的用户附加组，选项的值可以是用户组的id，也可以是组名
- -u：uid，用户的id，系统会默认从1000之后按顺序分配uid，如果不想使用系统分配的，也可以通过选项自定义
- -l：修改用户名

修改用户名：

#usermod -l  新用户名  旧用户名 

例：#usermod  -l lisi  zhangsan

<br/><br/><br/>

##### ③ 设置密码

<br/>

Linux不允许没有密码的用户登录到系统，因此前面创建的用户都处于锁定状态，需要设置密码后才能登录

常用语法：#passwd  用户名

注：设置密码时，密码不会显示，输入完直接回车就行。

​       当已进入到设置密码的用户时，可以不用输入用户名。

<br/><br/><br/>

##### ④ 切换用户

<br/>

常用语法：#su【用户名】

作用：当加用户名时就是切换到指定的用户，当不加用户名时就是切换到root用户。

切换用户需要注意的事项：

- 从root用户切换到普通用户不需要密码，但是反之需要root密码
- 切换用户前后的工作目录是不变的
- 普通用户无法访问root用户家目录，但是反之可以

<br/><br/><br/>

##### ⑤ 删除用户

<br/>

常用语法：#userdel  选项  用户名

常用选项：

- -r：删除用户的同时删除其家目录

注：

- root用户可以直接删除未登录用户，但是不能直接删除已经登录的用户
- 若要删除已经登录的用户，可以先将该用户的所有进程kill，再进行删除。（删除父进程可以连带将子进程杀掉）

<br/>

提示：所有跟用户操作有关的命令（除passwd外），只有root用户有权限执行。

<br/><br/><br/><br/><br/><br/><br/><br/>

#### （2）用户组管理

<br/>

每个用户都有一个用户组，系统可以对一个用户组中的所有用户进行集中管理。不同Linux系统对用户组的规定有所不同，如Linux下的用户属于与他同名的用户组，这个用户组再创建用户时创建。

用户组的添加，删除，修改等操作实际上就是对 /etc/group 文件的更新。

<br/>

![image-20211006014245302](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux19.png)

<br/>

文件结构：用户组名：密码：用户组

<br/><br/><br/>



##### ① 用户组添加

<br/>

常用语法：#groupadd  选项  用户组名

常用选项：

- -g：就是组id，与用户的u类似。如果自己不指定，则默认从1000往后增。

<br/><br/><br/>



##### ② 用户组编辑

<br/>

常用语法：#groupmod  选项  用户组名

常用选项：

- -g：就是组id，与用户的u类似。如果自己不指定，则默认从1000往后增。
- -n：name，用户组名称

<br/><br/><br/>

##### ③ 用户组删除

<br/>

常用语法：#groupdel  用户组名

注意：当存在用户以要删除的组为主组时，要先将所有以此组为主组的用户 的主组改变为其他组，才能将此主删除。

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/linux20.png" alt="image-20211006014944501" style="zoom:80%;" />

<br/><br/><br/><br/><br/><br/><br/><br/>



### 3.网络设置

<br/>

##### ① 基本配置

首选要知道，网卡配置文件的位置：**/etc/sysconfig/network-scripts**，

其中，在目录中网卡的配置文件名称为：**ifcfg-网卡名**

<br/>

![](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux21.png)

<br/>

ifcfg-ens33为文件，可以直接访问

<br/>

![image-20211006181222897](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux22.png)

<br/>

- ONBOOT：是否开机自启动
- BOOTPROTO：ip地址分配方式，DHCP表示动态主机分配协议

<br/>

**命令：#service network restart**

作用：重新启动网卡（可以远程操作）

注：在有的Linux分支中可能没有service命令来快速执行操作服务，但是有一个共性的目录：**/etc/init.d**，这个目录中存放着很多对服务的快捷方式，此处重启命令还可以使用：**#/etc/init.d/network restart**

<br/><br/>

##### ② 文件创建快捷方式

扩展一：如果修改网卡的配置文件，但是配置文件的层数很深，此时可以在浅的目录中创建一个快捷方式（软连接），方便以后去查找,但是创建完后，不能直接用rm -rf删除，会将源文件的内容也删掉（我感觉不建议使用）

用法：#ln -s  要创建快捷方式的文件或文件夹  创建快捷方式的地址

<br/>

![image-20211006183459702](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux23.png)

<br/>

创建成功后：

<br/>

![image-20211006183609876](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux24.png)

<br/>

其中，文件类型位置的“ l ”表示其类型为link（连接类型），后面的“->”指向的是源文件的路径。

<br/><br/>

##### ③ 重启单个网卡

扩展二：重启单个网卡

**警告**：不建议使用关闭网卡，当为远程连接时，关闭网卡意味着远程控制端无法连接到服务端，也就不能远程启动。

停止某个网卡：#ifdown  网卡名

启动某个网卡：#ifup  网卡名

例如：停止ens33，用 #ifdown ens33

<br/><br/><br/><br/><br/><br/><br/><br/>

### 4.ssh服务

<br/>

ssh（secure shell，安全外壳协议），该协议有两个常用的作用：远程连接协议，远程文件传输协议。

协议使用端口号：默认是22

可以被修改的，如果需要修改，则需要修改ssh服务的配置文件：/etc/ssh/ssh_config

<br/>

![image-20211006204423553](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux25.png)

<br/>

端口号可以修改，但是得注意两个选项：

- 注意范围，端口范围是从0-65535
- 不能使用别的服务已经占用的端口

服务启动/停止/重启

#service sshd start/stop/restore

#/etc/init.d/sshd

<br/>

xshell，xftp下载

<br/><br/><br/><br/><br/><br/><br/><br/>

### 5.设置用户名

<br/>

回顾：

#hostname

#hostname -f     FQDN（全限定域名）

<br/>

（1）临时设置主机名

语法：#hostname  设置的主机名

注：这个只是临时生效，重启后就会复原

<br/>

（2）永久设置域名

找到主机名的配置文件：/etc/sysconfig/network    （CentOS这个文件是空的）

直接用命令：#hostnamectl  set-hostname  要设置的主机名

<br/>

（3）

修改linux服务器的host文件，将linux指向本地（设置FQDN）

Hosts文件地位置：/etc/hosts

<br/>

![image-20211006224735682](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux26.png)

<br/>

如果不设置FQDN会怎么样？

- 很多开源服务器软件则无法启动，或出现报错
- 方便记忆，看到主机名对其作用有一个初步判断
- 如果不设置则会影响本地的域名解析（本地访问）

<br/><br/><br/><br/><br/><br/><br/>

### 6.chkconfig和systemctl

<br/>

作用：相当于windows下“安全卫士”，“电脑管家”之类的安全辅助工具提供“开机启动项”的一个管理服务。

在linux下不是所有的软件安装完成之后都有开机启动服务，有的需要自己去添加。此外还可以查看和删除。

<br/>

（1）开机启动服务查询

#chkconfig --list

作用：查看开启是否自启动的服务查询

<br/>

![image-20211009134208242](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux27.png)

<br/>

其中。0~6代表启动级别。

以network为例，其三级别为开（on），则在三级别下默认开机自启。

<br/>

（2）删除服务

用法：#chkconfig --del 服务名

<br/>

（3）添加开机启动服务

用法：#chkconfig --add  服务名

注：必须要保证服务正常启动，才可以添加

<br/>

（4）设置服务下某个级别下开机启动/不启动

用法：#chkconfig --level  连在一起的启动级别  服务名 on/off

例如：关闭3，5级别下的

#chkconfig --level  35  httpd  off

<br/><br/>

具体详解：

(Linux systemctl是一个系统管理守护进程、工具和库的集合，用于取代System V、service和chkconfig命令)

CentOS 7.x开始，CentOS开始使用systemd服务来代替daemon，原来管理系统启动和管理系统服务的相关命令全部由systemctl命令来代替。

##### 1、原来的 service 命令与 systemctl 命令对比

<br/>

| daemon命令             | systemctl命令                 | 说明     |
| ---------------------- | ----------------------------- | -------- |
| service [服务] start   | systemctl start [unit type]   | 启动服务 |
| service [服务] stop    | systemctl stop [unit type]    | 停止服务 |
| service [服务] restart | systemctl restart [unit type] | 重启服务 |

<br/>

此外还是二个systemctl参数没有与service命令参数对应

- status：参数来查看服务运行情况
- reload：重新加载服务，加载更新后的配置文件（并不是所有服务都支持这个参数，比如network.service）

**应用举例：**

```
#启动网络服务
systemctl start network.service

#停止网络服务
systemctl stop network.service

#重启网络服务
systemctl restart network.service

#查看网络服务状态
systemctl status network.serivce
1234567891011
```

<br/>

##### 2、原来的chkconfig 命令与 systemctl 命令对比

<br/>

###### 2.1、设置开机启动/不启动

| daemon命令           | systemctl命令                 | 说明                 |
| -------------------- | ----------------------------- | -------------------- |
| chkconfig [服务] on  | systemctl enable [unit type]  | 设置服务开机启动     |
| chkconfig [服务] off | systemctl disable [unit type] | 设备服务禁止开机启动 |

**应用举例：**

```
#停止cup电源管理服务
systemctl stop cups.service

#禁止cups服务开机启动
systemctl disable cups.service

#查看cups服务状态
systemctl status cups.service

#重新设置cups服务开机启动
systemctl enable cups.service
1234567891011
```

<br/>

###### 2.2、查看系统上上所有的服务

命令格式：

```
systemctl [command] [–type=TYPE] [–all]
```

参数详解：

`command` - list-units：依据unit列出所有启动的unit。加上 –all 才会列出没启动的unit; - list-unit-files:依据/usr/lib/systemd/system/ 内的启动文件，列出启动文件列表

`–type=TYPE` - 为unit type, 主要有service, socket, target

**应用举例：**

| systemctl命令                                    | 说明                       |
| ------------------------------------------------ | -------------------------- |
| systemctl                                        | 列出所有的系统服务         |
| systemctl list-units                             | 列出所有启动unit           |
| systemctl list-unit-files                        | 列出所有启动文件           |
| systemctl list-units –type=service –all          | 列出所有service类型的unit  |
| systemctl list-units –type=service –all grep cpu | 列出 cpu电源管理机制的服务 |
| systemctl list-units –type=target –all           | 列出所有target             |

<br/>

##### 3、systemctl特殊的用法

| systemctl命令                   | 说明                       |
| ------------------------------- | -------------------------- |
| systemctl is-active [unit type] | 查看服务是否运行           |
| systemctl is-enable [unit type] | 查看服务是否设置为开机启动 |
| systemctl mask [unit type]      | 注销指定服务               |
| systemctl unmask [unit type]    | 取消注销指定服务           |

**应用举例：**

```
#查看网络服务是否启动
systemctl is-active network.service

#检查网络服务是否设置为开机启动
systemctl is-enable network.service

#停止cups服务
systemctl stop cups.service

#注销cups服务
systemctl mask cups.service

#查看cups服务状态
systemctl status cups.service

#取消注销cups服务
systemctl unmask cups.service
1234567891011121314151617
```

<br/>

##### 4、init 命令与systemctl命令对比

| init命令 | systemctl命令      | 说明     |
| -------- | ------------------ | -------- |
| init 0   | systemctl poweroff | 系统关机 |
| init 6   | systemctl reboot   | 重新启动 |

与开关机相关的其他命令：

| systemctl命令       | 说明                 |
| ------------------- | -------------------- |
| systemctl suspend   | 进入睡眠模式         |
| systemctl hibernate | 进入休眠模式         |
| systemctl rescue    | 强制进入救援模式     |
| systemctl emergency | 强制进入紧急救援模式 |

<br/>

##### 5、设置系统运行级别

###### 5.1、运行级别对应表

<br/>

| init级别 | systemctl target  |
| -------- | ----------------- |
| 0        | shutdown.target   |
| 1        | emergency.target  |
| 2        | rescure.target    |
| 3        | multi-user.target |
| 4        | 无                |
| 5        | graphical.target  |
| 6        | 无                |

此外还是一个getty.target用来设置tty的数量。

<br/>

###### 5.2、设置运行级别

<br/>

命令格式：

```
systemctl [command] [unit.target]
1
```

参数详解：

```
command:
1
```

- get-default :取得当前的target
- set-default :设置指定的target为默认的运行级别
- isolate :切换到指定的运行级别
- unit.target :为5.1表中列出的运行级别

| systemctl命令                           | 说明                                         |
| --------------------------------------- | -------------------------------------------- |
| systemctl get-default                   | 获得当前的运行级别                           |
| systemctl set-default multi-user.target | 设置默认的运行级别为mulit-user               |
| systemctl isolate multi-user.target     | 在不重启的情况下，切换到运行级别mulit-user下 |
| systemctl isolate graphical.target      | 在不重启的情况下，切换到图形界面下           |

<br/>

##### 6、使用systemctl分析各服务之前的依赖关系

<br/>

命令格式：

```
systemctl list-dependencies [unit] [–reverse]
1
```

`–reverse`是用来检查寻哪个unit使用了这个unit

**应用举例：**

```
#获得当前运行级别的target
[root@www ~]# systemctl get-default
multi-user.target

#查看当前运行级别target(mult-user)启动了哪些服务
[root@www ~]# systemctl list-dependencies
default.target
├─abrt-ccpp.service
├─abrt-oops.service
├─vsftpd.service
├─basic.target
│ ├─alsa-restore.service
│ ├─alsa-state.service
.....(中间省略).....
│ ├─sockets.target
│ │ ├─avahi-daemon.socket
│ │ ├─dbus.socket
.....(中间省略).....
│ ├─sysinit.target
│ │ ├─dev-hugepages.mount
│ │ ├─dev-mqueue.mount
.....(中间省略).....
│ └─timers.target
│   └─systemd-tmpfiles-clean.timer
├─getty.target
│ └─getty@tty1.service
└─remote-fs.target

#查看哪些target引用了当前运行级别的target
[root@www ~]# systemctl list-dependencies --reverse
default.target
└─graphical.target
1234567891011121314151617181920212223242526272829303132
```

<br/>

##### 7、关闭网络服务

<br/>

在使用systemctl关闭网络服务时有一些特殊 需要同时关闭unit.servce和unit.socket

使用systemctl查看开启的sshd服务

```
[root@www system]#  systemctl list-units --all | grep sshd
sshd-keygen.service loaded inactive dead        OpenSSH Server Key Generation
sshd.service        loaded active   running     OpenSSH server daemon
sshd.socket         loaded inactive dead        OpenSSH Server Socket
1234
```

可以看到系统同时开启了 `sshd.service` 和 `sshd.socket` , 如果只闭关了 `sshd.service` 那么 `sshd.socket`还在监听网络，在网络上有要求连接 sshd 时就会启动 `sshd.service` 。因此如果想完全关闭sshd服务的话，需要同时停用 `sshd.service` 和 `sshd.socket` 。

```
systemctl stop sshd.service
systemctl stop sshd.socket
systemctl disable sshd.service sshd.socket
123
```

由于centos 7.x默认没有安装net-tools，因此无法使用netstat 来查看主机开发的商品。需要通过yum安装来获得该工具包：

```
yum -y install net-tools
1
```

查看是否关闭22端口

```
netstat -lnp |grep sshd
1
```

<br/>

##### 8、关闭防火墙firewall

<br/>

Centos 7.x 中取消了iptables, 用firewall取而代之。要关闭防火墙并禁止开机启动服务使用下面的命令:

```
systemctl stop firewalld.service
systemctl disable firewalld.service1
```

<br/><br/><br/><br/><br/><br/><br/>

### 7.ntp服务

<br/>

##### **这是centos6的方法：**

<br/>

作用：ntp主要是用来对计算机的时间同步管理。

时间对服务器来说是很重要的，一般很多网站都需要读取服务器时间来记录数据。

（1）一次性同步时间

用法：#ntpdate  时间服务器域名或ip地址

<br/>

（2）设置时间同步服务

服务名：ntpd（）

启动ntpd服务

#service ntpd start

<br/><br/>

##### 这是centos7的方法：

<br/>

###### 设置时区（CentOS 7）

<br/>

先执行命令`timedatectl status|grep 'Time zone'`查看当前时区，如果不是中国时区（Asia/Shanghai），则需要先设置为中国时区，否则时区不同会存在时差。

```bash
#已经是Asia/Shanghai，则无需设置
[root@xiaoz shadowsocks]# timedatectl status|grep 'Time zone'
       Time zone: Asia/Shanghai (CST, +0800)
```

执行下面的命令设置时区

```bash
#设置硬件时钟调整为与本地时钟一致
timedatectl set-local-rtc 1
#设置时区为上海
timedatectl set-timezone Asia/Shanghai
```

<br/>

###### 使用ntpdate同步时间

<br/>

目前比较常用的做法就是使用ntpdate命令来同步时间，使用方法如下：

```bash
#安装ntpdate
yum -y install ntpdate
#同步时间
ntpdate -u  pool.ntp.org
#同步完成后,date命令查看时间是否正确
date
```

另外再分享下几个常用的ntp server，如果需要更多可以前往：[http://www.ntp.org.cn](http://www.ntp.org.cn/)获取

```bash
#中国
cn.ntp.org.cn
#中国香港
hk.ntp.org.cn
#美国
us.ntp.org.cn
```

同步时间后可能部分服务器过一段时间又会出现偏差，因此最好设置`crontab`来定时同步时间，方法如下：

```bash
#安装crontab
yum -y install crontab
#创建crontab任务
crontab -e
#添加定时任务
*/20 * * * * /usr/sbin/ntpdate pool.ntp.org > /dev/null 2>&1
#重启crontab
service crond reload
```

上面的计划任务会在每20分钟进行一次时间同步，注意`/usr/sbin/ntpdate`为`ntpdate`命令所在的绝对路径，不同的服务器可能路径不一样，可以使用`which`命令来找到绝对路径，方法如下：

```bash
[root@xiaoz ~]# which ntpdate
/usr/sbin/ntpdate
```

<br/>

###### 使用rdate同步时间

<br/>

ntpdate服务需要使用`udp/123`端口，但是某些服务商禁止了所有UDP协议，所以你会发现无论如何ntpdate总是同步出错。

```bash
#下方是ntpdate同步时间报错的一个列子
[root@sharktech ~]# ntpdate -u  pool.ntp.org
 1 Jun 16:13:46 ntpdate[8389]: no server suitable for synchronization found
```

这个时候我们可以改用rdate命令来同步时间，方法如下：

```bash
#安装rdate
yum -y install rdate
#同步时间
rdate -s time-b.nist.gov
#查看时间是否正确
date
```

和上面一样，我们最好是加入定时任务来定期同步时间，方法如下：

```bash
#安装crontab
yum -y install crontab
#创建crontab任务
crontab -e
#添加定时任务
*/20 * * * * /usr/bin/rdate -s time-b.nist.gov > /dev/null 2>&1
#重启crontab
service crond reload
```

还有一些其它的rdate时间服务器如下：

```bash
s1d.time.edu.cn #东南大学
s1e.time.edu.cn #清华大学
s2a.time.edu.cn #清华大学
s2b.time.edu.cn #清华大学
s2c.time.edu.cn #北京邮电大学
ntp.sjtu.edu.cn 202.120.2.101 #(上海交通大学网络中心NTP服务器地址）
s1a.time.edu.cn #北京邮电大学
s1b.time.edu.cn #清华大学
s1c.time.edu.cn #北京大学
clock.cuhk.edu.hk #香港中文大学授时中心
```

<br/>

###### 总结

<br/>

无论是使用`ntpdate`还是`rdate`来同步时间，方法都比较简单，大致流程就是“设置时区” -> “同步时间” -> “设置定时任务”。在实际的测试中，xiaoz发现部分服务商屏蔽UDP端口的情况下，`ntpdate`命令无法同步，但使用`rdate`命令却可以，有类似情况的童鞋不妨试一下。

<br/><br/><br/><br/><br/><br/><br/><br/>

### 8.防火墙

<br/>

- Firewalld命令：

```
#进程与状态相关
systemctl start firewalld.service            #启动防火墙  
systemctl stop firewalld.service             #停止防火墙  
firewall-cmd --state                         #查看防火墙状态  
firewall-cmd --reload                        #更新防火墙规则  
firewall-cmd --state                         #查看防火墙状态  
firewall-cmd --reload                        #重载防火墙规则  
firewall-cmd --list-ports                    #查看所有打开的端口  
firewall-cmd --list-services                 #查看所有允许的服务  
firewall-cmd --get-services                  #获取所有支持的服务  


#区域相关
firewall-cmd --list-all-zones                    #查看所有区域信息  
firewall-cmd --get-active-zones                  #查看活动区域信息  
firewall-cmd --set-default-zone=public           #设置public为默认区域  
firewall-cmd --get-default-zone                  #查看默认区域信息  
firewall-cmd --zone=public --add-interface=eth0  #将接口eth0加入区域public


#接口相关
firewall-cmd --zone=public --remove-interface=eth0       #从区域public中删除接口eth0  
firewall-cmd --zone=default --change-interface=eth0      #修改接口eth0所属区域为default  
firewall-cmd --get-zone-of-interface=eth0                #查看接口eth0所属区域  


#端口控制
firewall-cmd --add-port=80/tcp --permanent               #永久添加80端口例外(全局)
firewall-cmd --remove-port=80/tcp --permanent            #永久删除80端口例外(全局)
firewall-cmd --add-port=65001-65010/tcp --permanent      #永久增加65001-65010例外(全局)  

firewall-cmd  --zone=public --add-port=80/tcp --permanent            #永久添加80端口例外(区域public)
firewall-cmd  --zone=public --remove-port=80/tcp --permanent         #永久删除80端口例外(区域public)
firewall-cmd  --zone=public --add-port=65001-65010/tcp --permanent   #永久增加65001-65010例外(区域public) 
```

**注：如果某个接口不属于任何Zone，那么这个接口的所有数据包使用默认的Zone的规则。**

- 命令含义：
  --zone #作用域
  --add-port=80/tcp #添加端口，格式为：端口/通讯协议
  --permanent #永久生效，没有此参数重启后失效
- Systemctl命令：

```
systemctl start firewalld.service               #启动服务
systemctl stop firewalld.service                #关闭服务
systemctl reloadt firewalld.service             #重载配置
systemctl restart firewalld.service             #重启服务
systemctl status firewalld.service              #显示服务的状态
systemctl enable firewalld.service              #在开机时启用服务
systemctl disable firewalld.service             #在开机时禁用服务
systemctl is-enabled firewalld.service          #查看服务是否开机启动
systemctl list-unit-files|grep enabled          #查看已启动的服务列表
systemctl --failed                              #查看启动失败的服务列表
```

- 关闭CentOS7自带Firewall启用iptables：

```
yum install iptables-services           #安装iptables  
systemctl stop firewalld.service        #停止firewalld  
systemctl mask firewalld.service        #禁止自动和手动启动firewalld  
systemctl start iptables.service        #启动iptables
systemctl start ip6tables.service       #启动ip6tables  
systemctl enable iptables.service       #设置iptables自启动  
systemctl enable ip6tables.service      #设置ip6tables自启动  
注：静态防火墙规则配置文件是 /etc/sysconfig/iptables 以及 /etc/sysconfig/ip6tables  
```

<br/><br/><br/><br/><br/><br/><br/><br/>

### 9.rpm软件管理

<br/>

#### （1）RPM包的命名规则

<br/>

**httpd-2.4.6-67.el7.centos.x86_64.rpm**

<br/>

| httpd      | 软件包名        |
| ---------- | --------------- |
| 2.4.6      | 软件版本        |
| 67         | 软件发行的次数  |
| el7.centos | 适合的linux平台 |
| x86_64     | 适合的硬件平台  |
| rpm        | rpm包扩展名     |



<br/><br/><br/><br/>

#### （2）RPM包的依赖性

<br/>

树形依赖性：a -> b -> c,即a依赖b，b依赖c
环形依赖：a -> b -> c -> a
模块依赖：模块依赖查询网站：www.rpmfind.com

<br/><br/><br/><br/>

#### （3）安装、升级、卸载和查询

<br/>

##### ① 包全名和包名


| 包全名                                     | 包名                               |
| ------------------------------------------ | ---------------------------------- |
| 例如：httpd-2.4.6-67.el7.centos.x86_64.rpm | 例如：httpd                        |
| 操作的包时没有安装的软件包时，使用包全名   | 操作的已经安装的软件包时，使用包名 |
| 安装、升级时用                             | 查询、卸载时用                     |

<br/><br/>

##### ② RPM安装

安装要先到官网下载安装包或者直接从驱动光盘中获取，在进行安装

#rpm包的安装格式

**rpm -ivh 包全名  【--nodeps】**

选项:

- ​    -i(install)    安装
- ​    -v(verbose)    显示详细信息
- ​    -h(hash)       显示进度
- ​    --nodeps       不检测依赖性

<br/>

举例：

```
[root@localhost Packages]# rpm -ivh httpd-2.4.6-67.el7.centos.x86_64.rpm 
```

可能会有很多依赖性问题出现，根据一个个依赖性继续rpm安装就可以了（这个过称可能要很长时间）

<br/><br/>

##### ③ RPM包升级

#RPM包的升级格式

rpm -Uvh 包全名
选项:
    -U (upgrade)    升级

过程和安装完全一样。

<br/><br/>

##### ④ RPM包的卸载

#RPM包的卸载格式

rpm -e 包名  【--nodeps】
选项:
    -e (erase)    卸载
    --nodeps      不检测依赖性

<br/>
举例：

```
[root@localhost Packages]# rpm -e httpd
错误：依赖检测失败：
        httpd = 2.4.6-67.el7.centos 被 (已安裝) httpd-devel-2.4.6-67.el7.centos.x86_64 需要
[root@localhost Packages]# rpm -e httpd-devel 
[root@localhost Packages]# rpm -e httpd
```



出现错误提示依赖关系，要先卸载依赖关系或者忽略依赖关系。才能卸载

注：卸载要按照安装依赖性的反向卸载



<br/><br/>

##### ⑤ RPM包的查询

用法一：# rpm -q 包名

作用：查询包是否安装

选项:
    -q    查询(query)





<br/>

用法二：#rpm -qa

作用：查询所有已经安装的RPM包

选项:
    -a    所有 

<br/>

用法三：#rpm -qi 包名

作用：查询软件包的详细信息

选项:
    -i    查询软件信息（information）

<br/>

用法四：#rpm -ql 包名

作用：查询包中文件安装位置
选项:
    -l    列表（list）

<br/>

用法五：# rpm -qf 系统文件名

作用：查询系统文件属于哪个RPM包

选项:
    -f    （file）

<br/>

用法六：# rpm -qR 包名

作用：查询软件包的依赖性

选项:
    -R    （requires）

<br/><br/><br/><br/><br/><br/><br/><br/>

### 10.块状设备挂载与解挂

<br/>

#### （1）查看挂载信息

<br/>

用法：#lsblk      

作用：查看块状设备信息（list block devices）     

<br/>

![image-20211009175033280](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux28.png)

- NAME：名称
- Size：设备大小
- Type：类型
- MountPoint：挂载点（类似于Windows下的盘符）

<br/><br/><br/><br/>

#### （2）解挂

<br/>

命令：umount

语法：#umount  当前设备的挂载点（路径）

注：当有空格时这个地方就会告诉你有错误，这时要使用转义字符 \ 放在空格的前面，这时才会读取空格；或者将文件路径用单引号或双引号括起来。

解挂成功后，相当于U盘在windows上已经被弹出但是没有拔下。

<br/>

![image-20211009181627939](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux29.png)

<br/><br/><br/><br/>

#### （3）挂载

<br/>

命令：mount

语法：#mount  设备原始地址  要挂载的位置路径

设备原始地址：地址统一在/dev下，然后根据大小确定具体的name值，拼凑在一起组成原始地址，例如当前：“/dev/sr0”

要挂载的位置路径：挂载目录一般都在mnt下，也可以在mnt下创建目录，此处以“dev/DVD”为例

<br/>

成功展示：

<br/>

![image-20211009182732069](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux30.png)

![image-20211009182838440](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux31.png)

<br/><br/><br/><br/><br/><br/><br/><br/>

### 11.cron计划任务

<br/>

作用：操作系统不可能24小时都有人操作，所有当完成一些定时任务时，可以直接设置定时，让操作系统在指定时间自己运行。

语法：#crontab  选项

选项：

- -l：list，列出指定用户的计划任务表
- -e：edit，编辑指定用户的计划任务列表
- -u：user，指定用户，如果不指定就是当前用户
- -r：remove，删除指定用户的计划任务列表

例：#crontab  -l  -u meilun

<br/>

编辑计划任务

计划任务的规则语法格式，以行为单位，一行则为一个计划：

分  时  日  月  周  需要执行的命令

0 0 * * * init 6

<br/>

注意：执行命令的特殊字符需要用  **“ \ ”**   进行转义,比如：%，""

<br/>

取值范围：

分：0~59

时：0~23

日：1~31

月：1~12

周：0~6，0表示周日

<br/>

四个符号：

*：表示所有时间

-：表示连续区间，比如1~7，就写为1-7

/：表示每多少个，比如，想要每10分钟一次，就可以写为*/10

,：表示多个取值，比如想在1点，7点执行，就可以写成1,7

<br/>

当遇到错误时，可以去**/var/spool/mail**查看对应用户中的问题

<br/><br/>

crontab权限问题：本身是任何用户都可以进行创建自己的计划任务。但是root用户可以通过配置来设置使得某些用户不能创建计划任务。

此配置文件为：/etc/cron.deny，只需在里面写用户名即可

<br/>

root用户还可以自己创建一个文件（白名单）是某些用户可以创建计划任务。这个文件为：/etc/cron.allow。（本身不存在，要自己创建）

注意：白名单的等级要高于黑名单，若一个用户名同时在两个名单中，以白名单为主。

<br/><br/><br/><br/><br/><br/><br/><br/>

## （五）权限管理

<br/>

### 1.权限概述

<br/>

总述：Linux系统一般将文件可存/可访问的身份分为3个类别：owner，group，others，且3种身份各自有read，write，execute等权限。

<br/>

#### （1）权限介绍

<br/>

什么是权限？

在多用户（可以不同时）计算机系统的管理种，权限是指某个特定的用户具有特定的系统资源使用权力，像是文件夹，特定系统指令的使用或者存储量的限制。

<br/>

要设置权限，就要知道文件的一些基本属性和权限的分配规划。在Linux中，ls命令常用于查看文件的属性，用于显示文件的文件名和一些相关属性。

<br/>

Linux中存在用户，用户组和其他人概念，各自都有不同的权力，对于一个文件来说，其权限分配情况如下：

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/linux32.png" alt="image-20211009232850063" style="zoom:80%;" />

<br/><br/><br/><br/>

#### （2）身份介绍

<br/>

##### ① Owner身份

(文件所有者，默认为文档的创建者)

由于Linux是多用户、多任务的操作系统，因此可能常常有多人同时在某台主机上工作，但每个人均可在主机上设置文件的权限，让其成为个人的“私密文件”，即个人所有者。因为设置了适当的文件权限，除本人(文件所有者)之外的用户无法查看文件内容。

例如某个MM给你发了一封Email情书,你将情书转为文件之后存档在自己的主文件夹中。为了不让别人看到情书的内容，你就能利用所有者的身份去设置文件的适当权限，这样，即使你的情敌想偷看你的情书内容也是做不到的。

<br/><br/>

##### ② Group身份

(与文件所有者同组的用户)

与文件所有者同组最有用的功能就体现在多个团队在同一台主机上开发资源的时候。例如主机上有A、B两个团体，A中有a1,a2,a3三个成员，B中有b1,b2两个成员，这两个团体要共同完成一份报告F。由于设置了适当的权限，A、B团体中的成员都能互相修改对方的数据，但是团体C的成员则不能修改F的内容，甚至连查看的权限都没有。同时，团体的成员也能设置自己的私密文件，让团队的其它成员也读取不了文件数据。在Linux中，每个账户支持多个用户组。如用户a1、b1 即可属于A用户组，也能属于B用户组。

<br/><br/>

##### ③ Others身份

(其他人)

这个是个相对概念。打个比方，大明、二明、小明一家三兄弟住在一间房9房产证上的登记者是大明，那么，大明一家就是一个用户组，这个组有大明、二明、小明三个成员;另外有个人交张三，和他们三没有关系，那么这个张三就是其他人了。

同时，大明、二明、小明有各自的房间，三者虽然能自由进出各自的房间，但是小明不能让大明看到自己的情书、日记等，这就是文件所有者(用户)的意义。

<br/><br/>

##### ⑤ Root用户

(超级用户)

在Linux中，还有一个神一-样存在的用户，这就是root用户，因为在所有用户中它拥有最大的权限，所以管理着普通用户。

<br/><br/><br/><br/><br/><br/><br/><br/>

### 2.权限设置

<br/>

语法：#chmod  选项  权限模式  文档

常用选项：

- -R：递归设置权限（当文档类型为文件夹时）

权限模式：就是该文档需要设置的权限信息

注：

a. 文档可以是文件也可以是文件夹，可以是相对路径也可以是绝对路径。

b. 如果想要给文档设置权限，操作者要么是root用户，要么是文档的所有者。

c. 修改时要修改u|g|o，可以用逗号分隔。

<br/>

#### （1）字母形式

<br/>

| 选项     | 字母 |   介绍   |
| -------- | ---- | :------: |
| （谁）   | u    |  所用者  |
| （谁）   | g    |  所属组  |
| （谁）   | o    |  其他人  |
| （谁）   | a    |  所用人  |
| （作用） | +    | 增加权限 |
| （作用） | -    | 减少权限 |
| （作用） | =    | 确定权限 |
| （权限） | r    |   可读   |
| （权限） | w    |   可写   |
| （权限） | x    |  可执行  |

<br/>

给谁设置：

- u：表示所有者身份owner（user）

- g：表示所有者同组设置（group）

- o：表示other，给其他用户设置权限

- a：表示all，给所有人（ugo）设置权限

  ​      如果在设置权限的时候不指定给谁设置，则默认给所有用户设置

权限字符：

- r：读
- w：写
- x：执行

权限分配方式：

- +：表示给具体的用户设置权限
- -：表示删除用户的权限
- =：表示将权限设置为具体的值

<br/>

例子：

#chmod  u+x,g-r,o=---  a.txt，所用者加可执行权限，用户组去除读权限，其他人没有任何权限

#chmod  +x  a.txt ，所有人都加执行权限

<br/><br/><br/><br/>

#### （2）数字形式

<br/>

| 数值 | 权限                             | 目录列表 |
| :--: | -------------------------------- | -------- |
|  0   | 不能读，不能写，不能执行         | ---      |
|  1   | 不能读，不能写，能执行           | --x      |
|  2   | 不能读，能写，不能执行（不建议） | -w-      |
|  3   | 不能读，能写，能执行（不建议）   | -wx      |
|  4   | 能读，不能写，不能执行           | r--      |
|  5   | 能读，不能写，能执行             | r-x      |
|  6   | 能读，能写，不能执行             | rw-      |
|  7   | 能读，不能写，能执行             | rwx      |

<br/>

例：chmod -R  741 aaa.txt

<br/><br/><br/><br/>

#### （3）注意事项

<br/>

在一个文件夹中，即使用户拥有所有权限，当遇到删除，移动，重命名操作时，还是要先看此用户是否有文件夹的写权限。

<br/><br/><br/><br/><br/><br/><br/><br/>

### 3.属主与属组设置

<br/>

![image-20211011181412359](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux33.png)

<br/>

#### （1）chown

<br/>

用法一：#chown 【-R】 username  文件名/文件夹名

作用：修改文件的所有者

选项：

- -R：当为文件夹时需要加上（centos7可以不加）

例：#chown root bb

<br/>

用法二：#chown 【-R】 username:username  文件名/文件夹名

作用：修改文件的所有者和所属组

例：#chown meilun:meilun bb

<br/><br/><br/><br/>

#### （2）chgrp

<br/>

用法：#chgrp 【-R】 username  文件名/文件夹名

作用：修改文件的所属组

选项：

- -R：当为文件夹时需要加上（centos7可以不加）

例：#chgrp root bb

<br/><br/><br/><br/><br/><br/><br/><br/>

### 4.sudo

<br/>

sudo使用的意义：当需要给用户一定的root权限使其可以使用一些root的命令时，可以通过更改配置文件来赋予权限。

<br/>

（1）sudo的使用

首先需要root赋予某个用户sudo权限，进入配置文件（这里进入不能直接到文件里找，而是需要一个命令）：

配置文件：/etc/sudoers

进入方式：#visudo

进入后找到此位置：

<br/>

![image-20211011193955997](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux35.png)

<br/>

- root：表示可执行此命令的用户
- ALL：表示可执行此命令的主机名（地址）
- （ALL）：其中的ALL表示执行身份，ALL表示root，如果以root身份执行的话，这个地方连带括号都是可以不加的
- ALL（末尾的ALL）：表示可以执行的命令，建议不要直接写命令，用配置文件的命令来启动,当有多个命令时，可以
- 找到配置文件的命令用：**which 命令**，来查找命令的位置

添加命令：meilun  ALL=  /usr/sbin/useradd,/usr/bin/passwd [a-zA-Z]*,!/usr/bin/passwd root

<br/>

赋予用户，添加用户和设置用户名的权限，但不包括root用户

/usr/sbin/useradd,/usr/bin/passwd [a-zA-Z]*,!/usr/bin/passwd root

解释：

- 后面的两句位置不能更换,

  按我的理解就是/etc/sudoers中的命令是顺序执行，原本其他用户就是没有设置密码的权限的，将!/usr/bin/passwd root直接写在前面会让系统直接忽略这条命令，使得只有后面这句/usr/bin/passwd [a-zA-Z]*被执行，使得其他用户可以更改root的密码；而将!/usr/bin/passwd root写在后面就会在允许修改密码之后只将这一条禁止，使得其他用户无法修改root的密码。

- [a-zA-Z]的目的是让用户不能不写任何用户，因为在设置时，是让此用户以root的身份执行这条命令，如果不写任何用户，就会默认为root，修改的就是root的密码。

<br/><br/><br/><br/><br/><br/><br/><br/>

## （六）shell

<br/>

### 1.关于shell

<br/>

#### （1）什么是shell

<br/>

##### ① 什么是shell

shell（外壳）是一种用C语言编写的程序，他是用户使用Linux的桥梁，shell即是一种命令语言，又是一种程序设计语言。

shell：是一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统的内核服务。

<br/><br/>

##### ② 什么是脚本

<br/>

脚本简单的说就是一条条的文字命令，这些文字命令是可以看到的。

常见的脚本：javascript，asp，jsp。python等。

<br/><br/>

##### ③ 为什么要学习shell

<br/>

程序开发的效率非常高，依赖于功能强大的命令可以循序完成开发任务。

<br/><br/>

##### ④ 常见的shell种类

<br/>

在linux中有许多不同的shell，不同的shell具有不同的功能，shell还规定了脚本中函数的语法，在linux中默认的shell是/bin/bash,流行的shell有ash，bash，ksh，csh，zsh等，不同的shell都有自己的特点和用途。

<br/>

- csh：C shell  使用的是“类C”语法，csh具有C语言风格的一种shell，其内部命令有52个，较为庞大，目前使用的不多，已经被bin/tcsh取代
- ksh：Korn shell 的语法与Bourne shell相同，同时具备了C shell的易用特点，许多安装脚本都使用ksh，有42条内部命令，与bash相比有一定的限制性。
- tcsh：是csh的增强版，与C shell完全兼容。
- sh：是一种快捷方式，已经被/bin/bash所取代。
- nologin：指用户不能登录
- zsh：目前最为庞大的一种shell，有84个内部命令，使用起来比较复杂，一般情况下，不会使用该shell。

<br/>

- **bash**：大多数Linux系统默认使用的shell，bash shell是Bourne shell的一个免费版本，他是最早的Unix shell，bash还有一个特点，可以通过help来查看帮助，包含的功能几乎包含shell的所有功能，所以一般的shell脚本都会指定他为执行路径。

<br/><br/><br/><br/>

#### （2）shell入门

<br/>

编写规范：

```
代码规范：
#!/bin/bash       【指定告知系统当前这个脚本要使用的shell解析器】
shell命令
```

使用流程：

```
① 创建.sh文件
② 编写shell代码
③ 执行shell脚本      脚本必须有执行权限
```

注意：

- 在每一句shell代码的后面可以加冒号也可以不加，但是如果一行中有多句shell代码，则每一句后面都要加。
- 想要直接输出内容，如果包含字母和符号（不包含变量），则需要用引号包括起来。如果是纯数字，可以不包。
- 运行时一定要写成./文件名，而不能直接写文件名，运行其他的二进制文件也是一样的，直接写成文件名，Linux的话系统会去PATH中去找有没有叫 这个文件名，而只有/bin，/sbin，/usr/bin，/usr/sbin等在PATH中，所以你的目录不在PATH中，就会找不到。

<br/>

单引号与双引号注意点：

- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的
- **单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用**。
- 双引号里可以有变量
- 双引号里可以出现转义字符

<br/>

案例：使用root用户账号创建并执行shelltest.sh，是先创建一个shelltest用户，并在其家目录中创建文件try.html。

<nr/>

![image-20211012173331705](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux37.png)

![image-20211012173452966](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux38.png)

<br/><br/><br/><br/><br/><br/><br/><br/>

### 2.shell进阶

<br/>

#### （1）变量

<br/>

##### ① 变量的含义

<br/>

a.什么是量？

量就是数据

b.什么是变量？

就是可以变得数据

在一个脚本周期内，气质可以发生改变的亮

c.什么叫做一个脚本周期？

可以理解为当前的shell文件

变量是shell中不可或缺的一部分，也是最基础，最重要的一部分。

<br/><br/>

##### ② 变量的定义和使用

<br/>

变量：先定义后使用。

<br/>

定义如：str=“linux”

使用如：ecoh $str

<br/>

定义的第一部分就是变量名，第二部分就是变量的值。（**之间“=”两边都不要有空格**）

变量名的规范：

- 在使用变量名之前必须有$
- 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头
- 名称中间不能有空格，但可以有下划线
- 不能使用标点符号
- 不能用bash中的关键字

<br/>

关于单双引号之间的问题：

- 双引号能够识别变量，双引号能够识别转移字符（“  \ ” ）
- 单引号不能识别变量，只能直接输出

<br/>

注：**要想在变量中使用命令，就需要在命令的两端加上“ ` ”（esc下面）**

<br/><br/>

##### ③ 只读变量

<br/>

语法：readonly 变量名

注：可以在定义变量时加入，也可以在变量定义后再后面加入

<br/>

![image-20211012195746054](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux39.png)

<br/><br/>

##### ④ 接收用户输入

<br/>

语法：read -p  "提示信息"   变量名

当接收输入的数值时，用 "$变量名" 之后就是自己输入的值，不需要转义。

<br/>

![image-20211012200207781](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux40.png)

<br/><br/>

##### ⑤ 删除变量

<br/>

语法：unset  变量名

<br/><br/><br/><br/>

#### （2）条件判断语句

<br/>

[ command ]，在命令的两端必须有空格，不然识别不出来。

<br/>

语法一（一个条件）：

```
if [condition]
then
    command1
    command2
    ...
fi
```

<br/>

单行写法（一般在命令行中执行的时候）：if [ condition ];then command;fi

<br/>

语法二（两个条件）：

```
if [condition]
then
    command1
    command2
    ...
else
    command
fi
```

<br/>

语法三（多个条件）：

```
if [condition1]
then
    command1
    command2
    ...
elif [condition2]
then
    command
    ...
elif ...
else
    command
fi
```

<br/><br/><br/><br/>

### 3.运算符

<br/>

在shell中，运算符和其他编程脚本是一样的，常见的有算术运算符，关系运算符，逻辑运算符，字符串运算符，文件测试符等。

<br/>

#### （1）算术运算符

<br/>

下表列出了常用的算术运算符，假定变量 a 为 10，变量 b 为 20.

| 运算符 | 说明 | 举例              |
| ------ | ---- | ----------------- |
| +      | 加法 | \`expr $a + $b\`  |
| -      | 减法 | \`expr $a - $b\`  |
| *      | 乘法 | \`expr $a \* $b\` |
| /      | 除法 | \`expr $a / $b\`  |
| %      | 取余 | \`expr $a % $b\`  |
| =      | 赋值 | a=$b              |
| ==     | 相等 | [$a == $b]        |
| ！=    | 不等 | [$a != $b]        |

注意：

- 条件表达式要放在方括号之间，并且要有空格，例如[$a==$b]是错的，必须写成[$a == $b]
- expr为命令，后面的数字和符号之间要有空格
- 原生的bash不知处简单的算数运算，但是可以通过其他命令来实现，例如：awk和expr

<br/>

**expr相关：**

expr 是一种表达式计算工具，使用它能够完成表达式的求值操作

注意：

- 表达式和运算符之间要有空格
- 在脚本中使用外部命令时，要用“ `` ”将命令括起来

<br/>

![image-20211012215324862](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux41.png)

<br/><br/><br/><br/>

#### （2）关系运算符

<br/>

关系运算符只支持数字，除非字符串的值是数字。

<br/>

下表列出了常用的关系运算符，假定变量a为10，b为20

| 运算符 | 说明                           | 举例          |
| ------ | ------------------------------ | ------------- |
| -eq    | 检测两数是否相等               | [ $a -eq $b ] |
| -ne    | 检测两数是否不相等             | [ $a -ne $b ] |
| -gt    | 检测左边的是否大于右边的       | [ $a -gt $b ] |
| -lt    | 检测左边的数是否小于右边的     | [ $a -lt $b ] |
| -ge    | 检测左边的数是否大于等于右边的 | [ $a -ge $b ] |
| -le    | 检测左边的数是否小于等于右边的 | [ $a -le $b ] |

<br/><br/><br/><br/>

#### （3）逻辑运算

<br/>

| 运算符 | 说明   | 举例                        |
| ------ | ------ | --------------------------- |
| ！     | 非运算 | [ !false ]                  |
| -o     | 或运算 | [ $a -lt 10 -o $b -gt 100 ] |
| -a     | 与运算 | [ $a -lt 10 -a $b -gt 100 ] |

<br/><br/><br/><br/>

#### （4）字符串运算符

<br/>

| 运算符 | 说明                                     | 举例         |
| ------ | ---------------------------------------- | ------------ |
| =      | 检测两个字符串是否相等，相等返回true     | [ $a = $b ]  |
| !=     | 检测两个字符串是否不相等，不相等返回true | [ $a != $b ] |
| -z     | 检测字符串的长度是否为0，为0返回true     | [ -z $a ]    |
| -n     | 检测字符串长度是否为0，不为0返回true     | [ -n $a ]    |
| 空     | 检测字符串是否为空，不为空返回true       | [ $a ]       |

<br/><br/><br/><br/>

#### （5）文件测试运算符

<br/>

| 操作符  | 说明                         | 举例         |
| ------- | ---------------------------- | ------------ |
| -d file | 检测文件是否是目录           | [ -d $file ] |
| -f file | 检测文件是否是普通文件       | [ -f $file ] |
| -r file | 检测文件是否可读             | [ -r $file ] |
| -w file | 检测文件是否可写             | [ -w $file ] |
| -x file | 检测文件是否可执行           | [ -x $file ] |
| -e file | 检测文件（包括目录）是否存在 | [ -e $file ] |

<br/><br/><br/><br/>

### 4.shell脚本附带选项

<br/>

作用：在执行脚本文件时，将自己写的一些选项加在上面，实现在一个脚本中将简化多种操作。

实现：#./test.sh  选项一 选项二 【文件】

接收：在脚本中可以用$0接受文件本身，$1接收选项一，$2接收选项二。

附加：可以使用起别名的方式将脚本文件的运行简化。

<br/><br/><br/><br/><br/><br/><br/><br/>

## （七）额外拓展

<br/>

### 1.网络相关命令

<br/>

#### （1）ping

<br/>

作用：检测当前主机与目标主机之间的连通性（不是100%准确，有些服务器是禁ping）

语法：#ping 主机地址（ip地址，主机名或域名等）

该命令可以跨平台，windows下默认发送四个，而linux默认无限发

<br/><br/><br/><br/>

#### （2）netstat

<br/>

（在指令的高级命令里也有这个）

作用：查看网络的连接信息

语法一：#netstat -tnlp

-t：tcp协议，-n：将字母转化为数字，-l：列出状态为监听，-p：显示进程相关信息

<br/>

语法二：#netstat -an

-a：表示全部，-n：表示数字

在TCP/IP协议需要使用这个命令

<br/><br/><br/><br/>

#### （3）traceroute

<br/>

用法：#traceroute 主机地址

作用：查找当前主机与目标主机之间的所有的网关（路由器，会给沿途的各个路由器发送icmp数据包，路由器可能不会响应）

<br/>

在windows中也有类似的命令，tracert

<br/><br/><br/><br/>

#### （4）arp

<br/>

地址解析协议，即ARP（Address Reso Protocol），是根据ip地址获取物理地址的协议。

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/linux36.png" alt="image-20211011230906115" style="zoom:80%;" />

<br/>

解释：当一个主机发送数据时，首先查看本机MAC地址缓存中有没有目标主机的MAC地址，如果有就使用缓存中的结果;如果没有，ARP协议就会发出一个广播包，该广播包要求查询目标主机IP地址对应的MAC地址，拥有该IP地址的主机会发出回应，回应中包括了目标主机的MAC地址,这样发送方就得到了目标主机的MAC地址。如果目标主机不在本地子网中，则ARP解析到的MAC地址是默认网关的MAC地址。

<br/>

语法：#arp -a

作用：查看本地的网络地址缓存表

注：在windows中也适用

<br/><br/><br/><br/><br/><br/><br/><br/>

### 2.软件包解压

<br/>

常用语法：

​         #tar -zxvf  *.tar.gz

​         #tar -jxvf  *.tar.bz2

选项含义：

- -z 或 --gzip或 --ungzip：通过gzip指令处理文件
- -j：支持bzip解压文件
- -x 或 --extract或 --get：从文件中还原文件
- -v：显示操作过程
- -f或 --file：指定一个文件



<br/><br/><br/><br/><br/><br/><br/><br/>

### 3.软件安装

<br/>

（操作前先保证时间准确）

<br/>

#### （1）安装方式

<br/>

##### ① 源码包

<br/>

优点：

​        开源，如果有足够的能力，可以修改源代码

​        编译安装，更加适合自己的系统

缺点：

​         安装步骤较多，容易出错

​         编译过程时间较长

<br/>

配置（config/configure/bootstrap） ->  编译（ make/bootstrapd ） -> 安装（make install/bootstarp ）

配置操作主要是指定软件的安装目录、需要安装在什么地方、指定不需要可选依赖、配置文件的路径、通用数据存储位置等等。

指定安装的路径：--prefix=路径

需要依赖的路径：--with-PACKAGE 包名=包所在路径

不需要依赖：--without-PACHAGE 包名

<br/>

案例：使用源码编译安装的方式安装ncurses

第一步：下载ncurses安装包

```
 wget https://ftp.gnu.org/pub/gnu/ncurses/ncurses-6.1.tar.gz --no-check-certificate
 这个网站的sll证书已经过期，要加--no-check-certificate忽略网站是否安全

```

第二步：解压安装包

```
tar -zxvf ncurses-6.1.tar.gz
```

第三步：进入解压好的文件，配置安装地址

```
./configure --prefix=/usr/local/ncurses
```

第四步：编译

```
make
```

第五步：安装

```
make install
```

<br/><br/><br/>

##### ② 二进制包

<br/>

优点：包管理系统简单，只需要几个命令就可以是实现包的安装，升级，查询和卸载

缺点：进过编译，不可以在看到源代码

<br/>

去官网下载rpm包：

输入：rpm -ivh 安装包名

安装时可能遇到各种依赖问题，建议将依赖全部下载。

即可完成安装

<br/><br/><br/>

##### ③ yum 等傻瓜式安装

<br/>

优点：

​      安装简单，快捷

缺点

​       完全丧失了自定义性

注意：需要联网才能使用

<br/>

常用的yum命令：

#yun list                                   列出当前已经安装和可以安装的软件（全部）

#yum search                            搜索指定的关键词的包

#yum 【-y】install 包名           安装指定的包（-y 表示允许，不在确认）

#yum 【-y】install 包名           更新指定功能的包，不指定包则更新全部部件

#yum 【-y】install 包名            卸载指定的包

<br/><br/><br/><br/><br/><br/><br/><br/>

### 4.CentOS7安装mysql5.6

<br/>

**此文章为知乎佞臣原创：https://zhuanlan.zhihu.com/p/83470848**

<br/>

（1）检查系统中是否已安装 MySQL。

```text
rpm -qa | grep mysql
```

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux42.png)

<br/>

返回空值的话，就说明没有安装 MySQL 。

**注意：**在新版本的CentOS7中，默认的数据库已更新为了Mariadb，而非 MySQL，所以执行 yum install mysql 命令只是更新Mariadb数据库，并不会安装 MySQL 。

<br/>

![](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux51.jpg)

<br/>

（2）查看已安装的 Mariadb 数据库版本。

```text
rpm -qa|grep -i mariadb
```

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux48.png)

<br/>

（3）卸载已安装的 Mariadb 数据库。

```text
rpm -qa|grep mariadb|xargs rpm -e --nodeps
```

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux52.png)

<br/>

（4）再次查看已安装的 Mariadb 数据库版本，确认是否卸载完成。

```text
rpm -qa|grep -i mariadb
```

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux53.png)

<br/>

（5）下载安装包文件。

```text
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
```

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux54.jpg)

<br/>

（6）安装mysql-community-release-el7-5.noarch.rpm包

```text
rpm -ivh mysql-community-release-el7-5.noarch.rpm
```

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux43.png)

<br/>

安装完成之后，会在 /etc/yum.repos.d/ 目录下新增 mysql-community.repo 、mysql-community-source.repo 两个 yum 源文件。

<br/>

执行 yum repolist all | grep mysql 命令查看可用的 mysql 安装文件。

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux44.jpg)



<br/>

（6）安装mysql。

```text
yum install mysql-server
```

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux45.jpg)

<br/>

（7）检查mysql是否安装成功。

```text
rpm -qa | grep mysql
```

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux46.jpg)

<br/>

（8）启动 mysql 服务 。



systemctl start mysqld.service #启动 mysql

systemctl restart mysqld.service #重启 mysql

systemctl stop mysqld.service #停止 mysql

systemctl enable mysqld.service #设置 mysql 开机启动

<br/>

（9）设置密码 。

mysql5.6 安装完成后，它的 root 用户的密码默认是空的，我们需要及时用 mysql 的 root 用户登录（第一次直接回车，不用输入密码），并修改密码。

```text
# mysql -u root
mysql> use mysql;
mysql> update user set password=PASSWORD("这里输入root用户密码") where User='root';
mysql> flush privileges;
 
```

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux47.jpg)

<br/>

（10）设置远程主机登录



mysql> GRANT ALL PRIVILEGES ON *.* TO 'your username'@'%' IDENTIFIED BY 'your password';

执行以下命令，为root 用户添加远程登录的能力。

**这是需要先将防火墙的3306端口打开，才能远程连接**

```
*# 开放端口*
firewall-cmd --zone=public --add-port=3306/tcp --permanent 
*# 重启防火墙*
systemctl restart firewalld.service
```



mysql> GRANT ALL PRIVILEGES ON *.* TO root@"%" IDENTIFIED BY "123456";

<br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux49.jpg)

<br/>

到这里mysql就安装好了！

<br/><br/><br/><br/><br/><br/><br/><br/>

### 5.nginx的下载与安装

<br/>

#### （1）环境准备

<br/>

（1）需要安装 gcc 的环境【此步省略】

yum install gcc-c++

<br/>

（2）第三方的开发包。

<br/>

**PCRE**

  PCRE(Perl Compatible Regular Expressions)是一个 Perl 库，包括 perl 兼容的正则表达式库。nginx 的 http 模块使用 pcre 来解析正则表达式，所以需要在 linux 上安装 pcre 库。

yum install -y pcre pcre-devel

注：pcre-devel 是使用 pcre 开发的一个二次开发库。nginx 也需要此库。

<br/>

  **zlib**

<br/>

zlib 库提供了很多种压缩和解压缩的方式，nginx 使用 zlib 对 http 包的内容进行 gzip，所以需要在 linux 上安装 zlib 库。

yum install -y zlib zlib-devel

<br/>

 **OpenSSL**

OpenSSL 是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及 SSL 协议，并提供丰富的应用程序供测试或其它目的使用。nginx 不仅支持 http 协议，还支持 https（即在 ssl 协议上传输 http），所以需要在 linux安装 openssl 库。

yum install -y openssl openssl-devel

<br/><br/><br/>

#### （2）Nginx下载

<br/>

官方网站下载 nginx：http://nginx.org/

<br/>

#### （3）Nginx安装

<br/>

第一步：把 nginx 的源码包nginx-1.8.0.tar.gz上传到 linux 系统

第二步：解压缩

tar zxvf nginx-1.8.0.tar.gz

第三步：进入nginx-1.8.0目录  使用 configure 命令创建一 makeFile 文件。

```
./configure \
--prefix=/usr/local/nginx \
--pid-path=/var/run/nginx/nginx.pid \
--lock-path=/var/lock/nginx.lock \
--error-log-path=/var/log/nginx/error.log \
--http-log-path=/var/log/nginx/access.log \
--with-http_gzip_static_module \
--http-client-body-temp-path=/var/temp/nginx/client \
--http-proxy-temp-path=/var/temp/nginx/proxy \
--http-fastcgi-temp-path=/var/temp/nginx/fastcgi \
--http-uwsgi-temp-path=/var/temp/nginx/uwsgi \
--http-scgi-temp-path=/var/temp/nginx/scgi
```

执行后可以看到Makefile文件

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux56.jpg) 



```
----  知识点小贴士 ----
Makefile是一种配置文件， Makefile 一个工程中的源文件不计数，其按类型、功能、模块分别放在若干个目录中，makefile定义了一系列的规则来指定，哪些文件需要先编译，哪些文件需要后编译，哪些文件需要重新编译，甚至于进行更复杂的功能操作，因为 makefile就像一个Shell脚本一样，其中也可以执行操作系统的命令。

----  知识点小贴士 ----
configure参数
./configure \
--prefix=/usr \                                                        指向安装目录
--sbin-path=/usr/sbin/nginx \                                 指向（执行）程序文件（nginx）
--conf-path=/etc/nginx/nginx.conf \                      指向配置文件
--error-log-path=/var/log/nginx/error.log \              指向log
--http-log-path=/var/log/nginx/access.log \            指向http-log
--pid-path=/var/run/nginx/nginx.pid \                      指向pid
--lock-path=/var/lock/nginx.lock \                         （安装文件锁定，防止安装文件被别人利用，或自己误操作。）
--user=nginx \
--group=nginx \--with-http_ssl_module \                      启用ngx_http_ssl_module支持（使支持https请求，需已安装openssl）
--with-http_flv_module \                       启用ngx_http_flv_module支持（提供寻求内存使用基于时间的偏移量文件）
--with-http_stub_status_module \     启用ngx_http_stub_status_module支持（获取nginx自上次启动以来的工作状态）
--with-http_gzip_static_module \   启用ngx_http_gzip_static_module支持（在线实时压缩输出数据流）
--http-client-body-temp-path=/var/tmp/nginx/client/ \ 设定http客户端请求临时文件路径
--http-proxy-temp-path=/var/tmp/nginx/proxy/ \ 设定http代理临时文件路径
--http-fastcgi-temp-path=/var/tmp/nginx/fcgi/ \ 设定http fastcgi临时文件路径
--http-uwsgi-temp-path=/var/tmp/nginx/uwsgi \ 设定http uwsgi临时文件路径
--http-scgi-temp-path=/var/tmp/nginx/scgi \ 设定http scgi临时文件路径
--with-pcre 启用pcre库
```



第四步：编译

make

<br/>

第五步：安装

make install

<br/><br/>

#### （4）Nginx启动与访问

<br/><br/>

注意：启动nginx 之前，上边将临时文件目录指定为/var/temp/nginx/client， 需要在/var  下创建此 目录

mkdir /var/temp/nginx/client -p

进入到Nginx目录下的sbin目录

cd /usr/local/ngiux/sbin

输入命令启动Nginx

./nginx

启动后查看进程

ps aux|grep nginx

 <br/>

![img](https://cdn.jsdelivr.net/gh/hemeilun/picture/linux55.jpg) 

<br/>

地址栏输入虚拟机的IP即可访问（默认为80端口）

 关闭 nginx：

./nginx -s stop

或者

./nginx -s quit

<br/>

重启 nginx：

1、先关闭后启动。

2、刷新配置文件：

./nginx -s reload