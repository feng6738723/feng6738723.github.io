# Linux

Linux是一个通用操作系统。一个操作系统要负责任务调度、内存分配、处理外围设备I/O等操作。操作系统通常由内核（运行其他程序，管理像磁盘、打印机等硬件设备的核心程序）和系统程序（设备驱动、底层库、shell、服务程序等）两部分组成。 

### 1. 基础命令

Linux系统的命令通常都是如下所示的格式：

```
命令名称 [命名参数] [命令对象]
```

1. 获取登录信息 - **w** / **who** / **last**。

```
[root@izwz97tbgo9lkabnat2lo8z ~]# w
 23:31:16 up 12:16,  2 users,  load average: 0.00, 0.01, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
root     pts/0    182.139.66.250   23:03    4.00s  0.02s  0.00s w
jackfrue pts/1    182.139.66.250   23:26    3:56   0.00s  0.00s -bash
[root@izwz97tbgo9lkabnat2lo8z ~]# who
root     pts/0        2018-04-12 23:03 (182.139.66.250)
jackfrued pts/1        2018-04-12 23:26 (182.139.66.250)
[root@izwz97tbgo9lkabnat2lo8z ~]# who am i
root     pts/0        2018-04-12 23:03 (182.139.66.250)
```

2. 查看自己使用的Shell - **ps**。

   Shell也被称为“壳”，它是用户与内核交流的翻译官，简单的说就是人与计算机交互的接口。目前很多Linux系统默认的Shell都是bash（Bourne Again SHell），因为它可以使用Tab键进行命令补全、可以保存历史命令、可以方便的配置环境变量以及执行批处理操作等。

   ```
   [root@izwz97tbgo9lkabnat2lo8z ~]# ps
     PID TTY          TIME CMD
    3531 pts/0    00:00:00 bash
    3553 pts/0    00:00:00 ps
   ```

3. 查看帮助文档 - **man** / **info** / **apropos**。

   ```
   [root@izwz97tbgo9lkabnat2lo8z ~]# ps --help
   Usage:
    ps [options]
    Try 'ps --help <simple|list|output|threads|misc|all>'
     or 'ps --help <s|l|o|t|m|a>'
    for additional help text.
   For more details see ps(1).
   [root@izwz97tbgo9lkabnat2lo8z ~]# man ps
   PS(1)                                User Commands                                PS(1)
   NAME
          ps - report a snapshot of the current processes.
   SYNOPSIS
          ps [options]
   DESCRIPTION
   ...
   [root@izwz97tbgo9lkabnat2lo8z ~]# info ps
   ...
   ```

4. 切换用户 - **su**。

   ```
   [root@izwz97tbgo9lkabnat2lo8z ~]# su hellokitty
   [hellokitty@izwz97tbgo9lkabnat2lo8z root]$
   ```

5. 以管理员身份执行命令 - **sudo**。

   ```
   [jackfrued@izwz97tbgo9lkabnat2lo8z ~]$ ls /root
   ls: cannot open directory /root: Permission denied
   [jackfrued@izwz97tbgo9lkabnat2lo8z ~]$ sudo ls /root
   [sudo] password for jackfrued:
   calendar.py  code  error.txt  hehe  hello.c  index.html  myconf  result.txt
   ```

6. 登入登出相关 - **logout** / **exit** / **adduser** / **userdel** / **passwd** / **ssh**。

   ```
   [root@izwz97tbgo9lkabnat2lo8z ~]# adduser hellokitty
   [root@izwz97tbgo9lkabnat2lo8z ~]# passwd hellokitty
   Changing password for user jackfrued.
   New password:
   Retype new password:
   passwd: all authentication tokens updated successfully.
   [root@izwz97tbgo9lkabnat2lo8z ~]# ssh hellokitty@1.2.3.4
   hellokitty@1.2.3.4's password:
   Last login: Thu Apr 12 23:05:32 2018 from 10.12.14.16
   [hellokitty@izwz97tbgo9lkabnat2lo8z ~]$ logout
   Connection to 1.2.3.4 closed.
   [root@izwz97tbgo9lkabnat2lo8z ~]#
   ```

7. 查看系统和主机名 - **uname** / **hostname**。

   ```
   [root@izwz97tbgo9lkabnat2lo8z ~]# uname
   Linux
   [root@izwz97tbgo9lkabnat2lo8z ~]# hostname
   izwz97tbgo9lkabnat2lo8z
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat /etc/centos-release
   CentOS Linux release 7.4.1708 (Core) 
   ```

8. 重启和关机 - **reboot** / **init 6** / **shutdown** / **init 0**。 

9. 查看历史命令 - **history**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# history
   ...
   452  ls
   453  cd Python-3.6.5/
   454  clear
   455  history
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# !454
   ```

说明：查看到历史命令之后，可以用`!历史命令编号`来重新执行该命令；通过`history -c`可以清除历史命令。 



### 2. 实用程序

#### 1.文件和文件夹操作

1. 创建/删除目录 - **mkdir** / **rmdir**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# mkdir abc
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# mkdir -p xyz/abc
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# rmdir abc
   ```

