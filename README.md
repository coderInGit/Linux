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

   2. 第二讲 目录处理命令

   3. 第三讲 文件处理命令

   4. 第四讲 链接命令

* 第二节 权限管理命令

   1. 第一讲 权限管理命令chmod

   2. 第二讲 其他权限管理命令
  
* 第三节 文件搜索命令

  1. 第一讲 文件搜索命令find

  2. 第二讲 其他文件搜索命令

* 第四节 帮助命令

* 第五节 用户管理命令

* 第六节 压缩解压命令

* 第七节 网络命令

* 第七节 挂载命令

* 第八节 关机重启命令

## 第五章 文本编译器Vim

* 第一节 Vim常用操作

* 第二节 Vim使用技巧

## 第六章 软件包管理
* 第一节 软件包管理简介
* 第二节 rpm命令管理

   1. 第一讲 包命名与依赖性
   2. 第二讲 安装升级与卸载
   3. 第三讲 查询
  第四讲 检验和文件提取
* 第二节 RPM包管理

  yum在线管理
   1. 第一部分ip地址配置和网络yum源
   2. 第二部分 yum命令
   3. 第三部分 光盘yum源搭建
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


