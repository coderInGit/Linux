# Linux学习笔记
## 第一章 Linux起源
unix，C语言，TCP-IP 可以看作三胞胎，他们结合在一起相互诞生，其他具体自行可以看：计算机组成原理，计算机网络，以及C语言。可以结合在一起来学习，效果更佳。
## 第二章 系统分区
Linux与Windows一样，它的主分区和拓展分区加起来不能超过四个，而且拓展分区最多一个且不能放入数据文件以及它不能格式化，拓展分区里放的逻辑分区可以放数据和格式化。
Linux 硬件全为文件 这一点与Windows不一样，下面介绍一些Linux的主要硬件文件名已经存放路径。
* IDE硬盘 /dev/hd[a-d]
* SCSI/SATA/USB硬盘 /dev/sd[a-p]
* 光驱 /dev/cdrom或/dev/sr0
* 软盘 /dev/fd[0-1]
* 打印机（25针） /dev/lp[0-2]
* 打印机（USB） /dev/usb/lp[0-15]
* 鼠标 /dev/mouse
## 第三章 Linux安装与配置
在Linux远程登录管理配置IP时，需要的一些简单命令：
```
  ifconfig  查询当前网卡信息
  ifconfig eth0  配置网卡 
  ifconfig eth0 后+ VmNAT8的网络IP   
  df    查看系统分区
  ls /bin/   里面存放的为Linux命令文件  
```
注意：这些配置都是临时配置，在重启之后IP会丢，永久修改需要在配置文件中修改
VmNAT8为VMware虚拟中虚拟网卡 可以自行查询IP
具体操作看以下视频：
链接: [VMware环境配置](https://www.bilibili.com/video/BV1mW411i7Qf?p=9 "VMware环境配置")

## 第四章 Linux常用命令
 * 第一节 文件处理命令
 
   1. 第一讲 命令格式与目录处理命令ls
       * 以下为不同文件的不同后缀
         压缩包：.gz .bz2 .tar.bz2 .tgz
         二进制软件包：.rpm
         网页文件：.html .php
         脚本文件：.sh
         配置文件：.conf 
       * 注意： Linux不靠扩展名区分文件信息，而且所有存储设备必须挂载后方可使用（硬盘，U盘，光盘）
       * 一些主要目录
        /bin/ ( bin的意思是二进制可执行文件)
        /sbin/
        /usr/bin/
        /usr/sbin/
        /boot/:系统启动相关数据。需要备份时 /boot目录（也需备份）
        /dev：硬件信息 设备文件保存文字
        /etc :（也需备份） 配置文件保存位置 如账 户，密码
        /lib/ :系统函数保存位置 （也需备份）
        /lost+found/:意外关机或者系统崩溃产生的碎片文件 可以复原 家目录
        /media/: 挂载目录 软盘或光盘
        /mnt/: 挂载U盘或者移动硬盘
       * 空目录才可以作为挂载点
        例如：/mnt/cdrom 挂载光盘 /mnt/usb 挂载U盘
        /opt/ ：第三方软件保存位置 不过保存到/usr/local/里更好 为约定俗成的
        /proc/ :保存系统内核 进程的 例如CPU信息不能存放文件没有意义 内存占满死机 没满重启消失
        /sys/ :与proc一样 是在内存里的 不可以写东西 放内核信息
        /tmp/ ：临时目录 做练习
        /usr/：系统软件资源目录（也需备份）
        /var/: 动态数据保存 保存缓存，日志以及软件运行产生的文件（也需备份）
        ### 文中标记（也需备份）的为在服务器中使用进行安全备份时主要的备份目录 非常重要
        * 常用命令
         ls -a 查看隐藏文件
         ls -l 长显示,显示文件或者目录详细信息包括大小 修改时间
         ls -d 显示目录
         ls -h 更加人性化显示 比如字节转换为MB，GB 不用自己算
         ls -i 查询文件inode号(inode存储文件的详细信息) 信息编号，类似于人的身份证号码
        * 用户有三类
         第一类：所有者（只有一个）
         第二类：所属组
         第三类：其他人
         在 ls -l 查询文件详细信息后，第一列会出现类似：-rwxr-xr-x 这样的字符，其中开头的 - 便是代表这个文件是二进制文件的意思，以下为其他开头的含义：
         -：二进制文件
         d：目录
         l ：软链接文件
         r 代表可以读 w 代表可以写 x代表可以执行
         -rwxr-xr-x
        -(rwx)(r-x)(r-x ) Linux中的文件以这种方式来显示不同用户的不同权限
        u g o
        u 所有者 g 所属组 o 其他人
        -(rwx)(r-x)(r-x )说明这个文件：所有者可以读，写，执行；所属组可以读和执行，但是不能写；其他人可以读和执行，但是不能写。

   2. 第二讲 目录处理命令
       * mkdir 创建目录 在/tmp/目录下创建临时文件 只能创建/tmp/***** 二级目录
       mkdir -p 可以递归创建 在没有一级目录的情况下新创建二级目录
       pwd 显示当前所在路径
       cd . . 返回上一级目录(两个点连着）
       rmdir 删除空目录 只能删除没有文件的空目录 （不经常使用）
       cp 复制文件 cp [原文件路径][需要复制到的路径]
       cp -r 复制目录
       cp -p 保留原文件属性复制目录 比如保留创建时间 日志文件的复制需要用到
       cp -rp 复制目录并且保留原文件属性
       mv 剪切 改名（在同一个目录下为改名）
       rm 删除文件
       rm -f 强制删除 不再询问
       rm -r 删除目录 一般是rm -rf 连着用
       control+C退出选项
     ** 
     注意：rm -rf 使用时一定要谨慎 切记 ！！！
     使用时一定要谨慎 切记 ！！！
     使用时一定要谨慎 切记 ！！！
     rm -rf /* 系统直接全部被删除！！！
     **
   3. 第三讲 文件处理命令
   * touch [文件名] 在当前目录下创建空文件
     touch[绝对路径+文件名]。 指明绝对路径，在绝对路径处创建文件
     “Program files” 加双引号创建带空格的文件名 不推荐使用 以后的查询，操作都需要用到 除了代表根分区的/ 以外 其他符号都可以
   * cat [文件名] 显示文件内容 只适合短的文件内容
     cat -n [文件名] 显示行号 给文件内容的每一行标号
     cat -A [文件名] 显示隐藏字符
     tac [文件名] 逆序显示文件内容 倒着来 不支持-n   
   * more [文件名] 一页一页显示文件内容 适合长的文件内容 空格或者f 翻页 回车（Enter）一行一行翻，换行 q或者Q ，退出
   * less [文件名] 一页一页显示文件内容，只不过这条命令可以往回翻页，查看翻过的文件内容 page up向上翻页，↑箭头向上翻一行
其他操作和more命令一样 在less命令中 可以按/+需要查找文件内容的关键字查询内容，高亮内容即为含有关键字的内容，按n（表示next）可以查看下一个含有关键字的内容
   * head [文件名] 显示文件最前几行 具体几行加n head -n 行数 [文件名] 没有指定 默认10行
   * tail [文件名] 显示文件最后几行 具体几行加n tail -n 行数 [文件名] 没有指定 默认10行 tail -f 动态显示文件末尾内容 
   4. 第四讲 链接命令
  ### 首先给大家介绍一下软链接：
  软链接的作用和Windows中的快捷方式是差不多的。他只不过是指向源文件安装路径的符号链接，所以大小也很小 而且它的文件类型是lrwxrwxrwx 看似三种用户都可以拥有所有权限。其实，真正拥有的权限是源文件所决定的权限 ，所以这中显示也是软链接的一大特征之一。
  * ln -s [原文件] [目标文件] 创建软链接
  ### 硬链接：
  硬链接就是把源文件拷贝到目标位置，而他与cp -p 最大的一点区别就是他可以同步更新，源文件有变化 硬链接文件也会同时发生变化，但是如果源文件丢失或者被删除，硬链接也并不会消失。可以通过i节点来区分，源文件和硬链接文件的i节点是一样的，所以他们会同步更新，但是他不能跨分区放置硬链接比如：/分区 硬链接 不能放到/boot 分区 ，而且不能对目录使用。
  * ln [原文件] [目标文件] 创建硬链接
* 第二节 权限管理命令

   1. 第一讲 权限管理命令chmod
    ### 这一部分主要说明一下如何修改文件或者目录的权限。
    * chmod [{u,g,o,a}{+,-,=}{r,w,x}] [文件或者目录]
      u ：所有者
      g ：所属组
      o ：其他人
      a ：所有用户
      例如：chomd g+x,o+r /tmp/testfile
      就是把testfile文件的所有组增加执行权限，其他人增加读权限
      chomd a=rwx /tmp/testfile
      就是testfile文件的所有用户增加读写执行权限
    ### 权限位的数字表示：
    * chmod [rwx的和,rwx的和,rwx的和]] [文件或者目录]
      首先需要知道 r=4 w=2 x=1
      例如：rwxrw-r- - 它的权限位数字表示就是 764
      具体算法：
      r+w+x=4+2+1=7
      r+w=4+2+0=6
      r=4+0+0=4
    * chmod -R [rwx的和,rwx的和,rwx的和][文件或目录]
      这条命令与mkdir -p递归创建目录一样 这个命令把一个目录下的所有子目录的操作权限全部修改为同样的
    * 创建用户命令
      useradd [用户名] 创建普通用户
      passwd [用户名] 用户密码
      su - [用户名] 切换普通用户**
  ## 我们仍需注意在文件与目录中的不同权限，他们具体可以实施的操作是什么！这一点非常重要，有许多人到现在也不太清楚，认为对文件有写权限就可以删除文件。这一点是非常错误的。
附下表以供参考：
| 代表字符 |   权限   |                                   对文件含义 |                                        对目录的含义 |
| -------- | :------: | -------------------------------------------: | --------------------------------------------------: |
| r        |  读权限  | 可以查看文件内容 可以cat/more/head/tail/less |                         可以列出目录中的内容 可以ls |
| w        |  写权限  |                     可以修改文件内容 可以vim | 可以在目录中创建，删除文件 可以touch/mkdir/rmdir/rm |
| x        | 执行权限 |  可以执行文件 可以script(脚本) command(命令) |                                 可以进入目录 可以cd |

   2. 第二讲 其他权限管理命令
  ### 改变文件或者目录所有者
  * chown [所有者] [文件或者目录]
  ### 改变所有组
  * Groupadd [所有组组名] 添加组
  * chgrp [所有组][文件或者目录]  
**默认组为创建文件的所有者的缺省组**
  * umask -S 以rwx形式显示新建文件缺省权限
*改变文件或者目录所有者和所属组*
  * chown [所有者]:[所属组] [文件或者目录]
  
  **但是在mkdir 一个目录之后**

**进行ls -ld 发现他的权限为 drwxr-xr-x**

**但是在touch 一个文件之后**

**进行ls -l 发现他的权限为-rw-r- -r- -**

**这是因为在Linux系统里面把任何新建的文件都会把可执行权限去掉，其实umask值还没变，只不过是因为他是文件，木马病毒入侵之后没有可执行权限，就没有作用了。**
  * umask
 
  **umask 指令直接输入之后会显示 0022**

  **其中 0代表特殊权限**

  **022代表 777与022之间的一种逻辑与的关系**

  **他会进行逻辑比对，两者重复的不能保留，把没有的写下来**

777 rwx rwx rwx

022 — -w- -w-

755 rwx r-x r-x 目录

rw- r— r— 二进制文件

如果想把默认创建的文件改为700

700 rwx — --- 目录

rw- — --- 二进制文件

这样运算 进行逻辑与比对

777 rwx rwx rwx

X

700 rwx — ---

**这就像一个解方程 求X**

**X=— rwx rwx 077**
**可以使用umask 077 修改缺省创建文件权限，但是不推荐修改。**

* 第三节 文件搜索命令

  1. 第一讲 文件搜索命令find
  * find [搜索范围][匹配条件] 用于文件搜索
  * find [搜索范围] -name [关键字] 在特定路径下搜索文件名作为关键字的文件或者目录
  * find [搜索范围] -name [关键字]* 这样为带有关键字开头的任何文件都可以被搜索出来
  * find [搜索范围] -name * [关键字] * 这样为带有关键字的任何文件都可以被搜索出来
匹配任意字符 加通配符*
  * find [搜索范围] -name [关键字]??? 这样搜索的是关键字后带三个字符的 几个问号为几个字符
  * find [搜索范围] -iname [关键字] 不区分大小写搜索
注意：不能在服务区高峰时候使用查找命令。太占内存资源，搜索的范围路径越小越好，搜索条件越精准越好
  * find [搜索范围] -size [数据块] 根据文件大小查找
数据块前面加+表示查找大于这个大小的文件，-表示查找小于这个大小的文件，不加表示查找等于这个大小的文件(一般不常用)
1个数据块=512字节=0.5K
size后接的数据只能为数据块 需要换算，比如需要查找大于100MB的文件
100MB=102400KB=204800
  * find /etc -size +204800
数据块为Linux存储文件最小单位
  * find [搜索范围] -user [所有者名] 根据所有者查找
  * find [搜索范围] -group [所属组名] 根据所属组查找
  * find [搜索范围] -amin [时间] 查找时间以内被访问过的文件和目录 a：access
  * find [搜索范围] -cmin [时间] 查找时间以内被修改过属性的文件和目录 c：change
  * find [搜索范围] -mmin [时间] 查找时间以内被修改过内容的文件和目录 m：modift
+：超过多长时间 -：多长时间以内
  * find [搜索范围] -size [数据块] -a -size [数据块]
-a：两个条件同时满足
-o：两个条件满足任意一个即可
  * find /etc -size +163840 -a -size -204800
在/etc下查找大于80MB小于100MB的文件
  * find [搜索范围] -name [关键字] -a -type f
在特定路径下搜索文件名作为关键字的文件
-type 根据不同类型查找
f：文件
d：目录
l：软链接
  * find [搜索范围] -name [关键字] -exec ls -l {} \ ;
查找到文件之后并且对其进行查看ls操作。
-exec：查找到文件之后并且对其进行各种操作 {} \ ;不能丢
-ok：用于询问确认 一般在删除操作的时候使用，比如：
  * find -user yangyang -ok rm {} \ ;
删除yangyang用户的文件 他会挨个询问你是不是确定删除
  * find [搜索范围] -inum [i节点值] 根据i节点查询
  * find /etc -inum 12345 -exec rm {} \ ;
删除这个i节点文件 非常方便
也可以用来查询一个文件的硬链接
  * find /etc inum 12345 -exec ls -l {} \ ;
因为硬链接和文件肯定在同一个分区，并且i节点一样
2. 第二讲 其他文件搜索命令
  * locate [文件名]
在文件资料库中查找 速度更快
updatedb 更新文件资料库 因为locate并不是实时的
如果存放的文件在/tmp 临时文件存放处下面 locate就找不到，文件资料库不存储临时文件内容
注意：在使用的Linux系统为Linux（CentOS7）的时候，使用命令locate时发现系统显示：-bash: locate: 未找到命令，遇到错误。它的原因是：在CentOS 7 系统中默认没有安装该命令。
以下为解决办法：
链接:  [解决locate命令未找到问题.](https://blog.csdn.net/yy150122/article/details/106164472)
* locate -i 不区分大小写查找
* which 查找命令存放位置，可以看到命令可以使用的使用者是谁，也可以查看命令别名 which rm 会显示 alias rm='rm -i’
我们所使用的rm只不过是别名 不是真正的rm命令，其实是rm -i命令，所以才会询问是否真的删除，真正的rm是不会询问的，比如：
/bin/rm /tmp/yangyang 文件直接删除不会询问是否删除 相当于加了 -f
* whereis 也可以找到命令的绝对路径，还可以找到查询命令的帮助信息文档所在位置
* grep 在文件内查询字符串或者关键字列出来
* grep -i 不区分大小写查找
* grep -v 排除指定字符串
  
**比如：
  grep -v ^# /etc/inittab
查找排除#开头的注释行文件信息
^代表行首
文件中#开头的行 为配置文件信息,脚本信息**
* 第四节 帮助命令
  * man [命令名称或者配置文件名称] 获得命令或者配置文件的帮助信息
 
man后面直接写命令或者配置文件的名称就好，不能加绝对路径。进入里面之后操作和more，或者less一样。

如过使用CentOS服务器，没有man命令，需要输入下面命令来下载：

sudo yum install man-pages

配置文件帮助文档第一步看他是干什么用的，第二步看配置文件的格式。

man services

service-name | port/protocol | [aliases …]

服务名称 | 端口/传输协议 | [别名]

就可以看懂more /etc/services里的配置文件了

man passwd 他会把命令，命令的帮助，配置文件，全部找到

通过whereis passwd 可以发现

/usr/bin/passwd /etc/passwd /usr/share/man/man1/passwd.1.gz /usr/share/man/man5/
passwd.5.gz

有三个路径 他们分别为命令的路径，命令的帮助的路径，配置文件的帮助路径

其中man1代表命令的帮助，man5代表配置文件的帮助

所以我们可以通过man 5 passed就可以直接找到配置文件的帮助

  * whatis ls [命令] 查询简短的命令的作用
  * apropos [配置文件名称] 查询简短的配置文件的作用
[命令] - -help 找到命令的主要选项
  * date 查询系统当前时间
如果想修改提前用man date 查看一下时间格式

例如：

date 051910272020.18

修改完毕

man与info作用大同小异，没有本质区别，依照个人习惯使用
  * help 查询shell内置命令的帮助信息 
 在CentOS7之前的版本 直接which 命令是找不到所在路径的，因为：

 Shell是一个命令解释器 它里面有内置命令比如cd，umask

 他们使用which后找不到命令所在路径，他们就不能使用man 命令 ,他会把所有的内置命令全列出来 可以直接使用help

help用于内置命令的帮助和shell编程查看语法规则

* 第五节 用户管理命令
  * useradd 添加新用户
  * passwd [新用户名称] 给新用户填加密码
  * who 查看登陆用户信息
第一列 登陆用户名
第二列 登陆终端 tty表示本地终端 pts表示远程登陆终端
第三列 登陆时间
第四列 登陆主机的IP地址 如果没有写表示本机登陆
  * w **查看登陆用户详细信息**
 
第一行显示

17:04:55 up 22 days, 21:32, | 2 users,| load average: 0.02, 0.02, 0.05

第一个表示当前时间

第二个表示服务区系统连续运行时间没有重启或者关机，衡量服务区稳定性

第三个表示当前总共有多少个用户登陆

第四个表示负载均衡指数，分别记录了过去一分钟，五分钟，十五分钟系统的负载情况，加起来除以三就是平均负载指数，系统的负载情况主要是指 CPU和内存的负载情况，数字大表示负载严重

uptime 命令也可以显示此项数据

第二行显示
**USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT**

**其中IDLE表示用户登陆过来后空闲多久**

**PCPU表示用户登陆后执行的操作占用的CPU的时间 CPU时间**

**JCPU表示累计占用的CPU时间**

**WHAT表示执行的操作**

* 第六节 压缩解压命令
  * gzip [文件名] 压缩文件 只能压缩文件不能压缩目录，而且不保留原文件
压缩后格式为：.gz
  * gunzip [压缩包名] 解压缩.gz文件
  * gzip -d [压缩包名] 也是一样的作用，解压缩.gz文件
  * tar [选项] [压缩后文件名] [目录]
-c 打包
-v 显示详细信息
-f 指定文件名
-z 打包同时压缩
例子：
  * tar -cfv Japan.tar Japan
打包目录Japan 并且以Japan.tar命名
tar -zcfv Japan.tar.gz Japan
打包并且压缩 目录Japan 以Japan.tar.gz命名
一步到位
tar [选项] [压缩文件名] [目录]
-x 解包
-v 显示详细信息
-f 指定解压文件名
-z 解压缩
tar -xfv Japan.tar Japan
解包目录Japan.tar并且以Japan命名
tar -zxfv Japan.tar.gz
解压缩并且解包目录Japan.tar.gz以Japan命名
  * zip [选项] [压缩后文件或目录名] [文件或目录]
原文件会保留 而且提示压缩比 deflated
没有gzip压缩比大，不常用
压缩后格式为：.zip
zip -r 压缩目录
  * unzip [压缩文件] 解压zip文件
  * bzip2 [选项] [文件名] 压缩文件，大型文件一般用这个压缩
例子：
bzip2 -k Japan
-k：保留原文件 如果不需保留可去掉
生成Japan.bz2压缩文件
他还可以与tar结合使用
tar -cjfv Japan.tar.bz2 Japan
  * bunzip2 [选项] [压缩文件名] 解压文件
-k：保留压缩包
与tar结合使用
tar -xjfv Japan.tar.bz2 Japan

* 第七节 网络命令
  * write <用户名> 给在线用户发信息，按Ctrl+D保存结束 只能给在线用户发 可以用w查询用户在线情况 不在线发不出去
  * wall [信息] 发广播信息 群发所有在线用户
  * ping [IP地址] 测试网络连通性
ping -c 指定发送次数
  * ifconfig 查看网卡信息 主要功能是查询当前本机IP地址
  * mail <用户名>
给不在线的用户发送邮件

例子：mail yangyang

进入之后：

Subject：输入标题

下面输入正文，按Ctrl+D保存结束并发送

按mail查询收到的邮件

N 表示未读邮件

想看第几封邮件就按前面的标号数字

h键查看邮箱列表

d [n] 删除第n封邮件

q 退出

在CentOS7服务器中，比如阿里云ESC服务器中运行的CentOS7中，就会出现mail命令无法使用：Linux CentOS7 命令错误：send-mail: fatal: parameter inet_interfaces: no local interface found for ::1

解决办法写在了我的另一片博文上：

链接: [mail命令错误解决办法.](https://blog.csdn.net/yy150122/article/details/106179803)
以供大家解决问题。
  * last 列出目前与过去登陆系统的用户信息
  * lastlog 检查某特定用户上次登陆的时间
  * lastlog -u [uID] 检查uID用户上次登陆的时间
  * traceroute 显示数据包到主机间的路径
这里CentOS7用户也会出现traceroute命令不能使用的问题，直接下载traceroute就好了
yum install -y traceroute 安装
  * traceroute [网站网址] 可以检查网络哪个节点出现问题
  * netstat [选项] 显示网络相关信息
-t TCP协议：传输控制协议
-u UDP协议：用户数据报
-l 监听
-r 路由：网关
-n 显示IP地址和端口号
netstat -tlun ：查询本机监听的端口
netstat -an ：查看本机所有的网络连接
netstat -rn ：查看本机路由（网关）
  * setup 配置网络 redhat专有命令 ,在其他版本不存在，他是永久生效的 和刚开始介绍的ifconfig命令不一样
CentOS7使用 nmtui命令代替setup，不过是在虚拟机中调试
* 第七节 挂载命令 
  * mount [-t 文件系统] 设备文件名 挂载点
   
  * mount 设备文件名/挂载点 卸载光盘，设备文件名和挂载点两者任选其一
   
第一步：放入光盘，虚拟机中放入，或者服务器下载ios文件

第二步：创建一个空目录，设为挂载点

mkdir /media/cdrom /media用来做光盘挂载的，/mnt 也可以

第三部：输入命令

mount -t iso9660 /dev/sr0 /media/cdrom

设备文件名默认就是/dev/sr0，文件系统为iso9660 它是国际标准的cd文件格式，它告诉mount命令，我要挂载的是一个标准的cd。需要死记！！！

/dev/cdrom也可以写 /dev/sr0

/dev/cdrom是sr0的软链接。

第四步：进入挂载后的盘符

cd /media/cdrom

第四步：卸载光盘

先退出/media/cdrom，输入命令：cd；然后再输入命令：umount /dev/sr0

注意：如果之前挂载过其他盘，需要卸载之后才能挂载，输入命令：

umount /dev/sr0

* 第八节 关机重启命令
  * shutdown [选项] 时间
  
时间选项里可以填具体时间比如：

now 现在关机

20:30 八点半关机

-c：取消前一个关机命令

-h：关机

-r：重启

例子：

shutdown -h now 关机

shutdown -c 取消上一次设定的关机时间

在服务器上重启需要谨慎，需要先停掉服务，否则物理内存会坏

而且远程服务器只能重启，关机后需要管理员手动开机

  * 其他关机命令：
   
    halt

    poweroff 相当于直接断电

    init 0

    推荐使用shutdown关机，会保存正在运行的服务

    其他重启命令：

    reboot

    init 6

    系统的运行级别：

    init 0-6

    0：关机

    1：单用户 进入选项菜单 只有root用户登陆进去 相当于Windows安全模式F8，只不过没有图形界面

    2：不完全多用户，不含NFS服务，没有图形界面 NFS网络文件系统，Linux之间文件传输共享方式，除了NFS服务，和3一样。

    3：完全多用户，没有图形界面

    4：未分配，没有图形界面

    5：图形界面

    6：重启

  * runlevel 查询系统运行级别
  *   logout 退出登陆命令
    
    **注意：在服务器中一定要在操作完成之后退出登陆，否则其他人会直接进入你的服务器，造成非常大的损失。最基本的安全意识一定要有！！！**
## 第五章 文本编译器Vim

* 第一节 Vim常用操作
 
**Vim没有菜单，只有命令**
**Vim的工作模式有三种：**

  * 第一种：命令模式 vi/vim+文件名 进入命令模式 不可以输入文字，只能识别命令
  * 
  **插入命令：**

  a：在光标所在字符后插入

  A：在光标所在行尾插入

  i：在光标所在字符前插入

  I：在光标所在行行首插入

  o：在光标下插入新行

  O：在光标上插入新行

  * 第二种：插入模式 按i/a/o进入，可以继续输入文字，按Esc退出
  * 第三种：编辑模式 在命令模式下按:，即可进入 编辑模式 可以输入编辑命令 比如：保存并退出，加行号

定位命令：

   * :set nu 设置行号
   * :set nonu 取消行号
   * gg 到第一行
   * G 到最后一行
   * nG 到第n行
   * : n 到第n行 和上面一样的格式
   * $ 移动到行尾
   * 0 移动到行首
 * 删除命令：
   * x 删除光标所在处的字符
   * nx 删除光标所在处后n个字符
   * nd 删除光标所在行
   * ndd 删除n行
   * dG 删除光标所在行到文件末尾的内容
   * D 删除光标所在处到行尾内容
   * :n1,n2d 删除指定范围的行 n1-n2的行全部被删除
   * 复制和剪切命令：
   * yy 复制当前行
   * nyy 复制当前行一下n行
   * dd 剪切当前行
   * ndd 剪切当前行以下n行
   * p 粘贴在当前光标所在行下
   * P 粘贴在当前光标所在行上
 * 替换或取消命令：
   * r 替换光标所在处字符
   * R 从光标所在处开始替换字符，按Esc结束
   * u 取消上一不操作
 * 搜索和搜索替换命令：
   * /string 搜索指定字符串string 与less命令操作类似
   * 
   搜索时忽略大小写:set ic

   搜索时不忽略大小写:set noic

   * n 搜索指定字符串的下一个出现位置
   * :%s/要替换的字符串/替换的新的字符串/g 不询问
   * 
    把/g换成/c 进行询问确认

    全文替换指定字符串

   * :n1,n2s/要替换的字符串/替换的新的字符串/g
    
  ### 在一定范围内替换指定字符串
 * 保存和退出命令：
   :w 保存修改

   :w new_filename 另存为指定文件

   :wq 保存修改并退出

   ZZ 快捷键，保存修改退出

   :q! 不保存修改退出

   :wq! 保存修改并退出（只有文件所有者以及root可以使用）适合保存root只有只读权限的文件

* 第二节 Vim使用技巧
**在Vim中有许多黑科技小技巧便于我们操作，我总结了以下几天最为方便的操作，以供大家学习：**

   * :r !命令 当前的Vim文档导入命令执行结果
例子：
:r !date 直接把当前时间导入当前的Vim文档
   * map [快捷键] [触发命令] 定义快捷键
    其中快捷键需要按ctrl+v+需要设定的键位，设定好之后颜色会变，比如想设定ctrl p为快捷键那么就按ctrl+v+p 会出现^P ，不能按shift+6出现的^,这两个虽然看起来一样但是颜色不一样
    触发命令按需要执行的命令的先后顺序来排列，比如给脚本加注释#键就可以把[触发命令]设为I#
    例子：
map ^P I# 给脚本行首加#注释
   * :n1,n2s/^/#/g 替换行首字符为#，连续行的注释，不过需先设置行号 :set nu
   * :n1,n2s/^#/ /g 取消注释
   * :n1,n2s/^/ \ / \ //g 给行首加// 需先设置行号 :set nu
因为系统无法识别太多的，所以需要在//每一条/前都加转义符\，\表达命令的正在含义，比如ls /etc 里面的文件会有颜色，但是\ls 就没有，他是表达执行ls真正含义不执行ls别名
   * ab [a内容][b内容]
   例子：
    ab mymail 1771566679@qq.com
    替换命令，当你在vim文档中输入mymail时按回车或者空格会自动变1771566679@qq.com
    即：会自动把b内容替换成a
    非常实用的小技巧
    **有些时候在重启服务器之后，定义的快捷键会消失，这时候我们需要在用户的家目录下写配置文件，保存快捷键**
    **root用户在 /root/.vimrc**
    **其他用户在 /home/username/.vimrc在里面进行编辑，永久生效**
## 第六章 软件包管理
* 第一节 软件包管理简介
* 源码包：可以看到源代码，但是安装时间较慢，脚本安装包 类似Windows安装软件， 他是写了安装界面的源码包

  优点：
    * 1.开源，如果有足够的能力，可以修改源代码
    * 2.可以自由选择所需的功能
    * 3.软件是编译安装，所以更适合自己的系统，使用更加稳定也效率更高
    * 4.卸载方便，直接删除安装目录
  缺点：
    * 1.安装过程步骤较多，尤其安装较大的软件集合时（如LAMP环境搭建），容易出现拼写错误
    * 2.编译过程时间较长，安装比二进制安装时间长
    * 3.因为是编译安装，安装过程中一旦报错新手很难解决
     
### 二进制包：RPM包，系统默认包，厂商已经进行了编译，看不到源代码，但是安装时间较快

  优点：

  * 1.包管理系统简单，只通过几个命令就可以实现包的安装，升级，查询和卸载
  * 2.安装速度比源码包安装快得多
   
  缺点：
  * 1.经过编译，不再可以看到源代码
  * 2.功能选择不如源码包灵活
  * 3.依赖性 依赖性指的是要想安装A包就得先安装B包，要想安装B包又得先安装C包，所以只能以CBA的顺序安装RPM包，删除的时候得按ABC顺序删除安装包，基本上所有的RPM包全有依赖性

* 第二节 rpm命令管理

   1. 第一讲 包命名与依赖性
   ### RPM包命名规则
    例子：
    Httpd-2.2.15.el6.centos.1.i686.rpm
    其中：

    * Httpd 软件包包名
    * 2.2.15 软件版本
    * 15 软件发布的次数
    * el6.centos 适合的Linux平台
    * i686 适合的硬件平台 noarch 表示任何硬件平台都可以安装
    * rpm rpm包扩展名
    如果自己组建rpm包，都以rpm结尾，这样更加清晰，其他管理员可以明白
    **注意：Httpd-2.2.15.el6.centos.1.i686.rpm为包全名，Httpd 为包名是有区别的，Linux系统命令严格区分两者** 
    **RPM包依赖性** 

    * 树形依赖：a→b→c
    * 环形依赖：a→b→c→a
    * 环形依赖需要把a,b,c三个同时安装
    * 模块依赖：模块依赖查询网站：www.rpmfind.net
     
      ==如果安装时遇到问题，出现依赖性错误

      被依赖文件以.so.[数字]结尾的为库依赖，需要直接安装这个软件，错误会自动解决

      安装这个包时需要进入网站 [www.rpmfind.net.](https://www.rpmfind.net/)
      
      查询被依赖文件

   2. 第二讲 安装升级与卸载
    **包全名：操作的包是没有安装的软件包时，使用包全名。而且要注意路径**
    **包名：操作以及安装的软件包时，使用包名。是默认在搜索/var/lib/rpm中的数据库**

      * rpm -ivh 包全名 RPM安装
       
        -i 安装（install）

        -v 显示详细安装信息（verbose）

        -h 显示进度（hash）

        –nodeps 不检测依赖性 一般不用，安装时都得显示依赖性

        **注意：安装一定要用包全名**
      * rpm -Uvh 包全名 RPM包升级
       
        -U 升级（upgrade）

        rpm -e 包名

        -e 卸载（erase）

        –nodeps 不检查依赖性

   4. 第三讲 查询
   * rpm -q 包名 查询是否安装 
    
      -q 查询（query）

      rpm -qa 查询所有安装的包

      -a 所有（all）

   * rpm -qa | grep [关键字]
     查询所有含义关键字的包，| 为管道符 。作用是管道符左边命令的输出就会作为管道符右边命令的输入

      **注意：**
      **1、管道命令只处理前一个命令正确输出，不处理错误输出。**
      **2、管道命令右边命令，必须能够接收标准输入流命令才行。**
    *  rpm -qi 包名 查询安装过软件包详细信息
   
      -i 查询软件信息（information）

      -p 查询未安装包信息（package）

    *  rpm -qip 包全名 查询没安装过软件包详细信息 因为包没有安装所以得加包全名，因为包在生产好的时候他的信息就已经生成，所以可以查到没安装好的包的信息
    *  rpm -ql 包名 查询包中文件安装位置  
   
      -l 列表（list）

      -p 查询未安装包信息（package）

    *  rpm -qf 系统文件名 查询系统文件属于哪个RPM包
      
      -f 查询系统文件属于哪个软件包（file）

    *  rpm -qR 包名 查询软件包的依赖性
      
      -R 查询软件包的依赖性（requires）

      -p 查询未安装包信息（package）

  第四讲 检验和文件提取
   * rpm -V 已安装的包名 RPM包校验
   
  -V 校验指定RPM包中的文件（verify）

  例子：rpm -V httpd 显示：

  S.5……T. c /etc/httpd/conf/heepd.conf

  * 验证内容中的8个信息的具体内容：
 
      S：文件大小是否改变

      M：文件的类型或文件的权限(rwx)是否被改变

      5：文件MD5校验和是否改变(可以看成文件内容是否改变) MD5是进行文件完整性验证的

      D：设备的中，从代码是否改变

      L：文件路径是否改变

      U：文件的属主(所有者)是否改变

      G：文件的属组是否改变

      T：文件的修改时间是否改变

  * 文件类型：
      c：配置文件（config file）

      d：普通文档（documentation）

      g：“鬼”文件（ghost file），很少见，就是该文件不应该被这个RPM包包含

      l：授权文件（license file）

      r：描述文件（read me）

   *  rpm2cpio 包全名 | cpio -idv.文件绝对路径
      **rpm2cpio 将rpm包转换为cpio格式的命令**
      **cpio 是一个标准工具，他用于创建软件档案文件和从档案文件中提取文件**

* 第二节 RPM包管理

  第一讲 yum在线管理

   1. 第一部分ip地址配置和网络yum源
    
  **IP地址配置**

  **红帽使用setup 命令配置IP，子网掩码，网关，DNS**

  **然后service network restart 重启网络服务**

  **CentOS7使用nmtui命令配置IP，子网掩码，网关，DNS**

  **然后service network restart 重启网络服务**

  **云服务器进阿里云/腾讯云远程登陆端口配置**

  **如果还没有联网 输入命令：**

  **vi/etc/sysconfig/network-scripts/ifcfg-eth0**

  **进入Vim编辑器后把ONBOOT=“no”改为ONBOOT=“yes” ，接着需要使用命令service network restart，重新启动网卡**

  **网络yum源**

  **vi /etc/yum.repos.d/CentOS-Base.repo**

  **其中：**

   * CentOS-Base.repo为网络yum源
   * CentOS-Media.repo为本地磁盘yum源
    
  **进入yum内部配置文件中可以看到以下内容：**

   * [base]：容器名称，一定要放在[]中
   * name：容器说明，可以自己随便写
   * mirrorlist：镜像站点，这个可以注释掉
   * baseurl：我们的yum源服务器的地址。默认是CentOS的官方的yum源服务器，是可以使用的，如果觉得慢可以改成你喜欢的yum镜像源地址
   * enabled：此容器是否生效
   * 如果不写或者写成enable=1都是生效的，写成enable=0就是不生效
   * gpgcheck：如果1是指RPM的数字证书生效，如果是0则不生效
   * gpgkey：数字证书的公钥文件保存位置。不用修改

   1. 第二部分 yum命令
     * yum list 查询所有可用软件包列表 
      
     * yum search [关键字(包名)] 搜索服务器上所有和关键字相关的包
     * yum -y install [包名] 安装软件包
     
        install 安装

        -y 自动回答yes

     *  yum -y update [包名] 升级软件包
       
        update 升级
        -y 自动回答yes
        注意：yum -y update 后必须加包名，否则就是全盘更新，包括Linux内核也会更新，Linux内核在更新完成之后需要在本地进行配置，内核才可以启动，如果你是在服务器上跑这条命令，服务器直接崩溃，永远无法连接，再也不能启动！！！
     *  yum -y remove 包名 卸载包
    
        remove 卸载

        -y 自动回答yes

        注意：yum -y remove卸载会把包所有的依赖包都会卸载，有时候会把系统文件也同时卸载，小心使用，尽量不要多用！！！
        
        Linux 服务器安装软件包原则：
        最小化安装，不安装多余软件，使用什么软件安装什么软件，手工装，尽量不卸载，尤其yum卸载尽量不要用！！！

    **yum软件组管理命令**

    * yum grouplist 列出所有可用的软件组列表
    * yum groupinstall “软件组名” 安装指定软件组，组名可以由grouplist查询出来，如果组名之间有空格，用双引号扩起来
    * yum groupmove 软件组名 卸载指定软件组

   1. 第三部分 光盘yum源搭建
* 第三节 源码包管理

   1. 第一讲 源码包和RMP包的区别
   2. 源码包包装过程
* 第四节脚本包管理

    脚本包安装
## 第七章 用户和用户组管理
 * 第一节 用户配置文件
   1. 第一讲 用户信息文件/etc/passwd
   2. 第二讲 影子文件/etc/shadow
   3. 第三讲 组文件信息/etc/group
   4. 第四组 组密码文件/etc/gshadow
 * 第二节 用户管理相关文件
 * 第三节 用户管理命令
   1. 第一讲 用户添加命令 useradd
   2. 第二讲 修改用户密码 passwd
   3. 第三讲 修改用户信息 usermod
   4. 第四讲 修改用户密码状态 chage
   5. 第五讲 删除用户 userdel 
   6. 用户切换命令 su
  * 第四节 用户组管理命令
## 第八章 权限管理
* 第一节 ACL权限
   1. 第一讲 ACL权限简介与开启
   2. 第二讲 ACL 权限查看与设定
   3. 第三讲 ACL 权限最大有效权限与删除
   4. 第四讲 ACL 权限默认与递归
* 第二节 文件特殊权限
   1. 第一讲 SetUID 
   2. 第二讲 SetGID
   3. 第三讲 Sticky BIT 
* 第三节 文件属性chattr权限
* 第四节 系统命令 sudo权限
## 第九章 文件系统管理
 * 第一节 回顾分区和文件系统
 * 第二节 文件系统常用命令
   1. 第一讲 df命令 du命令 fsck命令和dump2fs命令
   2. 第二讲 挂载命令
   3. 第三讲 挂载光盘与U盘
   4. 第四讲 支持NTFS文件系统
* 第三节 fdisk分区
   1. 第一讲 fdisk 命令分区过程
   2. 第二讲 分区自动挂载与fstab文件修复
* 第四节 新建swap分区
## 第十章 Shell基础
* 第一节 Shell概述
* 第二节 Shell脚本执行方式
* 第三节 Bash的基本功能
  1. 第一讲 历史命令与命令补全
  2. 第二讲 命令别名与常用快捷键
  3. 第三讲 输入输出重定向
  4. 第四讲 多命令顺序执行与管道符 多命令顺序执行
  5. 第五讲 通配符与其他特殊符号
* 第四节 Bash的变量 
  1. 第一讲 用户自定义变量
  2. 第二讲 环境变量
  3. 第三讲 位置参数变量
  4. 第四讲 预定义变量
* 第五节 Bash的运算符
  1. 第一讲 数值运算与运算符
  2. 第二讲 变量测试与内容替换
* 第六节 Bash的运算符
  1. 第一讲 环境变量配置文件简介
  2. 第二讲 环境配置文件作用
  3. 第三讲 其他配置文件和登录信息
## 第十一章 Shell编程
* 第一节 基础正则表达式
* 第二节 字符截取命令
  1. 第一讲 cut字段提取命令
  2. 第二讲 printf命令
  3. 第三讲 awk命令
  4. 第四讲 sed 命令
* 第三节 字符处理命令 
* 第四节 条件判断
* 第五节 流程控制
  1. 第一讲 if语句
  2. 第二讲 case语句
  3. 第三讲 for循环
  4. 第四讲 while循环与until循环
## 第十二章 Linux服务管理
 * 第一节 服务简介与分类
 * 第二节 RPM包安装服务的管理
  1. 第一讲 独立服务的管理
  2. 第二讲 基于xinetd服务的管理
* 第三节 源码包安装服务的管理
* 第四节 服务管理总结
## 第十三章 Linux系统管理
* 第一节 进程管理
  1. 第一讲 进程查看
  2. 第二讲 进程管理
* 第二节 进程管理
* 第三节 系统资源查看
* 第四节 系统定时任务
## 第十四章 日志管理
 * 第一节 日志管理简介
 * 第二节 rsyslogd日志服务
 * 第三节 日志轮替
## 第十五章 启动管理
 * 第一节 CentOS 6.x启动管理
   1. 第一讲 系统运行级别
   2. 第二讲 系统启动过程
 * 第二节 启动引导程序grub
   1. Grub配置文件
   2. Grub加密与字符界面分辨率调整
* 第三节 系统修复模式
## 第十六章 备份与恢复
* 第一节 备份概述
* 第二节 dump和restore命令


