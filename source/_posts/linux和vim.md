---
title: linux和vim
date: 2021-06-18 22:46:17
tags:
  - linux基本指令和vim使用
categories:
  - 后端杂项
---

```
## 常用linux命令

0. 命令的语法格式为：命令名 + 选项 + 参数
1. date 返回系统当前时间
2. sudo apt install name 下载包，1.8版本后从apt-get优化到apt，sudo是以管理员身份运行。
3. cd / 用绝对路径的方法进入系统跟目录
4. ls 获取当前目录下所有文件或者文件夹
5. sudo reboot 重启系统
6. clear 清除命令行解释器屏幕。
7. cd 不带目录会回到该用户的家目录，注意不是home目录，home目录存放所有用户的家目录
8. sudo su 用户名 切换用户。
9. history 查看之前执行过的终端命令：
10. ls -l详细查看某一文件说明之后-rw-rw-r-- 1 fxy fxy 0 Jun 15 18:59 1.tx输出的语法
   -rw-rw-r--  文件属性字符串 一般来说共有十个字符，
               第一个字符- 表示普通文件
                       d 目录文件
                       l 软连接文件
                       c 字符设备文件
                       b 块设备文件
                       s 套接字文件
                       p 管道文件
               后九个字符分为三组 每三个字符为一组
                       第一组（wr-）表示文件所有者的权限： 可读可写可执行中的可读可写
                       第二组（wr-）文件所属组的权限：可读可写
                       第三组（r--）其他用户的权限：可读

   1           文件硬链接数量
   fxy         文件所属用户
   fxy         文件所属用户组
   0           文件所占用字节大小
   Jun 15 18:59文件最后一次创建或者修改时间
   1.tx        文件名
11. ln 文件 硬链接文件名 为指定文件创建硬链接 (硬链接可以理解为实现了数据同步备份文件！不同于软连接，指向同一个文件)
           硬链接源文件删除不影响硬链接文件。软连接源文件删除文件就真都删除了
12.cat 文件 捕获文件中的内容
13.rm 文件 删除指定文件路径的文件
14.stat 文件 查看单个文件的详细描述
15.mkdir 目录名 用来创建一个目录
16.命令 + --help 查看一个命令的帮助文档信息
17.ls -l > info.txt  通过>输出重定向，将控制台数据导入指定文件中，文件路径不存在就创建
   注意：只有一个重定向符是覆盖输出到一个文件中，两个重定向符是追加到文件中。
18.more 文件 在控制台输出文件内容，但不是一次性全部输出，和cat 文件命令的区别
19.tac 文件，捕获文件内容输出在控制台，但是输出顺序按行逆序
20.pwd 查看当前工作目录
21.mkdir a/b/c -p 通过p选项递归创建文件夹
22.rmdir 目录 删除目录，且目录必须是空目录
23.rm 目录 -r 递归删除目录，rm默认情况下只能删除文件，通过r选项可删除目录，
24.ln -s 源文件路径 产生文件路径 通过s选项创建软连接，不带s选项创建硬链接
   注意：可以给目录创建软连接，但是不能给目录创建软链接
25.ps命令用来显示当前系统进程，常见的选项有-aux,会显示所有的进程，
26.grep命令用来过滤我们的输入，具体用法查看grep --help显示 ，比如查看所有启动的进程中有没有mysql
   ps -aux | grep mysql
27.cat txt1.txt txt2.txt > txt3.txt 将两个文本内容输出重定向到第三个文本中，
28.cp file.txt /home/fxy/a 拷贝file.txt文件到某个home目录中去。
29.cp -r file /home/fxy/a 拷贝file目录到某个目录中，r选项也可以替换为a，a选项不会对文件或者目录创建时间产生影响
30.mv 源文件路径 目标路径 命令用于移动文件到指定目录中去 ,移动文件还可以达到修改文件名的目的
31.file 文件或者目录 查看文件或者目录的内容类型等信息
32.gzip -s 文件目录 用于压缩文件或者目录，不带s选项只能打包文件，更多选项通过--help命令查看
   注意：gzip只能用于压缩文件或者目录，不能压缩文件或者目录，且默认不会保留文件或者目录(可以通过选项保留)
33.gunzip -s 文件或者目录，解包文件或者目录
34.bzip2 或者目录，用来打包文件或者目录，且不能压缩，和gzip差不多
35.tar命令用来打包我们的文件或者目录
36.tar -zcvf 打包后的文件或者目录名  文件或者目录
   z 表示gzip格式压缩  j表示以bzip2的格式压缩
   c  表示创建压缩文件  解压的时候配置选项为x
   v  输出压缩详细
   f  指定压缩后的文件名
37.tar -zxvf info.tar.gz 解压打包压缩后的文件注意配置选项是zxvf，x选项表示解开压缩文件。不带选项可能会
38.zip命令和rar命令打包压缩文件或者目录常用需要安装该包，这些包不是linux内核的包
   当我们安装了zip和rar工具之后可以使用如下命令打包压缩该格式的文件或者目录
   ~$ zip -r zip_info data_info 用zip打包压缩文件或者目录  解压命令用unzip 源文件或者目录
   ~$ rar a -r my.rar file*     用rar打包压缩文件或者目录  解压命令用rar x 源文件或者目录

## 和用户、组权限相关

39.which 命令 查看命令文件所在的路径位置 注意window系统中才是where
40.whoami 查看当前用户
41.exit  退出当前用户
42.su 用户名 切换用户  该命令切换用户名不修改当前工作目录 su -用户名 该命令切换用户且修改工作目录
43.sudo su 切换root用户和普通用户
44.sudo adduser 用户名 添加用户
45.sudo deluser 用户名 删除用户  删除这个用户，但是组没有删除，且用户家目录下产生的文件不会删除，且不能在当前用户下删除这个用户
46.sudo chown 用户名 文件 修改文件的所有者为指定用户，但是用户组不受影响
47.sudo addgroup 组名 添加组
48.sudo delgroup 组命 删除组
49.sudo chgrp 组命 文件  修改文件所属组
50.passwd 更改当前用户的密码
51.sudo -R chmod 536 文件 以分组数字法修改文件的权限，注意文件权限中r权重为4，w的权重为2，x的权重为1
   R：选项表示递归修改某一目录下的所有文件的权限属性，
   5：权限属性第一组：表示r权限 + x权限
   3：权限属性第二组：表示w权限 + x权限
   6：权限属性第三组：表示r权限 + w权限

## 和系统管理相关的命令

52.ps -aux | grep redis 过滤显示是否有某个进程
53.top 显示进程详细信息，会自刷新
54.kill -9 进程id  杀死某个进程id的进程，进程id不等同与端口
   9选项是一个可靠的强制杀死进程的信号的别名，（所有信号可通过kill -l查看）建议杀死进程的时候带上。
     1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
     6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
    11) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM
    16) SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
    21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU     25) SIGXFSZ
    26) SIGVTALRM   27) SIGPROF     28) SIGWINCH    29) SIGIO       30) SIGPWR
    31) SIGSYS      34) SIGRTMIN    35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3
    38) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
    43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
    48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
    53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7
    58) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
    63) SIGRTMAX-1  64) SIGRTMAX
55.命令 &将命令挂起后台
56.jobs 查看后台挂起运行的进程
57.fg 恢复后台一个进程到前台执行。 可以带一个挂起进程编号以恢复指定后台挂起进程
58.reboot 重启
59.shutdown -r now指定时候关机
60 init 0/ 6 进行关机重启。这个命令也可以
61.ifconfig 查看所有网卡信息， window下查看网卡信息的命令为ipconfig
   一般情况下会有多个网卡信息，第一个一般我们需要的网卡信息，eth1为网卡名（名字是随意的）
62.find命令用来搜索文件：其语法格式为：
    find 目录位置 参数 搜索关键字  关键字需要带上引号
    参数可是是-name表示按名字搜索。
    参数可能是-type表示按类型进行搜索。 类型主要有 f、d、l、b、p、s
    参数可能是-size表示大小进行进行搜索， 语法格式 find ./a -size +10M -size -100M 单位可以使B k M G
    find命令默认会一直往下搜索。可以通过选项-maxdepth 1 指定，其位置放在find命令的位置参数后。
    find命令可以通过and选项加多个条件：语法格式为  find ./ -name ".png" and -type "f"
63.grep -r/R 文件内容 递归的按照文件内容进行查找。
## 和文件修改有关的vim gedit
64.sudo apt install vim
    （1）vim编辑器有三种工作模式，命令模式、编辑模式、末行模式。
        默认情况下进入命令模式： 按i、a、o、s和其大写的，进入编辑模式
        命令模式按：进入末行模式。 按w进行保存 按q进行退出、q！不保存退出。x表示保存并退出。
        在命令模式下按ZZ(大写)进行保存退出
    （2）vim编辑器的移动：
        在vim编辑器中，键盘上连续的hjkl分别表示左下上右。
        这四个键中外面的表示左右移动，里面的表示上下移动。左右移动的键中，左边的表示左移，右边的表示右移。
    （3）进入编辑模式的四种方式详解： 记得话就记iaos
        i 表示向光标所在位置的前面插入数据。
        a 表示向光标所在位置的后面插入数据
        o 表示向光标所在位置的下一行插入数据
        s 以删除光标位置一个字符为代价修改模式，也就是说进入编辑模式的时候会删除光标位置的字符
        O 大写 表示向光标所在位置的上一行插入数据。
        I 大写 表示向光标所在位置的行首插入数据。
        A 大写 表示向光标所在位置的行尾插入数据。
        S 大写 以删除光标所在行为代价修改模式，也就是说进入编辑模式的时候会删除光标位置的字符
    （3）在命令行模式下：按小写yy赋值光标所在行，按小写p粘贴在下一行，大写P粘贴在上一行。
        yy前可带上数据表示我们想要从光标所在行开始复制几行，比如 2yy 复制光标所在行及下一行。
        yw表示复制一个单次，此时光标要放置在单次首字母。
        如何完成区域复制，移动光标在需要复制的首字符上，然后按v进行区域选择，然后按y就能就行复制了
        然后按p粘贴在我们想要的地方就行。
        主要是区域选择在复制的话只需要一个y
    （4）在命令行模式下，完成内容的剪贴。
        小写dd表示剪切一行，dd前可以带上数字表示向下剪切指定行。
        dw表示剪切一个单次。
        区域剪切：移动光标在指定的区域中，然后按v进入视图区域，然后移动选择区域，然后一个小写d剪切视图选择区域。
        只要是区域操作，按一个d就可以完成剪切
    （5）在命令行模式下一个小写的x表示剪切一个字符，x命令前可以带上数字表示剪切指定个字符。
         移动光标在指定字符上，按r进入替换模式，然后按指定字符，就会将光标所在字符替换为该字符。
    （6）在命令行模式下按住$就能进入光标所在行的行尾。
    （7）在命令行模式下，移动光标在行首行尾或者指定行。
        小写的gg表示跳转到行首。
        大小的G表示跳转到行尾。
        数字加小写的gg表示跳转到指定行。
    （8）在末行，模式下按set nu 表示设置行号。
    （9）在打开文件的时候可以按vim +文件名 + 数字 表示打开文件时跳转到指定行。
    （10）在命令行模式下小写的gg =G的时候格式化文档。
    （11）在命令行模式下按/字符串 然后回车，就可以再文档中查找指定字符串了。
         另一种查找字符串的方法：适用于查找一个已经看到的单次：具体用法如下：
         移动光标在该单词身上、然后*向前查找，#向后查找。
    （12）在命令行模式下，按u撤销，
    （13）在命令行模式下，按ctrl + r 反撤销。
    （14）替换的另一种方式就是使用末行模式：通过正则来完成替换操作。举例如下。
        %s/需要替换的字符串/替换后的字符串   %表示选定所有行，s表示启用正则。
        注意%也可以替换为指定行到指定行，将来替换操作将只替换指定行。用法如下:
        1,20s/da/ad
        注意：通常情况下一行如果匹配了一次就会进行下一行的匹配，如果要替换一行中所有需要替换的字符串。需要带g
        具体用法：  10,20s/print/Println/g
    （15）注意给vim设置配置文件的方式有两种，一种是在/etc目录下给所有用户配置vim配置
        一种是在当前用户家目录下配置用户自己的配置文件。默认是不带的，需要用户创建一个.vimrc配置文件。
65. sudo apt show 软件名  -- 未安装，
66. ssh 用户名@远程地址  链接服务器，在服务器安装  通过远程登录或者链接可以向服务器传递文件。
67. scp -r 目标用户名@主机ip：存储绝对路径  向远程服务器某路径下拷贝文件。
68. window借助工具链接linux。
```