2. 创建/删除文件 - **touch** / **rm**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# touch readme.txt
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# touch error.txt
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# rm error.txt
   rm: remove regular empty file ‘error.txt’? y
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# rm -rf xyz
   ```

   * touch命令用于创建空白文件或修改文件时间。在Linux系统中一个文件有三种时间：
     * 更改内容的时间 - mtime。
     * 更改权限的时间 - ctime。
     * 最后访问时间 - atime。
   * rm的几个重要参数：
     - -i：交互式删除，每个删除项都会进行询问。
     - -r：删除目录并递归的删除目录中的文件和目录。
     - -f：强制删除，忽略不存在的文件，没有任何提示。

3. 切换和查看当前工作目录 - **cd** / **pwd**。

   > 说明：
   >
   > `cd`命令后面可以跟相对路径（以当前路径作为参照）或绝对路径（以`/`开头）来切换到指定的目录，
   >
   > 也可以用`cd ..`来返回上一级目录。

4. 查看目录内容 - **ls**。

   - -l：以长格式查看文件和目录。
   - -a：显示以点开头的文件和目录（隐藏文件）。
   - -R：遇到目录要进行递归展开（继续列出目录下面的文件和目录）。
   - -d：只列出目录，不列出其他内容。
   - -S/-t：按大小/时间排序。

5. 查看文件内容 - **cat** / **head** / **tail** / **more** / **less**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# wget http://www.sohu.com/ -O sohu.html
   --2018-06-20 18:42:34--  http://www.sohu.com/
   Resolving www.sohu.com (www.sohu.com)... 14.18.240.6
   Connecting to www.sohu.com (www.sohu.com)|14.18.240.6|:80... connected.
   HTTP request sent, awaiting response... 200 OK
   Length: 212527 (208K) [text/html]
   Saving to: ‘sohu.html’
   100%[==================================================>] 212,527     --.-K/s   in 0.03s
   2018-06-20 18:42:34 (7.48 MB/s) - ‘sohu.html’ saved [212527/212527]
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat sohu.html
   ...
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# head -10 sohu.html
   <!DOCTYPE html>
   <html>
   <head>
   <title>搜狐</title>
   <meta name="shenma-site-verification" content="1237e4d02a3d8d73e96cbd97b699e9c3_1504254750">
   <meta charset="utf-8"/>
   <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1"/>
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# tail -2 sohu.html
   </body>
   </html>
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# less sohu.html
   ...
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat -n sohu.html | more
   ...
   ```

6. 拷贝/移动文件 - **cp** / **mv**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# mkdir backup
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cp sohu.html backup/
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cd backup
   [root@iZwz97tbgo9lkabnat2lo8Z backup]# ls
   sohu.html
   [root@iZwz97tbgo9lkabnat2lo8Z backup]# mv sohu.html sohu_index.html
   [root@iZwz97tbgo9lkabnat2lo8Z backup]# ls
   sohu_index.html
   ```

7. 查找文件和查找内容 - **find** / **grep**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# find / -name "*.html"
   /root/sohu.html
   /root/backup/sohu_index.html
   [root@izwz97tbgo9lkabnat2lo8z ~]# find . -atime 7 -type f -print
   [root@izwz97tbgo9lkabnat2lo8z ~]# find . -type f -size +2k
   [root@izwz97tbgo9lkabnat2lo8z ~]# find . -type f -name "*.swp" -delete
   ```

8. 链接 - **ln**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l sohu.html
   -rw-r--r-- 1 root root 212131 Jun 20 19:15 sohu.html
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ln /root/sohu.html /root/backup/sohu_backup
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l sohu.html
   -rw-r--r-- 2 root root 212131 Jun 20 19:15 sohu.html
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ln /root/sohu.html /root/backup/sohu_backup2
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l sohu.html
   -rw-r--r-- 3 root root 212131 Jun 20 19:15 sohu.html
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ln -s /etc/centos-release sysinfo
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l sysinfo
   lrwxrwxrwx 1 root root 19 Jun 20 19:21 sysinfo -> /etc/centos-release
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat sysinfo
   CentOS Linux release 7.4.1708 (Core)
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat /etc/centos-release
   CentOS Linux release 7.4.1708 (Core)
   ```

   > 说明：链接可以分为硬链接和软链接（符号链接）。硬链接可以认为是一个指向文件数据的指针，就像Python中对象的引用计数，每添加一个硬链接，文件的对应链接数就增加1，只有当文件的链接数为0时，文件所对应的存储空间才有可能被其他文件覆盖。我们平常删除文件时其实并没有删除硬盘上的数据，我们删除的只是一个指针，或者说是数据的一条使用记录，所以类似于“文件粉碎机”之类的软件在“粉碎”文件时除了删除文件指针，还会在文件对应的存储区域填入数据来保证文件无法再恢复。软链接类似于Windows系统下的快捷方式，当软链接链接的文件被删除时，软链接也就失效了。

9. 压缩/解压缩和归档/解归档 - **gzip** / **gunzip** / **xz** / **tar**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# wget http://download.redis.io/releases/redis-4.0.10.tar.gz
   --2018-06-20 19:29:59--  http://download.redis.io/releases/redis-4.0.10.tar.gz
   Resolving download.redis.io (download.redis.io)... 109.74.203.151
   Connecting to download.redis.io (download.redis.io)|109.74.203.151|:80... connected.
   HTTP request sent, awaiting response... 200 OK
   Length: 1738465 (1.7M) [application/x-gzip]
   Saving to: ‘redis-4.0.10.tar.gz’
   100%[==================================================>] 1,738,465   70.1KB/s   in 74s
   2018-06-20 19:31:14 (22.9 KB/s) - ‘redis-4.0.10.tar.gz’ saved [1738465/1738465]
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls redis*
   redis-4.0.10.tar.gz
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# gunzip redis-4.0.10.tar.gz
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls redis*
   redis-4.0.10.tar
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# tar -xvf redis-4.0.10.tar
   redis-4.0.10/
   redis-4.0.10/.gitignore
   redis-4.0.10/00-RELEASENOTES
   redis-4.0.10/BUGS
   redis-4.0.10/CONTRIBUTING
   redis-4.0.10/COPYING
   redis-4.0.10/INSTALL
   redis-4.0.10/MANIFESTO
   redis-4.0.10/Makefile
   redis-4.0.10/README.md
   redis-4.0.10/deps/
   redis-4.0.10/deps/Makefile
   redis-4.0.10/deps/README.md
   ...
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls redis*
   redis-4.0.10.tar
   redis-4.0.10:
   00-RELEASENOTES  COPYING  Makefile   redis.conf       runtest-sentinel  tests
   BUGS             deps     MANIFESTO  runtest          sentinel.conf     utils
   CONTRIBUTING     INSTALL  README.md  runtest-cluster  src
   ```

10. 其他工具 - **sort** / **uniq** / **diff** / **tr** / **cut** / **paste** / **file** / **wc**。

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# cat foo.txt
grape
apple
pitaya
[root@iZwz97tbgo9lkabnat2lo8Z ~]# cat bar.txt
100
200
300
400
[root@iZwz97tbgo9lkabnat2lo8Z ~]# paste foo.txt bar.txt
grape   100
apple   200
pitaya  300
        400
[root@iZwz97tbgo9lkabnat2lo8Z ~]# paste foo.txt bar.txt > hello.txt
[root@iZwz97tbgo9lkabnat2lo8Z ~]# cut -b 4-8 hello.txt
pe      10
le      20
aya     3
0
[root@iZwz97tbgo9lkabnat2lo8Z ~]# cat hello.txt | tr '\t' ','
grape,100
apple,200
pitaya,300
,400
[root@iZwz97tbgo9lkabnat2lo8Z ~]# wget https://www.baidu.com/img/bd_logo1.png
--2018-06-20 18:46:53--  https://www.baidu.com/img/bd_logo1.png
Resolving www.baidu.com (www.baidu.com)... 220.181.111.188, 220.181.112.244
Connecting to www.baidu.com (www.baidu.com)|220.181.111.188|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 7877 (7.7K) [image/png]
Saving to: ‘bd_logo1.png’
100%[==================================================>] 7,877       --.-K/s   in 0s
2018-06-20 18:46:53 (118 MB/s) - ‘bd_logo1.png’ saved [7877/7877][root@iZwz97tbgo9lkabnat2lo8Z ~]# file bd_logo1.png
bd_logo1.png: PNG image data, 540 x 258, 8-bit colormap, non-interlaced
[root@iZwz97tbgo9lkabnat2lo8Z ~]# wc sohu.html
  2979   6355 212527 sohu.html
[root@iZwz97tbgo9lkabnat2lo8Z ~]# wc -l sohu.html
2979 sohu.html
```

#### 管道和重定向

1. 管道的使用 - **|**。

   例子：查找当前目录下文件个数。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# find ./ | wc -l
   6152
   ```

   例子：列出当前路径下的文件和文件夹，给每一项加一个编号。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls | cat -n
        1  dump.rdb
        2  mongodb-3.6.5
        3  Python-3.6.5
        4  redis-3.2.11
        5  redis.conf
   ```

   例子：查找record.log中包含AAA，但不包含BBB的记录的总数

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat record.log | grep AAA | grep -v BBB | wc -l
   ```

2. 输出重定向和错误重定向 - **>** / **>>** / **2>**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat readme.txt
   banana
   apple
   grape
   apple
   grape
   watermelon
   pear
   pitaya
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat readme.txt | sort | uniq > result.txt
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cat result.txt
   apple
   banana
   grape
   pear
   pitaya
   watermelon
   ```

3. 输入重定向 - **<**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# echo 'hello, world!' > hello.txt
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# wall < hello.txt
   [root@iZwz97tbgo9lkabnat2lo8Z ~]#
   Broadcast message from root@iZwz97tbgo9lkabnat2lo8Z (Wed Jun 20 19:43:05 2018):
   hello, world!
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# echo 'I will show you some code.' >> hello.txt
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# wall < hello.txt
   [root@iZwz97tbgo9lkabnat2lo8Z ~]#
   Broadcast message from root@iZwz97tbgo9lkabnat2lo8Z (Wed Jun 20 19:43:55 2018):
   hello, world!
   I will show you some code.
   ```

#### 别名

1. **alias**

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# alias ll='ls -l'
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# alias frm='rm -rf'
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ll
   ...
   drwxr-xr-x  2 root       root   4096 Jun 20 12:52 abc
   ...
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# frm abc
   ```

2. **unalias**

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# unalias frm
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# frm sohu.html
   -bash: frm: command not found
   ```

#### 其他程序