```
1. linux非桌面系统的使用
2. unix系统是内核系统，其衍生系统有很多，包括ubantu linux mac
3. linux系统无盘符概念，只有一个跟目录。
4. shell是niux命令解析器，默认运行在终端当中的程序（进程）
5. bash就是我们linux版的shell，作用还是解析命令
6. 所有的可执行文件都存放在我们的根目录的bin目录下
7. 在linux中操作系统中，所见皆文件。
8. 由于linux操作系统中，所见皆文件，和硬件设备对应的文件存放在根目录下dev目录下。
9. 根目录下的etc目录用来存放系统的配置文件，几乎所有软件的配置文件都要写到我们etc目录下。
10.根home目录用来记录当前操作系统有多少用户。具体某个用户的操作都在自己的home目录下。
11.linux是一款多用户多任务的分时复用操作系统。
12.注意home和家目录不是同一样的，每个用户都有自己的家目录，home目录下用来存放所有用的家目录。
13.根目录下的lib目录用来存放系统所使用的函数库目录。
14.系统管理员用户存放在我们根目录下root目录，home目录用来存放我们的普通用户。
15.sbin目录用于存放管理员的bin的函数库。
16.根目录下tmp目录用来存放我们的临时目录。
17.根目录下的srv目录用来存放服务启动之后需要访问的数据目录，
18.根目录下的usr目录用来存放我们的应用程序的目录，
19.linux系统不已文件后缀区分我们的文件类型，而是以文件属性区分我们的文件类型
20.什么是硬链接，硬链接是linux操作系统所独有的一个东西，硬链接的文件可以达到文件同步的效果。
21.其实硬链接文件共用一个inode编号，我们写数据会通知这个inode编号下的所有文件写数据所以达到了文件同步的效果
22.linux系统中以点开头的文件是隐藏文件，
23.ls命令可以配合通配符去查找我们的文件 通配符的匹配规则有点类似正则表达式。
24.rm命令删除的文件是不可恢复的
25.用相对路径创建的软连接在移动软连接之后可能会出现无法访问的情况。
26.管道符：用来将我们的前面命令的输出内容作为后面命令的输入，管道符通常用来链接两个命令！
27.fxy@admin:~/itca$ 命令行该提示信息的解释说明：
   fxy 表示当前用户
   @   表示at在哪个主机上
   admin表示主机
   ：  固定写法
   ~/tca表示当前工作目录，~代表当前用户的家目录
   $   表示用户身份为普通用户，root用户提示符为#
28.当工作路径较长的时候我们可以进入根目录下的bashrc文件修改配置隐藏工作目录，只显示用户身份标识
29.linux操作系统下默认支持两种压缩方式：gzip bzip2
30.注意有时候使用root用户权限不需要输入密码是因为在近期很短的时间内已经输入过了
31.默认情况下注册一个用户，该用户就会对应一个用户组
32.注意目录默认是带有执行权限的
33.前台进程和后台进程的判别标准：是否能与用户进行交互！
32.服务器安装ssh之后我们就可以远程登录我们的服务器了,具体使用查看如下。


```