1. 时间和日期 - **date** / **cal**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# date
   Wed Jun 20 12:53:19 CST 2018
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cal
         June 2018
   Su Mo Tu We Th Fr Sa
                   1  2
    3  4  5  6  7  8  9
   10 11 12 13 14 15 16
   17 18 19 20 21 22 23
   24 25 26 27 28 29 30
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cal 5 2017
         May 2017
   Su Mo Tu We Th Fr Sa
       1  2  3  4  5  6
    7  8  9 10 11 12 13
   14 15 16 17 18 19 20
   21 22 23 24 25 26 27
   28 29 30 31
   ```

2. 录制操作脚本 - **script**。

3. 给用户发送消息 - **mesg** / **write** / **wall** / **mail**。

### 文件系统

#### 文件和路径

1. 命名规则：文件名的最大长度与文件系统类型有关，一般情况下，文件名不应该超过255个字符，虽然绝大多数的字符都可以用于文件名，但是最好使用英文大小写字母、数字、下划线、点这样的符号。文件名中虽然可以使用空格，但应该尽可能避免使用空格，否则在输入文件名时需要用将文件名放在双引号中或者通过`\`对空格进行转义。
2. 扩展名：在Linux系统下文件的扩展名是可选的，但是使用扩展名有助于对文件内容的理解。有些应用程序要通过扩展名来识别文件，但是更多的应用程序并不依赖文件的扩展名，就像`file`命令在识别文件时并不是依据扩展名来判定文件的类型。
3. 隐藏文件：以点开头的文件在Linux系统中是隐藏文件（不可见文件）。

#### 目录结构

1. /bin - 基本命令的二进制文件。
2. /boot - 引导加载程序的静态文件。
3. /dev - 设备文件。
4. **/etc** - 配置文件。
5. /home - 普通用户主目录的父目录。
6. /lib - 共享库文件。
7. /lib64 - 共享64位库文件。
8. /lost+found - 存放未链接文件。
9. /media - 自动识别设备的挂载目录。
10. /mnt - 临时挂载文件系统的挂载点。
11. /opt - 可选插件软件包安装位置。
12. /proc - 内核和进程信息。
13. **/root** - 超级管理员用户主目录。
14. /run - 存放系统运行时需要的东西。
15. /sbin - 超级用户的二进制文件。
16. /sys - 设备的伪文件系统。
17. /tmp - 临时文件夹。
18. **/usr** - 用户应用目录。
19. /var - 变量数据目录。

#### 访问权限

1. **chmod** - 改变文件模式比特。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l
   ...
   -rw-r--r--  1 root       root 211878 Jun 19 16:06 sohu.html
   ...
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# chmod g+w,o+w sohu.html
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l
   ...
   -rw-rw-rw-  1 root       root 211878 Jun 19 16:06 sohu.html
   ...
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# chmod 644 sohu.html
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l
   ...
   -rw-r--r--  1 root       root 211878 Jun 19 16:06 sohu.html
   ...
   ```

   > 说明：通过上面的例子可以看出，用`chmod`改变文件模式比特有两种方式：一种是字符设定法，另一种是数字设定法。除了`chmod`之外，可以通过`umask`来设定哪些权限将在新文件的默认权限中被删除。

   长格式查看目录或文件时显示结果及其对应权限的数值如下表所示。

   ![img](https://github.com/jackfrued/Python-100-Days/raw/master/Day31-35/res/file-mode.png)

1. **chown** - 改变文件所有者。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l
   ...
   -rw-r--r--  1 root root     54 Jun 20 10:06 readme.txt
   ...
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# chown hellokitty readme.txt
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ls -l
   ...
   -rw-r--r--  1 hellokitty root     54 Jun 20 10:06 readme.txt
   ...
   ```

#### 磁盘管理

1. 列出文件系统的磁盘使用状况 - **df**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# df -h
   Filesystem      Size  Used Avail Use% Mounted on
   /dev/vda1        40G  5.0G   33G  14% /
   devtmpfs        486M     0  486M   0% /dev
   tmpfs           497M     0  497M   0% /dev/shm
   tmpfs           497M  356K  496M   1% /run
   tmpfs           497M     0  497M   0% /sys/fs/cgroup
   tmpfs           100M     0  100M   0% /run/user/0
   ```

2. 磁盘分区表操作 - **fdisk**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# fdisk -l
   Disk /dev/vda: 42.9 GB, 42949672960 bytes, 83886080 sectors
   Units = sectors of 1 * 512 = 512 bytes
   Sector size (logical/physical): 512 bytes / 512 bytes
   I/O size (minimum/optimal): 512 bytes / 512 bytes
   Disk label type: dos
   Disk identifier: 0x000a42f4
      Device Boot      Start         End      Blocks   Id  System
   /dev/vda1   *        2048    83884031    41940992   83  Linux
   Disk /dev/vdb: 21.5 GB, 21474836480 bytes, 41943040 sectors
   Units = sectors of 1 * 512 = 512 bytes
   Sector size (logical/physical): 512 bytes / 512 bytes
   I/O size (minimum/optimal): 512 bytes / 512 bytes
   ```

3. 格式化文件系统 - **mkfs**。

4. 文件系统检查 - **fsck**。

5. 挂载/卸载 - **mount** / **umount**。

### 编辑器 - vim

1. 启动vim。可以通过`vi`或`vim`命令来启动vim，启动时可以指定文件名来打开一个文件，如果没有指定文件名，也可以在保存的时候指定文件名。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# vim guess.py
   ```

2. 命令模式、编辑模式和末行模式：启动vim进入的是命令模式（也称为Normal模式），在命令模式下输入英文字母`i`会进入编辑模式（Insert模式），屏幕下方出现`-- INSERT --`提示；在编辑模式下按下`Esc`会回到命令模式，此时如果输入英文`:`会进入末行模式，在末行模式下输入`q!`可以在不保存当前工作的情况下强行退出vim；在命令模式下输入`v`会进入可视模式（Visual模式），可以用光标选择一个区域再完成对应的操作。

3. 保存和退出vim：在命令模式下输入`:` 进入末行模式，输入`wq`可以实现保存退出；如果想放弃编辑的内容输入`q!`强行退出，这一点刚才已经提到过了；在命令模式下也可以直接输入`ZZ`实现保存退出。如果只想保存文件不退出，那么可以在末行模式下输入`w`；可以在`w`后面输入空格再指定要保存的文件名。

4. 光标操作。

   - 在命令模式下可以通过`h`、`j`、`k`、`l`来控制光标向左、下、上、右的方向移动，可以在字母前输入数字来表示移动的距离，例如：`10h`表示向左移动10个字符。
   - 在命令模式下可以通过`Ctrl+y`和`Ctrl+e`来实现向上、向下滚动一行文本的操作，可以通过`Ctrl+f`和`Ctrl+b`来实现向前和向后翻页的操作。
   - 在命令模式下可以通过输入英文字母`G`将光标移到文件的末尾，可以通过`gg`将光标移到文件的开始，也可以通过在`G`前输入数字来将光标移动到指定的行。

5. 文本操作。

* 删除：在命令模式下可以用`dd`来删除整行；可以在`dd`前加数字来指定删除的行数；可以用`d$`来实现删除从光标处删到行尾的操作，也可以通过`d0`来实现从光标处删到行首的操作；如果想删除一个单词，可以使用`dw`；如果要删除全文，可以在输入`:%d`（其中`:`用来从命令模式进入末行模式）。
* 复制和粘贴：在命令模式下可以用`yy`来复制整行；可以在`yy`前加数字来指定复制的行数；可以通过`p`将复制的内容粘贴到光标所在的地方。
* 撤销和恢复：在命令模式下输入`u`可以撤销之前的操作；通过`Ctrl+r`可以恢复被撤销的操作。
* 对内容进行排序：在命令模式下输入`%!sort`。

6. 查找和替换。

   - 查找操作需要输入`/`进入末行模式并提供正则表达式来匹配与之对应的内容，例如：`/doc.*\.`，输入`n`来向前搜索，也可以输入`N`来向后搜索。
   - 替换操作需要输入: 进入末行模式并指定搜索的范围、正则表达式以及替换后的内容和匹配选项，例如：    :1,$s/doc.*/hello/gice，其中：
     - `g` - global：全局匹配。
     - `i` - ignore case：忽略大小写匹配。
     - `c` - confirm：替换时需要确认。
     - `e` - error：忽略错误。

7. 参数设定：在输入`:`进入末行模式后可以对vim进行设定。

   - 设置Tab键的空格数：`set ts=4`

   - 设置显示/不显示行号：`set nu` / `set nonu`

   - 设置启用/关闭高亮语法：`syntax on` / `syntax off`

   - 设置显示标尺（光标所在的行和列）： `set ruler`

   - 设置启用/关闭搜索结果高亮：`set hls` / `set nohls`

     > 说明：如果希望上面的这些设定在每次启动vim时都能生效，需要将这些设定写到用户主目录下的.vimrc文件中。

8. 录制宏。

   - 在命令模式下输入`qa`开始录制宏（其中`a`是寄存器的名字，也可以是其他英文字母或0-9的数字）。
   - 执行你的操作（光标操作、编辑操作等），这些操作都会被录制下来。
   - 如果录制的操作已经完成了，按`q`结束录制。
   - 通过`@a`（`a`是刚才使用的寄存器的名字）播放宏，如果要多次执行宏可以在前面加数字，例如`100@a`表示将宏播放100次。
   - 可以试一试下面的例子来体验录制宏的操作，该例子来源于[Harttle Land网站](https://harttle.land/tags.html#Vim)，该网站上提供了很多关于vim的使用技巧，有兴趣的可以去了解一下。

### 软件安装和配置

#### 使用包管理工具

1. yum - Yellowdog Updater Modified。

- `yum search`：搜索软件包，例如`yum search nginx`。
- `yum list installed`：列出已经安装的软件包，例如`yum list installed | grep zlib`。
- `yum install`：安装软件包，例如`yum install nginx`。
- `yum remove`：删除软件包，例如`yum remove nginx`。
- `yum update`：更新软件包，例如`yum update`可以更新所有软件包，而`yum update tar只会更新tar。
- `yum check-update`：检查有哪些可以更新的软件包。
- `yum info`：显示软件包的相关信息，例如`yum info nginx`。

2. rpm - Redhat Package Manager。

- 安装软件包：`rpm -ivh <packagename>.rpm`。
- 移除软件包：`rpm -e <packagename>`。
- 查询软件包：`rpm -qa`，例如可以用`rpm -qa | grep mysql`来检查是否安装了MySQL相关的软件包。

下面以MySQL为例，演示如何使用rpm安装软件。要安装MySQL需要先到[MySQL官方网站](https://www.mysql.com/)下载对应的[RPM文件](https://dev.mysql.com/downloads/mysql/)，当然要选择和你使用的Linux系统对应的版本。MySQL现在是Oracle公司旗下的产品，在MySQL被收购后，MySQL的作者重新制作了一个MySQL的分支MariaDB，可以通过yum进行安装。如果要安装MySQL需要先通过yum删除`mariadb-libs`这个可能会跟MySQL底层库冲突的库，然后还需要安装一个名为`libaio`的依赖库。

```
[root@iZwz97tbgo9lkabnat2lo8Z mysql]# ls
mysql-community-client-5.7.22-1.el7.x86_64.rpm
mysql-community-common-5.7.22-1.el7.x86_64.rpm
mysql-community-libs-5.7.22-1.el7.x86_64.rpm
mysql-community-server-5.7.22-1.el7.x86_64.rpm
[root@iZwz97tbgo9lkabnat2lo8Z mysql]# yum -y remove mariadb-libs
[root@iZwz97tbgo9lkabnat2lo8Z mysql]# yum -y install libaio
[root@iZwz97tbgo9lkabnat2lo8Z mysql]# ls | xargs rpm -ivh
warning: mysql-community-client-5.7.22-1.el7.x86_64.rpm: Header V3 DSA/SHA1 Signature, key ID 5072e1f5: NOKEY
Preparing...                          ################################# [100%]
...
```

> 说明：由于MySQL和[MariaDB](https://mariadb.org/)的底层依赖库是有冲突的，所以上面我们首先用`yum`移除了名为mariadb-libs的依赖库并安装了名为libaio的依赖库。由于我们将安装MySQL所需的rpm文件放在一个独立的目录中，所以可以通过`ls`命令查看到安装文件并用`xargs`将`ls`的输出作为参数交给`rpm -ivh`来进行安装。关于MySQL和MariaDB之间的关系，可以阅读[维基百科](https://zh.wikipedia.org/wiki/MariaDB)上关于MariaDB的介绍。

移除安装的MySQL。

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# rpm -qa | grep mysql | xargs rpm -e
```

#### 下载解压配置环境变量

下面以安装MongoDB为例，演示这类软件应该如何安装。

```
[root@iZwz97tbgo9lkabnat2lo8Z ~]# wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-3.6.5.tgz
--2018-06-21 18:32:53--  https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-3.6.5.tgz
Resolving fastdl.mongodb.org (fastdl.mongodb.org)... 52.85.83.16, 52.85.83.228, 52.85.83.186, ...
Connecting to fastdl.mongodb.org (fastdl.mongodb.org)|52.85.83.16|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 100564462 (96M) [application/x-gzip]
Saving to: ‘mongodb-linux-x86_64-rhel70-3.6.5.tgz’
100%[==================================================>] 100,564,462  630KB/s   in 2m 9s
2018-06-21 18:35:04 (760 KB/s) - ‘mongodb-linux-x86_64-rhel70-3.6.5.tgz’ saved [100564462/100564462]
[root@iZwz97tbgo9lkabnat2lo8Z ~]# gunzip mongodb-linux-x86_64-rhel70-3.6.5.tgz
[root@iZwz97tbgo9lkabnat2lo8Z ~]# tar -xvf mongodb-linux-x86_64-rhel70-3.6.5.tar
mongodb-linux-x86_64-rhel70-3.6.5/README
mongodb-linux-x86_64-rhel70-3.6.5/THIRD-PARTY-NOTICES
mongodb-linux-x86_64-rhel70-3.6.5/MPL-2
mongodb-linux-x86_64-rhel70-3.6.5/GNU-AGPL-3.0
mongodb-linux-x86_64-rhel70-3.6.5/bin/mongodump
mongodb-linux-x86_64-rhel70-3.6.5/bin/mongorestore
mongodb-linux-x86_64-rhel70-3.6.5/bin/mongoexport
mongodb-linux-x86_64-rhel70-3.6.5/bin/mongoimport
mongodb-linux-x86_64-rhel70-3.6.5/bin/mongostat
mongodb-linux-x86_64-rhel70-3.6.5/bin/mongotop
mongodb-linux-x86_64-rhel70-3.6.5/bin/bsondump
mongodb-linux-x86_64-rhel70-3.6.5/bin/mongofiles
mongodb-linux-x86_64-rhel70-3.6.5/bin/mongoreplay
mongodb-linux-x86_64-rhel70-3.6.5/bin/mongoperf
mongodb-linux-x86_64-rhel70-3.6.5/bin/mongod
mongodb-linux-x86_64-rhel70-3.6.5/bin/mongos
mongodb-linux-x86_64-rhel70-3.6.5/bin/mongo
mongodb-linux-x86_64-rhel70-3.6.5/bin/install_compass
[root@iZwz97tbgo9lkabnat2lo8Z ~]# vim .bash_profile
...
PATH=$PATH:$HOME/bin:$HOME/mongodb-linux-x86_64-rhel70-3.6.5/bin
export PATH
...
[root@iZwz97tbgo9lkabnat2lo8Z ~]# source .bash_profile
[root@iZwz97tbgo9lkabnat2lo8Z ~]# mongod --version
db version v3.6.5
git version: a20ecd3e3a174162052ff99913bc2ca9a839d618
OpenSSL version: OpenSSL 1.0.1e-fips 11 Feb 2013
allocator: tcmalloc
modules: none
build environment:
    distmod: rhel70
    distarch: x86_64
    target_arch: x86_64
[root@iZwz97tbgo9lkabnat2lo8Z ~]# mongo --version
MongoDB shell version v3.6.5
git version: a20ecd3e3a174162052ff99913bc2ca9a839d618
OpenSSL version: OpenSSL 1.0.1e-fips 11 Feb 2013
allocator: tcmalloc
modules: none
build environment:
    distmod: rhel70
    distarch: x86_64
    target_arch: x86_64
```

> 说明：当然也可以通过yum来安装MongoDB，具体可以参照[官方网站](https://docs.mongodb.com/master/administration/install-on-linux/)上给出的说明。

#### 源代码构建安装

1. 安装Python 3.6。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# yum install gcc
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# wget https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tgz
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# gunzip Python-3.6.5.tgz
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ar -xvf Python-3.6.5.tar
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cd Python-3.6.5
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ./configure --prefix=/usr/local/python36 --enable-optimizations
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# make && make install
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ln -s /usr/local/python36/bin/python3.6 /usr/bin/python3
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# python3 --version
   Python 3.6.5
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# python3 -m pip install -U pip
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# pip3 --version
   ```

2. 安装Redis-3.2.12。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# wget http://download.redis.io/releases/redis-3.2.12.tar.gz
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# gunzip redis-3.2.12.tar.gz
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# tar -xvf redis-3.2.12.tar
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cd redis-3.2.12
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# make && make install
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# redis-server --version
   Redis server v=3.2.12 sha=00000000:0 malloc=jemalloc-4.0.3 bits=64 build=5bc5cd3c03d6ceb6
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# redis-cli --version
   redis-cli 3.2.12
   ```

### 配置服务

1. 启动服务。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# systemctl start firewalld
   ```

2. 终止服务。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# systemctl stop firewalld
   ```

3. 重启服务。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# systemctl restart firewalld
   ```

4. 查看服务。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# systemctl status firewalld
   ```

5. 设置是否开机自启。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# systemctl enable firewalld
   Created symlink from /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service to /usr/lib/systemd/system/firewalld.service.
   Created symlink from /etc/systemd/system/multi-user.target.wants/firewalld.service to /usr/lib/systemd/system/firewalld.service.
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# systemctl disable firewalld
   Removed symlink /etc/systemd/system/multi-user.target.wants/firewalld.service.
   Removed symlink /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.
   ```

### 计划任务

1. **crontab**命令。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# crontab -e
   * * * * * echo "hello, world!" >> /root/hello.txt
   59 23 * * * rm -f /root/*.log
   ```

   > 说明：输入`crontab -e`命令会打开vim来编辑Cron表达式并指定触发的任务，上面我们定制了两个计划任务，一个是每分钟向/root目录下的hello.txt中追加输出`hello, world!`；另一个是每天23时59分执行删除/root目录下以log为后缀名的文件。如果不知道Cron表达式如何书写，可以参照/etc/crontab文件中的提示（下面会讲到）或者用谷歌或百度搜索一下，也可以使用Cron表达式在线生成器来生成Cron表达式。

2. crontab相关文件。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# cd /etc
   [root@iZwz97tbgo9lkabnat2lo8Z etc]# ls -l | grep cron
   -rw-------.  1 root root      541 Aug  3  2017 anacrontab
   drwxr-xr-x.  2 root root     4096 Mar 27 11:56 cron.d
   drwxr-xr-x.  2 root root     4096 Mar 27 11:51 cron.daily
   -rw-------.  1 root root        0 Aug  3  2017 cron.deny
   drwxr-xr-x.  2 root root     4096 Mar 27 11:50 cron.hourly
   drwxr-xr-x.  2 root root     4096 Jun 10  2014 cron.monthly
   -rw-r--r--   1 root root      493 Jun 23 15:09 crontab
   drwxr-xr-x.  2 root root     4096 Jun 10  2014 cron.weekly
   [root@iZwz97tbgo9lkabnat2lo8Z etc]# vim crontab
     1 SHELL=/bin/bash
     2 PATH=/sbin:/bin:/usr/sbin:/usr/bin
     3 MAILTO=root
     4
     5 # For details see man 4 crontabs
     6
     7 # Example of job definition:
     8 # .---------------- minute (0 - 59)
     9 # |  .------------- hour (0 - 23)
    10 # |  |  .---------- day of month (1 - 31)
    11 # |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
    12 # |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
    13 # |  |  |  |  |
    14 # *  *  *  *  * user-name  command to be executed
   ```

   通过修改`/etc`目录下的crontab文件也能够定制计划任务。

### 网络访问和管理

1. 通过网络获取资源 - **wget**。

   - -b 后台下载模式
   - -O 下载到指定的目录
   - -r 递归下载

2. 显示/操作网络配置（旧） - **ifconfig**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ifconfig eth0
   eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
           inet 172.18.61.250  netmask 255.255.240.0  broadcast 172.18.63.255
           ether 00:16:3e:02:b6:46  txqueuelen 1000  (Ethernet)
           RX packets 1067841  bytes 1296732947 (1.2 GiB)
           RX errors 0  dropped 0  overruns 0  frame 0
           TX packets 409912  bytes 43569163 (41.5 MiB)
           TX errors 0  dropped 0 overruns 0  carrier 0  collisions 
   ```

3. 显示/操作网络配置（新） - **ip**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ip address
   1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
       link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
       inet 127.0.0.1/8 scope host lo
          valid_lft forever preferred_lft forever
   2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
       link/ether 00:16:3e:02:b6:46 brd ff:ff:ff:ff:ff:ff
       inet 172.18.61.250/20 brd 172.18.63.255 scope global eth0
          valid_lft forever preferred_lft forever
   ```

4. 网络可达性检查 - **ping**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ping www.baidu.com -c 3
   PING www.a.shifen.com (220.181.111.188) 56(84) bytes of data.
   64 bytes from 220.181.111.188 (220.181.111.188): icmp_seq=1 ttl=51 time=36.3 ms
   64 bytes from 220.181.111.188 (220.181.111.188): icmp_seq=2 ttl=51 time=36.4 ms
   64 bytes from 220.181.111.188 (220.181.111.188): icmp_seq=3 ttl=51 time=36.4 ms
   --- www.a.shifen.com ping statistics ---
   3 packets transmitted, 3 received, 0% packet loss, time 2002ms
   rtt min/avg/max/mdev = 36.392/36.406/36.427/0.156 ms
   ```

5. 查看网络服务和端口 - **netstat**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# netstat -nap | grep nginx
   ```

6. 安全文件拷贝 - **scp**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# scp root@1.2.3.4:/root/guido.jpg hellokitty@4.3.2.1:/home/hellokitty/pic.jpg
   ```

7. 安全文件传输 - **sftp**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# sftp root@120.77.222.217
   root@120.77.222.217's password:
   Connected to 120.77.222.217.
   sftp>
   ```

   - `help`：显示帮助信息。
   - `ls`/`lls`：显示远端/本地目录列表。
   - `cd`/`lcd`：切换远端/本地路径。
   - `mkdir`/`lmkdir`：创建远端/本地目录。
   - `pwd`/`lpwd`：显示远端/本地当前工作目录。
   - `get`：下载文件。
   - `put`：上传文件。
   - `rm`：删除远端文件。
   - `bye`/`exit`/`quit`：退出sftp。

### 进程管理

1. **ps** - 查询进程。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ps -ef
   UID        PID  PPID  C STIME TTY          TIME CMD
   root         1     0  0 Jun23 ?        00:00:05 /usr/lib/systemd/systemd --switched-root --system --deserialize 21
   root         2     0  0 Jun23 ?        00:00:00 [kthreadd]
   ...
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ps -ef | grep mysqld
   root      4943  4581  0 22:45 pts/0    00:00:00 grep --color=auto mysqld
   mysql    25257     1  0 Jun25 ?        00:00:39 /usr/sbin/mysqld --daemonize --pid-file=/var/run/mysqld/mysqld.pid
   ```

2. **kill** - 终止进程。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# kill 1234
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# kill -9 1234
   ```

   例子：用一条命令强制终止正在运行的Redis进程。

   ```
   ps -ef | grep redis | grep -v grep | awk '{print $2}' | xargs kill
   ```

3. 将进程置于后台运行。

   - `Ctrl+Z`
   - `&`

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# mongod &
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# redis-server
   ...
   ^Z
   [4]+  Stopped                 redis-server
   ```

4. **jobs** - 查询后台进程。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# jobs
   [2]   Running                 mongod &
   [3]-  Stopped                 cat
   [4]+  Stopped                 redis-server
   ```

5. **bg** - 让进程在后台继续运行。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# bg %4
   [4]+ redis-server &
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# jobs
   [2]   Running                 mongod &
   [3]+  Stopped                 cat
   [4]-  Running                 redis-server &
   ```

6. **fg** - 将后台进程置于前台。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# fg %4
   redis-server
   ^C5554:signal-handler (1530025281) Received SIGINT scheduling shutdown...
   5554:M 26 Jun 23:01:21.413 # User requested shutdown...
   5554:M 26 Jun 23:01:21.413 * Saving the final RDB snapshot before exiting.
   5554:M 26 Jun 23:01:21.415 * DB saved on disk
   5554:M 26 Jun 23:01:21.415 # Redis is now ready to exit, bye bye...
   ```

   > 说明：置于前台的进程可以使用`Ctrl+C`来终止它。

7. **top** - 进程监控。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# top
   top - 23:04:23 up 3 days, 14:10,  1 user,  load average: 0.00, 0.01, 0.05
   Tasks:  65 total,   1 running,  64 sleeping,   0 stopped,   0 zombie
   %Cpu(s):  0.3 us,  0.3 sy,  0.0 ni, 99.3 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
   KiB Mem :  1016168 total,   191060 free,   324700 used,   500408 buff/cache
   KiB Swap:        0 total,        0 free,        0 used.   530944 avail Mem
   ...
   ```

### 系统性能

1. 查看系统活动信息 - **sar**。

2. 查看内存使用情况 - **free**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# free
                 total        used        free      shared  buff/cache   available
   Mem:        1016168      323924      190452         356      501792      531800
   Swap:             0           0           0
   ```

3. 查看进程使用内存状况 - **pmap**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# ps
     PID TTY          TIME CMD
    4581 pts/0    00:00:00 bash
    5664 pts/0    00:00:00 ps
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# pmap 4581
   4581:   -bash
   0000000000400000    884K r-x-- bash
   00000000006dc000      4K r---- bash
   00000000006dd000     36K rw--- bash
   00000000006e6000     24K rw---   [ anon ]
   0000000001de0000    400K rw---   [ anon ]
   00007f82fe805000     48K r-x-- libnss_files-2.17.so
   00007f82fe811000   2044K ----- libnss_files-2.17.so
   ...
   ```

4. 报告设备CPU和I/O统计信息 - **iostat**。

   ```
   [root@iZwz97tbgo9lkabnat2lo8Z ~]# iostat
   Linux 3.10.0-693.11.1.el7.x86_64 (iZwz97tbgo9lkabnat2lo8Z)      06/26/2018      _x86_64_       (1 CPU)
   avg-cpu:  %user   %nice %system %iowait  %steal   %idle
              0.79    0.00    0.20    0.04    0.00   98.97
   Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
   vda               0.85         6.78        21.32    2106565    6623024
   vdb               0.00         0.01         0.00       2088          0
   ```