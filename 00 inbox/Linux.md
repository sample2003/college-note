# 一、Linux概述

## 1. Linux的诞生

Linux系统基于Unix系统，是Linux之父：Linus Benedict Torvalds在1991年创造的。Linux系统的组成由[**Linux系统内核**](https://www.kernel.org)和**系统级应用程序**两部分组成。

## 2. Linux的内核

内核提供了Linux系统的主要功能，如硬件调度管理的能力，Linux内核是免费开源的，这就代表了任何人都可以获得并修改内核，并且自行集成系统级程序。

## 3. Linux发行版

提供了内核+系统级程序的完整封装，称之为Linux发行版。Linux发行版有许多版本，主要分为debian系和redhat系，如本文的ubuntu系统就是由debian发展来的 的，centos就是redhat的免费版。

## 4. WSL

WSL：Windows Subsystem for Linux，是用于Windows系统之上的Linux子系统。可以在Windows系统中获得Linux系统环境，并完全直连计算机硬件，无需通过虚拟机虚拟硬件。

# 二、Linux开始

## 1. Linux安装

### 01 VMware虚拟机安装

1. 安装VMware虚拟机
2. 下载ubuntu镜像
3. 打开VMware虚拟机，点击创建新的虚拟机
![[011109562005_0屏幕截图_2024-01-11_094833.png|400]]

### 02 使用WSL安装

打开windows功能中的：适用于Linux的子系统

打开微软商店下载ubuntu，下载完打开即可

## 2. Linux配置

## 3. Linux目录结构

Linux的目录结构是一个树形结构，Linux没有盘符这个概念，只有一个根目录/，所有文件都在它下面
，在Linux系统中，路径之间的层级关系，使用：/来表示

## 4. Linux命令

Linux命令其实就是一个二进制可执行程序，和windows系统中的.exe文件是一个意思。

### ls：展示文件

>ls：在命令行中，以平铺的形式，展示当前工作目录（默认HOME目录）下的内容（文件或文件夹）；

HOME目录是每一个用户在Linux系统的专属目录，默认在：/home/用户名；

当前工作目录是Linux命令行在执行命令的时候，需要一个工作目录，打开命令行程序（终端）默认设置工作目录在用户的HOME目录；

==ls [option] linux路径==：在命令行中，以平铺的形式，展示该路径下的内容（文件或文件夹）；

-a选项，可选，表示all的意思，即列出全部文件（包含隐藏的文件/文件夹）；

-l选项，可选，表示以列表（竖向排列）的形式展示内容，并展示更多信息；

-h选项，可选，表示以易于阅读的方式，显示文件的大小；

选项之间可以组合使用，如：ls -l -a 路径，ls -al 路径；

### cd：切换目录

==cd linux路径==：切换目录；

linux路径：表示要切换到哪个目录下，如 cd /，切换到根目录；

### pwd：查看当前目录

==pwd==：查看当前所在的工作目录；

### 特殊路径符

. 表示当前目录；

.. 表示上一级目录；

~ 表示当前用户HOME目录；

### mkdir：创建文件夹

==mkdir [option] linux路径==：表示即要创建的文件夹的路径，相对或绝对路径皆可；

-p，选填，表示自动创建不存在的父目录，适用于创建连续多层级的目录；

### touch：创建文件

==touch linux路径==：touch命令无选项，路径必填，表示要创建的文件路径；

touch test{1..3}

### cat：查看文件

==cat linux路径==：cat命令无选项，路径必填，表示要查看的文件路径，并直接将内容全部显示出来；

### more：查看文件

==more linux路径==：more命令无选项，路径必填，表示要查看的文件路径，并支持翻页（空格），可以一页一页的展示，按q退出查看。

### cp：复制文件

==cp [option] 参数1 参数2==

-r：可选，用于复制文件夹使用，表示递归;
-a：此选项通常在复制目录时使用，它保留链接、文件属性，并复制目录下的所有内容。其作用等于dpR参数组合。  
-d：复制时保留链接。这里所说的链接相当于 Windows 系统中的快捷方式。  
-f：覆盖已经存在的目标文件而不给出提示。  
-i：与 -f 选项相反，在覆盖目标文件之前给出提示，要求用户确认是否覆盖，回答 y 时目标文件将被覆盖。  
-p：除复制文件的内容外，还把修改时间和访问权限也复制到新文件中。  
-r：若给出的源文件是一个目录文件，此时将复制该目录下所有的子目录和文件。  
-l：不复制文件，只是生成链接文件

参数1，表示被复制的文件或文件夹；

参数2，表示要复制去的地方。

### scp：复制文件

scp命令是cp命令的升级版，即ssh cp，通过SSH协议完成文件的复制。主要功能就是在不同的Linux服务器之间，通过SSH协议互相传输文件。只需知晓服务器的账号和密码（密钥），即可通过scp互传文件

==scp [option] 参数1 参数2==

-r：可选，用于复制文件夹使用，如果复制文件夹，必须使用-r

参数1：本机路径 或 远程目标路径

参数2：远程目标路径 或 本机路径

```shell
# 将本机上的jdk文件，以root的身份复制到node2的/export/server内
scp -r /export/server/jdk root@node2:/export/server/

# 将远程node2的jdk文件，复制到本机的/export/server内
scp -r node2:/export/server/jdk /export/server/

# 将本机当前路径的jdk文件，复制到node2服务器的同名路径下
scp -r jdk node2:`pwd`/
# or
scp -r jdk node2:$PWD
```

### mv：移动文件

==mv [option] 参数1 参数2==

-b: 当目标文件或目录存在时，在执行覆盖前，会为其创建一个备份。  
-i: 如果指定移动的源目录或文件与目标的目录或文件同名，则会先询问是否覆盖旧文件，输入 y 表示直接覆盖，输入 n 表示取消该操作。  
-f: 如果指定移动的源目录或文件与目标的目录或文件同名，不会询问，直接覆盖旧文件。  
-n: 不要覆盖任何已存在的文件或目录。  
-u：当源文件比目标文件新或者目标文件不存在时，才执行移动操作。

参数1，表示被移动的文件或文件夹；

参数2，表示移动去的地方。

### rm：删除文件

==rm [option] 参数1 参数2 ... 参数n==

参数1，参数2，... ，参数n，表示要删除的文件或文件夹

-r选项（recursion），可选，用于删除文件夹使用，表示递归

-f选项，强制删除

rm -rf / 等同于删除linux

### wc：统计行数等

==wc [option] 文件路径==

==wc 文件路径==：展示 行数 单词数量 字节数 文件名

-c，可选，统计bytes数量

-m，可选，统计字符数量

-l，可选，统计行数

-w，可选，统计单词数量

文件路径：必填，表示被统计的文件，可作为内容输入端口

### echo：输出信息

==echo==：输出的内容

==echo "hello world"==：含空格和\等特殊符号用双引号包裹

==echo \`pwd\`==：用飘号包裹将作为命令执行

==echo $Path==：查看环境变量的值

### tail：查看文件尾部内容

==tail [option] linux路径==

-f，可选，表示持续跟踪，停止ctrl + c

-num（具体数字），可选，表示查看尾部多少行，不填默认10行

linux路径：必填，表示被跟踪的文件路径

### which：查找命令位置

==which 要查找的命令==：如cd、pwd

### find：查找文件

==find 起始路径 -name 被查找文件名==

-name：表示按文件名查找

查找名为test.txt的文件：find / -name test

支持使用[[Linux#*：通配符|通配符*]]来做模糊查询

==find 起始路径 -size +/- n(kMG)==

-size：表示按文件大小查找

查大于10MB的文件：find / -size + 10M

查小于10KB的文件：find / -size - 10k

### grep：查找文件内容

==grep [option] 关键字 文件路径==

-n，可选，表示在结果中显示匹配的行的行号

关键字，必填，表示过滤的关键字，带有空格或其它特殊符号，用""包裹关键字

文件路径：必填，表示要过滤内容的文件路径，可作为内容输入端口

### [[Vim|vi编辑器]]

### su：切换账户

==su - 用户名==

-：可选项，表示是否在切换用户后加载环境变量；

用户名：表示要切换的用户，省略表示切换到root；

切换用户后，可以通过exit命令退回上一个用户，也可以使用快捷键：ctrl+d

### sudo：赋予root权限

==sudo 命令==：以root权限执行该命令；

root用户下执行visudo

在文件最后添加

用户名 ALL=(ALL)    NOPASSWD:ALL

### history：查看历史命令

==history==：查看历史命令

!命令前缀：自动执行上一次匹配前缀的命令

ctrl+r：输入内容去匹配历史命令，回车键直接执行，键盘左右键可以得到此命令（不执行）

### passwd：更改密码

passwd 用户名：更改密码，

### \*：通配符

test\*，表示匹配任何以test开头的内容

\*test，表示匹配任何以test结尾的内容

\*test\*，表示匹配任何包含test的内容

### |：管道符

==命令1 | 命令2==：将管道符左边的结果作为右边的输入，

如cat test.txt | wc ==> wc test.txt

### \> 和 >>：重定向符

`>`：将左侧命令的结果，**覆盖**写入符号右侧指定的文件中

`>>`：将左侧命令的结果，**追加**写入符号右侧指定的文件中

如，echo "hello linux" > test.txt

### jobs：查看当前任务

### nohub：后台运行

# 三、Linux进阶

## 用户与权限

linux系统中可以配置多个用户、多个用户组，用户可以加入多个用户组中，Linux权限管控的单元是用户级别和用户组级别；

以下命令须root用户执行，先切换为root用户或使用sudo命令；

### 给予普通用户root权限

终端执行如下命令
```shell
sudo visudo
# 或者
sudo vi /etc/sudoers
```

在打开的文件的最后添加
```txt
用户名 ALL=(ALL)    NOPASSWD:ALL
```

NOPASSWD:ALL表示使用sudo命令，无需输入密码

### groupadd：创建用户组

==groupadd 用户组名==

### groupdel：删除用户组

==groupdel 用户组名==

### useradd：创建用户

==useradd -g -d 用户名==

-g指定用户的组，不指定-g，会创建一个同名组并加入；指定-g，需要组已经存在

-d指定用户HOM路径，不指定，HOME目录默认在：/home/用户名

### userdel：删除用户

==userdel -r 用户名==

-r删除用户的HOME目录，不使用-r，删除用户时，HOME目录保留

### id：查看用户所属组

==id 用户名==

用户名，被查看的用户，如果不提，默认查看当前用户
### usermod：修改用户所属组

==usermod -aG 用户组 用户名==

### getent：查看系统中用户（组）

==getent passwd==

执行完成，输出共有7份信息，分别是：
用户名：密码（x）:用户ID:组ID:描述信息（无用）:HOME目录:执行终端（默认bash）

>sample:x:1000:1000:sample,,,:/home/sample:/bin/bash


==getent group==

执行完成，输出共有3份信息，分别是：
组名称:组认证（显示为x）:组ID

>sample:x:1000:


### 权限信息

通过ls -l 可以以列表形式查看内容，并显示权限细节

![[屏幕截图 2024-01-07 115312.png|600]]
- 序号1，表示文件、文件夹的权限控制信息，
- 序号2，表示文件、文件夹的所属用户
- 序号3，表示文件、文件夹的所属用户组
![[Pasted image 20240107120136.png|600]]
r：read查看    w：write修改    x：execute执行

### chmod：修改文件（夹）权限

只有文件、文件夹的所属用户或root用户可以修改

==chmod -R 权限 文件或文件夹==

-R，对文件夹内的全部内容应用同样的操作

如，chmod u=rwx,g=rx,o=x hello.txt，将文件权限改为了:rwxr-x--x
其中，u表示user所属用户权限，g表示group组权限，o表示other其他用户权限

快捷写法，如，chmod -R 751 test
其中：rwx(7)r-x(5)--x(1)，包含了二进制的计算
- 0：无任何权限，即---；
- 1：仅有x权限，即--x；
- 2：仅有w权限，即-w-；
- 3：有w和x权限，即-wx
- 4：仅有r权限，即r--；
- 5：有r和x权限，即r-x；
- 6：有r和w权限，即rw-；
- 7：有全部权限，即rwx；

### chown：修改文件（夹）所属用户（组）

普通用户无法修改所属为其它用户或组，所以此命令只适用于root用户执行

==chown -R 用户:用户组 文件或文件夹==

-R，对文件夹内的全部内容应用同样的操作

用户，修改所属用户

用户组，修改所属用户组

:，用于分隔用户和用户组

如，
chown root hello.txt ==> 修改文件所属用户为root；
chown :root hello.txt ==> 修改文件所属用户组为root；
chown root:root hello.txt ==> 修改文件所属用户为root，所属用户组为root；

## 状态管理

### 进程

程序运行在操作系统中，是被操作系统所管理的。为管理运行的程序，每一个程序在运行的时候，便被操作系统注册为系统中的一个：进程。并会为每一个进程都分配一个独有的进程ID（进程号）。

#### ps：查看进程

==ps -e -f==

-e：显示出全部的进程

-f：以完全格式化的形式展示信息（展示全部信息）

一般会配合grep使用：ps -ef | grep 进程

输出显示信息：
UID：进程所属的用户ID
PID：进程的进程号
PPID：进程的父ID（启动该进程的进程ID）
C：此进程的CPU占有率（百分比）
STIME：进程的启动时间
TTY：启动此进程的终端序号，如果显示?，表示非终端启动
TIME：进程占用CPU的时间
CMD：进程对应的名称或启动路径或启动命令

#### kill：关闭进程

==kill -9 进程ID==

-9：可选，表示强制关闭进程。

### 查看系统资源占用

==top==：可以查看CPU、内存使用情况，默认每5秒刷新一次，使用q或ctrl+c退出

##### 选项
-p：只显示某个进程的信息

-d：设置刷新时间,默认是5s

-c：显示产生进程的完整命令,默认是进程名

-n：指定刷新次数,比如 top -n 3,刷新输出3次后退出

-b：以非交互非全屏模式运行,以批次的方式执行top,一般配合-n指定输出几次统计信息,将输出重定向到指定文件,比如 top -b -n 3>/tmp/top.tmp

-u：不显示任何闲置(idle)或无用(zombie)的进程

-i：查找特定用户启动的进程

##### 交互式选项

当top以交互式运行(非-b选项启动),可以用以下交互式命令进行控制

按下h键,会显示帮助画面

按下c键,会显示产生进程的完整命令,等同于-c参数,再次按下c键,变为默认显示

按下f键,可以选择需要展示的项目

按下M键,根据驻留内存大小(RES)排序

按下P键,根据CPU使用百分比大小进行排序

按下T键,根据时间/累计时间进行排序

按下E键,切换顶部内存显示单位

按下e键,切换进程内存显示单位

按下1键,切换显示平均负载和启动时间信息。

按下i键,不显示闲置或无用的进程,等同于-i参数,再次按下,变为默认显示

按下t键,切换显示CPU状态信息

按下m键,切换显示内存信息

##### 输出显示信息解析
第一行
top:命令名称；14:39:58:当前系统时间；up 6min:启动了6分钟；users:2个用户登录；load:1、5、15分钟负载

第二行
Tasks:175个进程；1running:1个进程子在运行；174sleeping:174个进程睡眠；0个停止进程；0个僵尸进程

第三行
%Cpu(s):CPU使用率；us:用户CPU使用率；sy: 系统CPU使用率；ni:高优先级进程占用CPU时间百分比；id:空闲CPU率；wa:IO等待CPU占用率；hi:CPU硬件中断率；si:CPU软件中断率；st: 强制等待占用CPU率


第四、五行
Kib Mem:物理内存；total:总量；free:空闲；used:使用；buff/cache:buff和cache占用
KibSwap:虚拟内存(交换空间)；total:总量,free:空闲,used:使用,buff/cache:buff和cache占用

后面的列表
PID:进程id
USER:进程所属用户
PR:进程优先级,越小越高
NI: 负值表示高优先级,正表示低优先级
VIRT:进程使用虚拟内存,单位KB
RES:进程使用物理内存,单位KB
SHR:进程使用共享内存,单位KB
S:进程状态(S休眠,R运行, Z僵死状态, N负数优先级,I空闲状态)
%CPU:进程占用CPU率
%MEM:进程占用内存率
TIME+:进程使用CPU时间总计,单位10毫秒
COMMAND:进程的命令或名利或程序文件路径

### 磁盘信息监控

==df -h==：查看硬盘的使用情况

-h：可选，以更加人性化的单位显示

==iostat -x num1 num2==

-x：可选，显示更多信息

wrqm/s:
rsec/s:
wsec/:
rKB/s:
WKB/s:
avgrq-sz
avgqu-sz
await:
svctm
%util:

num1：刷新间隔

num2：刷新次数

### 网络监控

==sar -n DEV num1 num2==

-n：查看网络

DEV：表示查看网络接口

num1：刷新间隔（不填就查看一次结束）

num2：刷新次数（不填无限次数）

### 环境变量

环境变量是操作系统在运行的时候，记录的一些关键性信息，用以辅助系统运行，环境变量是一种KeyValue型结构

环境变量PATH，会记录一组目录，目录之间用:隔开。这里记录的是命令的搜索路径，执行命令会从记录中记录的目录挨个搜索要执行的命令并执行。

查看环境变量

==env==

取出环境变量的值：

==echo $Path==

临时生效的环境变量

==export 变量名=值==

当前用户永久生效的环境变量

```shell
vim ~/.bashrc
# 在文件中添加 
export 变量名=值
# 保存退出
source ~/.bashrc
```

所有用户永久生效的环境变量

```shell
vim /etc/profile
# 在文件中添加 
export 变量名=值
# 保存退出
source /etc/profile
```

配置一个所有场景都可执行的文件

```shell
# 在root用户下执行
mkdir myenv,
cd myenv
vim mypath
# 添加具体执行内容并保存退出
chmod 755 mypath
vim /etc/profile
export PATH=$PATH:/root/myenv
source /etc/profile
```

### 端口

Linux系统支持65535个端口,分为3类使用

>公认端口:1~1023,通常用于一些系统内置或知名程序的预留使用,如SSH服务的22端口,HTTPS服务的443端口,非特殊需要,不要占用这个范围的端口

>注册端口:1024~49151,通常可以随意使用,用于松散的绑定一些程序\服务

>动态端口:49152~65535,通常不会固定绑定程序,而是当程序对外进行网络链接时,用于临时使用。

查看端口占用:
==ss -tuln | grep 端口==

==lsof -i:端口号==

## 网络相关

### 在VMware中配置固定IP

当前IP地址是通过DHCP服务获取的。动态获取IP地址，每次重新启动都要再次配置

1. 在VMWare中配置IP地址网关和网段（IP地址的范围）
![[屏幕截图 2024-01-11 100238 1.png|400]]
![[Pasted image 20240111101111.png|400]]
2. 在centos系统中手动修改配置文件，固定IP
```shell
vim /etc/sysconfig/network-scripts/ifcfg-ens33

# 要改的部分
...
BOOTPROTO="static"
ONBOOT=yes
...
IPADDR="192.168.88.130"
NETMASK="255.255.255.0"
GATEWAY="192.168.88.2"
DNS1="192.168.88.2"
# 改完重启网卡
systemctl restart network
```
3. 在ubuntu系统中手动修改配置文件，固定IP
```shell
cd /etc/netplan

# 编辑该文件夹下的yaml文件
vim *.yaml

# 添加
network:
	version: 2
	renderer: NetworkManager
	ethernets:
		ens33:
			dhcp4: false
			addresses: [192.168.88.130/24]
			gateway4: 192.168.88.2
			nameservers:
				addresses: [192.168.88.2]
# 另一种写法
network:
  ethernets:
    ens33:
      addresses:
      - 192.168.220.131/24
      gateway4: 192.168.220.2
      nameservers:
        addresses:
        - 192.168.220.2
        search:
        - 8.8.8.8
# 保存退出
sudo netplan apply
```

4. 找到网络选项，关闭自动，选择手动

### ping：检查网络状态

可以通过ping命令，检查指定的网络服务器是否是可联通状态

==ping -c num ip或主机名==

-c num：检查的次数，不使用将无限次检查

### wget：下载

wget是非交互式的文件下载器，可以在命令行内下载网络文件，下载在当前目录

==wget -b url==

-b：可选，后台下载，会将日志写入wget-log

url：下载链接

可以通过tail命令监控后台下载进度：tail -f wget-log

### curl：发送http请求

curl可用于下载文件、获取信息

==curl -O url==

-O：可选，用于下载文件，当url是下载链接，可以使用此选项保存文件

url：要发送请求的网络链接

## 基本使用

### yum apt：软件安装

(yum)(apt) 命令：需要root权限

yum：RPM包软件管理器，用于自动化安装配置Linux软件，并可以自动解决依赖问题。

apt：DEB包软件管理器

==(yum)(apt) -y install | remove | search | update 软件名称==

-y：确认安装

install：安装

remove：卸载

search：搜索

update：更新

### rz：文件上传与 sz：文件下载

rz、sz命令安装：
==apt -y install lrzsz==

会弹出一个窗口，选择要上传的文件
==rz==

要下载的文件
==sz==

### 文件解压与压缩

Linux系统中操作：tar、gzip、zip这三种压缩格式

#### tar

.tar，称之为tarball，归档文件，即简单的将文件组装到一个.tar的文件内，并没有太多文件体积的减少，仅仅是简单的封装

.gz，也称为.tar.gz，gzip格式压缩文件，即使用gzip压缩算法将文件压缩到一个文件内，可以极大的减少压缩后的体积

这两种格式，使用tar命令均可以进行压缩和解压缩的操作

==tar -c -v -x -f -z -C 参数1 参数2 ... 参数n==

-c, 创建压缩文件,用于压缩模式

-v, 显示压缩、解压过程,用于查看进度

-x, 解压模式

-f, 要创建的文件,或要解压的文件,-f选项必须在所有选项中位置处于最后一个

-z, gzip模式,不使用-z就是普通的tarball格式

-C, 选择解压的目的地, 用于解压模式

常用压缩命令
```shell
# 将3个txt文件压缩到test.tar文件中
tar -cvf test.tar 1.txt 2.txt 3.txt

# 将3个txt文件压缩到test.tar.gz文件中
tar -zcvf test.tar.gz 1.txt 2.txt 3.txt
```
常用解压命令
```shell
# 将test.tar解压到当前目录
tar -xvf test.tar

# 将test.tar解压到指定目录
tar -xvf test.tar -C /home/sample

# 以gzip模式解压test.tar.gz，解压到指定目录
tar -zxvf test.tar.gz -C /home/sample
```

#### zip

==zip -r 参数1 参数2 ... 参数n==

-r：被压缩的包含文件夹时，需要使用-r选项

参数n：要压缩对文件

常用压缩命令
```shell
# 将3个txt文件压缩到test.zip文件中
zip test.zip 1.txt 2.txt 3.txt

# 将3个txt文件和一个文件夹压缩到test.zip文件中
zip -r test.zip test 1.txt 2.txt 3.txt
```

#### unzip

==unzip -d 参数==

-d：指定要解压去的位置，同tar的-C选项

参数：被解压的zip压缩包文件

常用解压命令
```shell
# 将test.zip解压到当前目录
unzip test.zip

# 将test.zip解压到指定目录
unzip test.zip -d /home/sample
```

### ln：软链接

在系统中创建软链接，可以将文件，文件夹链接到其它位置，类似windows系统中的快捷方式

==ln -s 参数1 参数2==

-s，可选，创建软连接

参数1：被链接的文件或文件夹

参数2：要链接去的目的地

### date：查看时间

通过date命令可以在命令行中查看系统的时间

==date -d +格式化字符串==

-d 按照给定的字符串显示日期,一般用于日期计算
支持的时间标记为：
year 年
month 月
day 天
hour 小时
minute 分钟
second 秒

格式化字符串:通过特定的字符串标记,来控制显示的日期格式
%Y 年份
%y 年份后两位数字(00-99)
%m 月份(01-12)
%d 日 (01-31)
%H 小时(00-23)
%M 分钟(00-59)
%S 秒(00-60)
%s 自$1970-01-01 00:00:00UTC到现在的秒数

### 修改Linux时区

使用root权限，执行如下命令，修改时间为东八区

```shell
rm -f /etc/localtime
sudo ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

### 主机名

**查看主机名**

==hostname==

地址文件在 /etc/hosts 

**修改主机名**

使用root权限，执行如下命令

```shell
hostnamectl set-hostname 主机名
```

**配置主机名映射**

Linux打开hosts文件
```shell
sudo vim /etc/hosts
```

Windows打开hosts文件
```shell
C:\Windows\System32\driver\etc\hosts
```

添加映射
```txt
xxx.xxx.xxx.xxx 映射名
如
127.0.0.1 localhost
192.168.88.131 node1
192.168.88.132 node2
192.168.88.133 node3
```

### 快捷键

ctrl + c：强制停止

ctrl + a：退出登出

ctrl + l：清屏

光标移动快捷键

ctrl + a：跳到命令开头

ctrl + e：跳到命令结尾

ctrl + ←：向左跳一个单词

ctrl + →：向右跳一个单词

## 服务

### systemctl：控制服务

Linux系统很多软件均支持使用systemctl控制，能被systemctl管理的软件，一般被称为服务

==systemctl start | stop | status | enable | disable 服务名==

start：开启

stop：停止

status：状态

enable：开机自启

disable：关闭开机自启

查看全部服务
systemctl list-units --type=service

### ntp

自动校准系统时间

启动并设置开机自启
```shell
systemctl start ntpd
systemctl enable ntpd
```

手动校准时间

ntpdate -u ntp.aliyun.com

### firewall

防火墙状态
```shell
systemctl status firewalld      # 查看防火墙状态
systemctl start firewalld       # 开启防火墙
systemctl restart firewalld     # 重启防火墙
systemctl stop firewalld        # 关闭防火墙
systemctl enable firewalld      # 开机自启
systemctl stop firewalld        # 关闭开机自启
```

查看防火墙规则
```shell
firewall-cmd --list-all
```

开放防火墙
1. 动态方式：现在设置立马可以起作用，但是一旦重启防火墙服务则动态设置的规则消失
```shell
firewall-cmd --zone=public --add-service=http
```
2. 静态方式：设置之后不会立马起作用，需要重启防火墙才能起作用，而且是永久起作用
```shell
firewall-cmd --zone=public --add-service=http --permanent
systemctl restart firewalld
```

### ssh

安装并开启ssh服务
```shell
sudo apt install openssh-server
sudo service ssh restart
```

ssh密码登录

先设置root密码
```shell
sudo passwd root
```
然后编辑ssh配置文件
```shell
vim /etc/ssh/sshd_config
```
重启服务器

ssh免密登录

每一台服务器都生成秘钥文件
```shell
ssh-keygen -t rsa -b 4096
# 接下来一路回车
```
把秘钥文件给所有服务器
```shell
ssh-copy-id node1 / 192.168.88.130
```

# 四、软件部署

## Docker

### 安装Docker

```sh
cat <<EOF > /etc/sysctl.d/docker.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.conf.default.rp_filter = 0
net.ipv4.conf.all.rp_filter = 0
net.ipv4.ip_forward=1
EOF

sysctl -p /etc/sysctl.d/docker.conf
```

### Docker安装Redis

1. 下载Redis镜像
	```sh
	docker pull redis:6.2.5
	```
2. 挂载redis的conf文件
	```sh
	mkdir -p /export/data/docker/redis/conf
	vim /export/data/docker/redis/conf/redis.conf
	```

	```vim
	# bind 192.168.1.100 10.0.0.1
	# bind 127.0.0.1 ::1
	bind 0.0.0.0
	protected-mode no
	port 6379
	tcp-backlog 511
	requirepass 000415
	timeout 0
	tcp-keepalive 300
	daemonize no
	supervised no
	pidfile /var/run/redis_6379.pid
	loglevel notice
	logfile ""
	databases 30
	always-show-logo yes
	save 900 1
	save 300 10
	save 60 10000
	stop-writes-on-bgsave-error yes
	rdbcompression yes
	rdbchecksum yes
	dbfilename dump.rdb
	dir ./
	replica-serve-stale-data yes
	replica-read-only yes
	repl-diskless-sync no
	repl-disable-tcp-nodelay no
	replica-priority 100
	lazyfree-lazy-eviction no
	lazyfree-lazy-expire no
	lazyfree-lazy-server-del no
	replica-lazy-flush no
	appendonly yes
	appendfilename "appendonly.aof"
	no-appendfsync-on-rewrite no
	auto-aof-rewrite-percentage 100
	auto-aof-rewrite-min-size 64mb
	aof-load-truncated yes
	aof-use-rdb-preamble yes
	lua-time-limit 5000
	slowlog-max-len 128
	notify-keyspace-events ""
	hash-max-ziplist-entries 512
	hash-max-ziplist-value 64
	list-max-ziplist-size -2
	list-compress-depth 0
	set-max-intset-entries 512
	zset-max-ziplist-entries 128
	zset-max-ziplist-value 64
	hll-sparse-max-bytes 3000
	stream-node-max-bytes 4096
	stream-node-max-entries 100
	activerehashing yes
	hz 10
	dynamic-hz yes
	aof-rewrite-incremental-fsync yes
	rdb-save-incremental-fsync yes
	```
3. 启动redis容器
```shell
docker run 
-p 6379:6379 \
--name redis6 \
--restart=always \
--log-opt max-size=100m \
--log-opt max-file=2 \
-v /export/data/docker/redis/conf/redis.conf:/etc/redis/redis.conf \
-v /export/data/docker/redis/data:/data \
-d redis:6.2.5 redis-server /etc/redis/redis.conf \
--appendonly yes --requirepass 123456
```

### Docker安装mongodb

创建外部挂载文件
```sh
mkdir -p /export/data/docker/mongodb/conf
mkdir -p /export/data/docker/mongodb/data
mkdir -p /export/data/docker/mongodb/logs
touch /export/data/docker/mongodb/conf/mongod.conf
chmod 777 /export/data/docker/mongodb
```

编辑mongod.conf
```conf
# 数据库文件存储位置
dbpath = /data/db
# log文件存储位置
logpath = /data/log/mongod.log  
#pid运行目录  
#pidfilepath = /var/run/mongodb/mongodb.pid
# 使用追加的方式写日志
logappend = true  
#启用日志文件，默认启用  
journal=true

#最大连接数  
maxConns=2048
# 是否以守护进程方式运行
# fork = true
# 全部ip可以访问
bind_ip = 0.0.0.0
# 端口号
port = 27017
# 是否启用认证
auth = true
# 设置oplog的大小(MB)
oplogSize=1755
```

运行mongo容器
```shell
docker run -dit --name mongo6 \
-p 27017:27017 \
-v /export/data/docker/mongodb/conf/mongod.conf:/etc/mongod.conf \
-v /export/data/docker/mongodb/data:/data/db \
-v /export/data/docker/mongodb/logs:/var/log/mongodb \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=123456 \
--restart=always  \
mongo:6.0
```

### Docker安装MySQL

1. 下载mysql:8.0镜像
	```sh
	# 检查docker是否可以下载mysql镜像
	docker search mysql
	# 下载mysql8.0镜像
	docker pull mysql:8.0
	```
2. 先简单安装运行
	```sh
	docker run -p 3306:3306 --name mysql8 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:8.0
	# 如果设置不区分大小写，运行下面代码，拷贝data文件之前就要执行，否则报错
	docker run -p 3306:3306 --name mysql8 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:8.0 --lower_case_table_names=1
	```
3. 拷贝容器文件到本地
	```sh
	# 若没有该文件夹则创建
	mkdir -p /export/data/docker/mysql
	cd /export/data/docker/mysql
	mkdir conf; mkdir data; mkdir logs;
	# 拷贝mysql配置文件到本地
	docker cp mysql8:/etc/mysql /export/data/docker/mysql/conf
	# 拷贝mysql配置文件数据源到本地
	docker cp mysql8:/var/lib/mysql /export/data/docker/mysql/data
	# 在本地创建logs日志存储文件
	# 创建错误日志存放文件
	mkdir -p /export/data/docker/mysql/logs/error/
	touch /export/data/docker/mysql/logs/error/error_log.log
	 
	# 不建议改
	# 创建查询日志存放地址  原地址/var/lib/mysql/9056323b388c.log 最好复制源文件否则有权限问题
	# 在外部加了mysql权限没成功，直接在运行容器时加了--privilged  也没成功
	mkdir -p /export/data/docker/mysql/logs/general/
	touch /export/data/docker/mysql/logs/general/mysql_general.log
	# 创建慢查询日志存放文件 原本存在/var/lib/mysql/9056323b388c-slow.log 最好复制源文件否则有问题
	mkdir -p /export/data/docker/mysql/logs/show_query/
	touch /export/data/docker/mysql/logs/show_query/show_query.log
	# 给日志赋权限
	chmod 777 /export/data/docker/mysql/logs/error/error_log.log
	chmod 777 /export/data/docker/mysql/logs/general/mysql_general.log
	chmod 777 /export/data/docker/mysql/logs/show_query/show_query.log
	 
	#chmod -R 777 /usr/local/src/docker/mysql/logs/
	```
4. my.cnf配置参考
	```conf
	#配置mysql my.cnf文件
	vim /export/data/docker/mysql/conf/my.cnf
	####################my.cnf##################
	[mysqld]
	#pid-file 指定将进程 ID 写入的文件的路径，以便其他程序或脚本可以轻松地访问该文件并使用 MySQL 服务器进程的 PID
	pid-file        = /var/run/mysqld/mysqld.pid   
	#MySQL 在本地可以通过 socket 方式连接，如果 my.cnf 配置文件中的 [client] 部分没有指定 socket 文件路径，mysql 默认会去寻找 /tmp/mysql.sock ，为了安全考虑，通常会设置特定的socket路径
	socket          = /var/run/mysqld/mysqld.sock
	#数据目录文件，需要保证它的权限和目录大小
	datadir         = /var/lib/mysql
	#指定允许读取和写入的目录位置
	secure-file-priv= NULL
	 
	user = mysql    #mysql用户
	prot = 3306     #mysql端口号
	#选项可以用来指定 MySQL 服务器应该使用哪种身份验证方式和插件
	authentication_policy=mysql_native_password
	 
	server_id = 3306     #mysql服务的ID 一般用于主从 具有唯一性
	 
	character_set_server = UTF8MB4 #指定 MySQL 服务器使用的默认字符集
	skip_name_resolve = 1
	#admin-address 选项定义了一个或多个管理员的联系信息，以便 MySQL 服务器可以向其发送通知或警报。这些联系信息通常包括电子邮件地址和名称，但也可以包括其他信息，如电话号码等。
	#admin_address = '127.0.0.1'
	#admin_port = 33062
	 
	#lower_case_table_names 的取值有以下几种
	#0：表名使用大小写敏感的方式处理。
	#1：表名在存储时将被转换为小写字母，但在检索时保持原样，此时如果存在大小写相同但是内容不同的表名，将会出现错误。
	#2：表名在存储和检索时都将被转换为小写字母，这样可以避免大小写不匹配的问题，但可能导致表名冲突。
	# 需要注意的是，lower_case_table_names 选项对已经存在的表名不会产生影响，只会影响新创建的表名。如果在 MySQL 数据库中已经存在表名，应该在设置 lower_case_table_names 选项之前备份数据，并进行相应的调整。
	lower_case_table_name = 2
	#local-infile 控制是否允许在客户端本地加载数据文件，即将数据文件从客户端传输到服务器，然后使用LOAD DATA INFILE语句将数据加载到 MySQL 表中。选项被设置为 ON，则允许在客户端本地加载数据文件。如果该选项被设置为 OFF，则不允许在客户端本地加载数据文件。
	local-infile = no
	 
	 
	 
	lock_wait_timeout = 3600        #事务锁等待超时时间
	open_files_limit = 65535        #操作系统对mysqld可用的文件描述符的限制
	back_log = 1024                 #表示在 MySQL 暂时停止响应新请求之前的这段短时间内可以堆叠多少请求
	max_connections = 10240         #mysql接受的最大连接数
	max_connect_errors = 1000000    #来自主机的连续连接请求在没有成功连接的情况下被中断后 服务器阻止该主机进一步连接
	table_open_cache = 20000        #所有线程打开表的数量
	table_definition_cache = 2000   #增加这个参数加速打开表的速度
	thread_stack = 512k             #每个线程的堆栈大小。如果线程堆栈大小太小，它会限制服务器可以处理的 SQL 语句的复杂性、存储过程的递归深度以及其他消耗内存的操作。默认值（64 位平台，≥ 8.0.27） 1048576   默认值（64 位平台，≤ 8.0.26） 286720
	sort_buffer_size = 2M           #每个必须执行排序的会话都会分配一个此大小的缓冲区 增加该值加速order by 或group by 的速度
	#join_buffer_size = 4M
	#read_buffer_size = 8M
	#read_rnd_buffer_size = 4M
	#bulk_insert_buffer_size = 64M
	 
	thread_cache_size = 256         #服务区缓存线程的数量 当客户端断开连接时，如果客户端的线程少于 thread_cache_size线程，则将其放入缓存中。如果可能，通过重用从缓存中获取的线程来满足对线程的请求，并且只有当缓存为空时才会创建新线程，默认值公式 上限为 100：
	#interactive_timeout = 600
	#wait_timeout = 600
	tmp_table_size 32M              #存储引擎创建的内部内存临时表的最大大小MEMORY
	max_heap_table_size = 32M
	 
	#log settings
	log_timestamps = SYSTEM        #log中日志文件记录时间戳的时区 Default Value UTC
	log_error = /var/log/mysql/mysql-error.log    ##错误日志路径
	log_error_verbosity = 3        #日志输出等级 log_error_verbosity Value Permitted Message Priorities  1 ERROR    2 ERROR, WARNING    3 ERROR, WARNING, INFORMATION
	slow_query_log = 1   #慢日志开启
	log_slow_extra = 1 #输出额外信息到slow log中  Thread_id: ID Errno: error_number Bytes_received: N Bytes_sent: N
	show_query_log_file = /var/log/mysql/mysql-slow.log  #慢查询的存放路径
	long_query_time = 0.1  #慢查询阈值
	#log_queries_not_using_indexes = 1 
	#log_throttle_queries_not_using_indexes = 60
	#min_examined_row_limit = 100
	log_slow_admin_statements = 1 #记录以下语句慢查询ALTER TABLE、 ANALYZE TABLE、 CHECK TABLE、 CREATE INDEX、 DROP INDEX、 OPTIMIZE TABLE和 REPAIR TABLE。
	log_show_replica_statements = 1
	 
	log_bin = /var/log/mysql/mysql_bin        #开启binlog
	binlog_format = ROW                       #binlog 格式
	sync_binlog = 1000    
	#sync_binlog=0：禁用MySQL服务器将二进制日志同步到磁盘。相反，MySQL 服务器依靠操作系统不时将二进制日志刷新到磁盘，就像它对任何其他文件所做的那样。此设置提供最佳性能，但在电源故障或操作系统崩溃的情况下，服务器可能已提交尚未同步到二进制日志的事务。
	#sync_binlog=1：在提交事务之前启用二进制日志到磁盘的同步。这是最安全的设置，但由于磁盘写入次数增加，可能会对性能产生负面影响。在电源故障或操作系统崩溃的情况下，二进制日志中丢失的事务仅处于准备状态。这允许自动恢复例程回滚事务，从而保证二进制日志中不会丢失任何事务。
	#sync_binlog=N，其中N是 0 或 1 以外的值：二进制日志在 N收集二进制日志提交组后同步到磁盘。在电源故障或操作系统崩溃的情况下，服务器可能已提交尚未刷新到二进制日志的事务。由于磁盘写入次数增加，此设置可能会对性能产生负面影响。较高的值可提高性能，但会增加数据丢失的风险。
	 
	 
	 
	 
	 
	binlog_cache_size = 4M #事务期间用于保存二进制日志更改的内存缓冲区的大小。
	max_binlog_cache_size = 2G #如果一个事务需要超过这个字节数的内存，服务器会生成一个Multi-statement transaction required more than ‘max_binlog_cache_size’ bytes of storage错误
	最大推荐值为4GB；这是因为 MySQL 当前无法处理大于 4GB 的二进制日志位置
	max_binlog_size = 1G      #如果写入二进制日志导致当前日志文件大小超过此变量的值，则服务器轮换二进制日志（关闭当前文件并打开下一个文件）
	binlog_rows_query_log_events = 1     #把sql语句打印到binlog日志里面
	binlog_expire_logs_seconds = 604800  #设置binlog过期时间 单位 秒
	 
	#mysql 8.0.22前，想用MGR的话需要设置binlog_checksum=NONE才醒
	binlog_checksum = CRC32
	 
	#myisam settings
	key_buffer_size = 32M
	mysiam_sort_buffer_size = 128M
	replication settings
	relay_log = /data/logs01/relaylog
	relay_log_index = /data/logs01/mysqld_relay_bin.index
	relay_log_recovery = 1
	replica_parallel_type = LOGICAL_CLOCK
	replica_parallel_workers = 16 #可以设置为逻辑CPU数量的2倍
	binlog_transaction_dependency_tracking = WRITESET
	replica_preserve_commit_order = 1
	replica_checkpoint_period  = 2
	skip_replica_start = ON
	read_only = 0 
	gtid_mode = ON
	enforce_gtid_consistency = ON
	replica_transaction_retries    = 128
	#
	#
	##mgr settings
	##loose-plugin_load_add = 'mysql_clone.so'
	##loose-plugin_load_add = 'group_replication.so'
	##loose-group_replication_group_name = "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaa1"
	##MGR本地节点IP:PORT，请自行替换
	##loose-group_replication_local_address = "172.16.16.10:33061"
	##MGR集群所有节点IP:PORT，请自行替换
	##loose-group_replication_group_seeds = "172.16.16.10:33061,172.16.16.11:33061,172.16.16.12:33061"
	##loose-group_replication_start_on_boot = OFF
	##loose-group_replication_bootstrap_group = OFF
	##loose-group_replication_exit_state_action = READ_ONLY
	##loose-group_replication_flow_control_mode = "DISABLED"
	##loose-group_replication_single_primary_mode = ON
	##loose-group_replication_communication_max_message_size = 10M
	##loose-group_replication_unreachable_majority_timeout = 30
	##loose-group_replication_member_expel_timeout = 5
	##loose-group_replication_autorejoin_tries = 288
	#
	#innodb settings  innodb设置
	transaction_isolation = REPEATABLE-READ
	innodb_buffer_pool_size = 8G
	innodb_buffer_pool_instances = 8
	innodb_data_file_path = ibdata1:2G;ibdata2:2G;ibdata3:2G;ibdata4:2G;ibdata5:16M:autoextend
	innodb_flush_log_at_trx_commit = 2 #MGR环境中由其他节点提供容错性，可不设置双1以提高本地节点性能
	innodb_log_buffer_size = 500M
	innodb_log_file_size = 2G #如果线上环境的TPS较高，建议加大至1G以上，如果压力不大可以调小
	innodb_log_files_in_group = 2
	innodb_max_undo_log_size = 4G
	innodb_thread_concurrency = 0
	innodb_read_io_threads = 48
	innodb_write_io_threads = 48
	innodb_commit_concurrency = 48
	# 根据您的服务器IOPS能力适当调整
	# 一般配普通SSD盘的话，可以调整到 10000 - 20000
	# 配置高端PCIe SSD卡的话，则可以调整的更高，比如 50000 - 80000
	innodb_io_capacity = 20000
	innodb_io_capacity_max = 50000
	innodb_open_files = 65535
	innodb_flush_method = O_DIRECT
	innodb_buffer_pool_dump_pct = 75
	#Innodb_io_capacity/innodb_buffer_pool_instances Innodb_io_capacity>innodb_lru_scan_depth*innodb_buffer_pool_instance
	innodb_lru_scan_depth = 4000
	#innodb_lock_wait_timeout = 10
	#innodb_rollback_on_timeout = 1
	innodb_print_all_deadlocks = 1
	innodb_online_alter_log_max_size = 1G
	innodb_print_ddl_logs = 1
	innodb_status_file = 1
	#注意: 开启 innodb_status_output & innodb_status_output_locks 后, 可能会导致log_error文件增长较快
	#innodb_status_output = 0
	innodb_status_output_locks = 1
	innodb_sort_buffer_size = 67108864
	innodb_adaptive_hash_index = OFF
	#提高索引统计信息精确度
	innodb_stats_persistent_sample_pages = 500
	 
	#innodb monitor settings   innodb监视器设置
	innodb_monitor_enable = "module_innodb"
	innodb_monitor_enable = "module_server"
	innodb_monitor_enable = "module_dml"
	innodb_monitor_enable = "module_ddl"
	innodb_monitor_enable = "module_trx"
	innodb_monitor_enable = "module_os"
	innodb_monitor_enable = "module_purge"
	innodb_monitor_enable = "module_log"
	innodb_monitor_enable = "module_lock"
	innodb_monitor_enable = "module_buffer"
	innodb_monitor_enable = "module_index"
	innodb_monitor_enable = "module_ibuf_system"
	innodb_monitor_enable = "module_buffer_page"
	#innodb_monitor_enable = "module_adaptive_hash"
	 
	#pfs settings #pfs设置
	performance_schema = 1
	##performance_schema_instrument = '%memory%=on'
	performance_schema_instrument = '%lock%=on'
	 
	[mysqldump]
	quick
	 
	 
	# Custom config should go here
	!includedir /etc/mysql/conf.d/
	```
5. 配置conf.d/mysql.cnf
	```conf
	#配置mysql.cnf
	vim /export/data/docker/mysql/conf/conf.d/mysql.cnf
	##############################
	[mysql]
	prompt = "\\u@\\d \\r:\\m:\\s>"
	no_auto_rehash
	loose-skip-binary-as-hex
	################################
	prompt = "\\u@\\d \\r:\\m:\\s>"   #设置命令行工具的提示符 默认为 mysql>
	no_auto_rehash                    #命令行工具中的自动命令补全功能
	loose-skip-binary-as-hex          #
	```
6. 详细配置my.cnf
	```conf
	#配置mysql my.cnf文件
	vim /usr/local/src/docker/mysql/config/my.cnf
	####################my.cnf##################
	[mysqld]
	pid-file        = /var/run/mysqld/mysqld.pid
	socket          = /var/run/mysqld/mysqld.sock
	datadir         = /var/lib/mysql
	secure-file-priv= NULL
	  
	#mysql服务端口号        
	prot = 3306
	#管理多因素身份认证功能 
	#mysql 8 默认 caching_sha2_password   mysql 5 默认 mysql_native_password
	authentication_policy=caching_sha2_password
	 
	 
	 
	#server级别字符集，服务器安装时指定的默认编码格式，不要人为定义，让系统自己定义
	character-set-server = utf8mb4
	#设置字段编码
	collation-server = utf8mb4_general_ci
	#设置初始化连接编码
	init_connect='SET NAMES utf8mb4'
	 
	 
	#设置大小写是否敏感的参数  0 区分大小写| 1 表明存储是小写，但是比较不区分大小写， 2 表名存储为给定的大小写但是比较是小写。unix\linux默认是0 windows默认是1 mac默认是2
	lower_case_table_names = 1
	#innodb使用后台线程处理数据页的读取IO（输入输出请求），根据cpu核数来更改默认是4
	innodb_read_io_threads = 4
	#数据库落盘脏页个数，配置压力和磁盘性能相关，如果过大，IO能力不足，则出现卡顿，默认是200单位是页，该参数设置大小取决于硬盘的IOPS，即每秒的输入输出量或读写次数。动态调整： set global innodb_io_capacity=2000;
	innodb_io_capacity = 400
	#定义innodb存储引擎的表数据和索引数据的最大内存缓冲区,看机器内存情况定
	#InnoDB缓存池缓存索引、行的数据、自适应哈希索引、插入缓存（Insert Buffer）、锁 还有其他的内部数据结构。（所以，如果数据库的数据量不大，并且没有快速增长，就不必为缓存池分配过多的内存，当为缓存池配置的内存比需要缓存的表和索引大很多也没什么必要，会造成资源浪费。）
	#a.很大的缓存池可能会有很多脏页，导致InnoDB在关闭的时候会消耗很长的时间，因为要把脏页写回到数据文件里
	#b.一个大的缓存池重启服务器可能也要比较长的时间用来预热缓冲池，当然Percona的Server有快速预热的功能可以节省很多时间。
	innodb_buffer_pool_size = 2G
	#每个日志文件的大小，综合大小到缓冲池大小的5%~100%，避免日志覆写上不必要的缓冲池刷新行为。注意一个大的日志文件大小会增加恢复进程所需要的时间
	innodb_log_file_size = 128M
	#独立表空间模式，每个数据库的没表表都会生成一个数据空间
	innodb_file_per_table = 1
	 
	 
	#此参数用来设置innodb线程的并发数，比如处理请求连接，默认值是0不限制，若要设置则与服务器cpu核心数相同或者是cpu核心数的2倍，合理修改会提升mysql的性能，最大是cpu核的两倍（常用设置），如果超过配置并发数则需要排队，这个值不宜太大，不然可能会导致线程之间锁争用严重，影响性能
	innodb_thread_concurrency=4
	 
	#innodb存储引擎下 Buffer Pool缓存大小，一般为屋里内存的60%-70%
	innodb_buffer_pool_size=30G
	 
	#innodb存储引擎下，行锁锁定时间，默认50s,根据公司业务定，没有标准值。如果一个事务在超过改时间后任然无法获取锁，那么该事务会被取消，并返回一个错误消息。如果系统有大量并发事务，并且经常出现锁等待超时的问题，那么可以调整该参数的值来降低锁等待时间，提高系统并发度。
	innodb_lock_wait_timeout=10
	 
	#如果设置为 1 ,InnoDB 会在每次提交后刷新(fsync)事务日志到磁盘上,这提供了完整的 ACID 行为.如果你愿意对事务安全折衷, 并且你正在运行一个小的食物, 你可以设置此值到 0 或者 2 来减少由事务日志引起的磁盘 I/O
	innodb_flush_log_at_trx_commit = 0
	#innodb_flush_log_at_trx_commit：是 InnoDB 引擎特有的，ib_logfile的刷新方式（ ib_logfile：记录的是redo log和undo log的信息）
	#取值:0/1/2
	#innodb_flush_log_at_trx_commit=0，表示每隔一秒把log buffer刷到文件系统中(os buffer)去，并且调用文件系统的“flush”操作将缓存刷新到磁盘上去。也就是说一秒之前的日志都保存在日志缓冲区，也就是内存上，如果机器宕掉，可能丢失1秒的事务数据。
	#innodb_flush_log_at_trx_commit=1，表示在每次事务提交的时候，都把log buffer刷到文件系统中(os buffer)去，并且调用文件系统的“flush”操作将缓存刷新到磁盘上去。这样的话，数据库对IO的要求就非常高了，如果底层的硬件提供的IOPS比较差，那么MySQL数据库的并发很快就会由于硬件IO的问题而无法提升。
	#innodb_flush_log_at_trx_commit=2，表示在每次事务提交的时候会把log buffer刷到文件系统中去，但并不会立即刷写到磁盘。如果只是MySQL数据库挂掉了，由于文件系统没有问题，那么对应的事务数据并没有丢失。只有在数据库所在的主机操作系统损坏或者突然掉电的情况下，数据库的事务数据可能丢失1秒之类的事务数据。这样的好处，减少了事务数据丢失的概率，而对底层硬件的IO要求也没有那么高(log buffer写到文件系统中，一般只是从log buffer的内存转移的文件系统的内存缓存中，对底层IO没有压力)。
	 
	 
	sync_binlog = 1
	#sync_binlog：是MySQL 的二进制日志（binary log）同步到磁盘的频率。
	#取值：0-N
	#sync_binlog=0，当事务提交之后，MySQL不做fsync之类的磁盘同步指令刷新binlog_cache中的信息到磁盘，而让Filesystem自行决定什么时候来做同步，或者cache满了之后才同步到磁盘。这个是性能最好的。
	#sync_binlog=1，当每进行1次事务提交之后，MySQL将进行一次fsync之类的磁盘同步指令来将binlog_cache中的数据强制写入磁盘。
	#sync_binlog=n，当每进行n次事务提交之后，MySQL将进行一次fsync之类的磁盘同步指令来将binlog_cache中的数据强制写入磁盘。
	#注：大多数情况下，对数据的一致性并没有很严格的要求，所以并不会把 sync_binlog 配置成 1. 为了追求高并发，提升性能，可以设置为 100 或直接用 0. 
	而和 innodb_flush_log_at_trx_commit 一样，对于支付服务这样的应用，还是比较推荐 sync_binlog = 1.
	 
	 
	 
	#索引缓冲区大小，增加他可得到更好的索引处理性能，如果是以InnoDB引擎为主的DB专用于MyISAM引擎的可以设置较小，8MB已足够，如果是MyISAM引擎为主可以设置较大，但不能超过4G，强烈不建议MyISAM引擎默认都是InnoDB引擎。注意：该参数值过大反而会使服务器整体效率降低
	key_buffer_size = 512M
	 
	#控制是否允许从客户端加载数据（大批量数据加载优化）到MySQL服务器。默认情况下，此选项处于禁用状态 on 禁用 off开启。当启用local-infile选项后，客户端可以使用LOAD DATA INFILE语句将本地文件中的数据加载到MySQL服务器中.
	local-infile = on
	 
	#指定链接空闲多长时间断开
	lock_wait_timeout = 3600
	 
	 
	#当此值设置为10时，意味着如果某一客户端尝试连接此MySQL服务器，但是失败（如密码错误等等）10次，则MySQL会无条件强制阻止此客户端连接。
	#如果希望重置此计数器的值，则必须重启MySQL服务器或者在mysql服务执行命令 FLUSH HOSTS;
	max_connect_errors = 10
	 
	 
	#表描述符的缓存大小，打卡一个标后会把这个表的文件描述缓存下来 动态查看 show global variables like 'table_open_cache'  动态设置 set global table_open_cache = 2048; （重启生效）
	table_open_cache = 20000
	#table open cache的值可以通过 opened_tables(打开的所有表数量)和open_tables（打开后缓存中的标数量）来判断值是否达到瓶颈，当缓存中的值open_tables 临近到了 table_open_cache 值的时候
	#说明表缓存池快要满了 但 Opened_tables 还在一直有新的增长 这说明你还有很多未被缓存的表
	#这时可以适当增加 table_open_cache 的大小
	 
	#对 InnoDB 数据字典缓存中打开的表实例数量进行软限制。即，如果打开的表实例的数量超过table_definition_cache 设置，则 LRU 机制标记表实例并最终从数据字典缓存中删除。该限制有助于缓解大量内存被极少使用的表实例占用的情况，注意：具有缓存元数据的表实例数可能高于table_definition_cache 定义的限制，因为带有外键关系的 InnoDB 系统表实例和具有父子关系的表实例不会放在 LRU 列表上，无法通过从内存中逐出这些表实例来减
	table_definition_cache = 2000
	 
	 
	#每个连接线程被创建时,MySQL给它分配的内存大小.当MySQL创建一个新的连接线程时,需要给它分配一定大小的内存堆栈空间,以便存放客户端的请求的Query及自身的各种状态和处理信息.
	#查看连接线程相关的系统变量的设置值： show variables like 'thread%';
	thread_stack = 512k
	 
	#每个需要排序的线程分配该大小的一个缓冲区。增加该值可以加速ORDER BY或GROUP BY操作。它是一个connection级的参数，在每个connection(session)第一次需要使用，这个buffer的时候，一次性分配设置的内存。数值也不是越大越好，由于是conection级参数过大的设置+高并发可能会好近系统内存资源，例如500个链接将会消耗 500*sort_buffer_size(2M)=1G
	sort_buffer_size = 2M
	#用于表关联缓存，和sort_buffer_size一样，该参数对应的分配内存也是每个链接独享。调大后可以避免多次的内表扫描，从而提高性能。也就是说，当mysql的join有使用缓存块嵌套循环连接（Block Nested-Loop Join），调大他的变量才会优化语句速度（有意义），其他时候这个变量毫无意义。默认值是256k,对于稍复杂的sql显然不够用。这个内存是回话级别分配，如果设置不好容易导致因无法分配内存而导致宕机问题。
	join_buffer_size=2M
	 
	#线程池缓存大小， 当客户端断开连接后 将当前线程缓存起来 当在接到新的连接请求时快速响应 无需创建新的线程.当 Threads_cached 越来越少 但 Threads_connected 始终不降 且 Threads_created 持续升高
	这时可适当增加 thread_cache_size 的大小
	#show global status like 'Threads_%'
	#Threads_cached    : 当前线程池中缓存有多少空闲线程
	#Threads_connected : 当前的连接数 ( 也就是线程数 )
	#Threads_created   : 已经创建的线程总数
	#Threads_running   : 当前激活的线程数 ( Threads_connected 中的线程有些可能处于休眠状态 )
	thread_cache_size = 256
	 
	#关闭一个交互链接之前所需要等待的秒数，它类似跳板机，过了多久没操作就会踢掉你，需要重新连接
	interactive_timeout = 600
	#关闭一个非交互链接之前所需要等待的秒数，如果有事务or存储过程需要，这个值可以调大一些
	wait_timeout = 600
	#默认值都是28800，可随实际情况进行调优，配置这两个参数可以减轻内存的压力。长连接的应用，为了不去反复的回收和分配资源，降低额外的开销。一般我们会将wait_timeout设定比较小，interactive_timeout要和应用开发人员沟通长链接的应用是否很多。如果他需要长链接，那么这个值可以不需要调整。动态查询如下：
	#select @@interactive_timeout;
	#select @@wait_timeout;
	#show processlist，如果经常发现MYSQL中有大量的Sleep进程，则需要修改wait-timeout值了，不过已实际为准。
	 
	#mysql允许的最大进程连接数 数据库经常出现“Too Many COnnection”错误提示，则需要增大数值
	max_connections = 6000
	#mysql 用户的最大链接数量，剩余链接数用于DBA管理
	max_user_connections = 5800
	# mysql能够暂存的链接数量，如果mysql的链接达到max_connection时，新的请求将会被存在堆栈中，等待某一链接释放资源，该堆栈数量即back_log,如果等待连接的数量唱过back_log将会被拒绝
	back_log = 1024
	 
	#默认存储引擎
	default-storage-engine=InnoDB
	 
	#临时表的内存缓存大小
	tmp_table_size = 32M
	#临时表的最大值，每个线程都要分配。（实际起限制作用的是tmp_table_size和max_heap_table_size的最小值）如果每个内存临时表超出了限制，mysql就会自动地把它转化为基于磁盘的MYISAM表存储在指定的tmpdir目录下 ，默认目录 /tmp/  动态查目录： show variables like "tmpdir"
	max_heap_table_size = 512M
	#优化查询语句的时候，要避免使用临时表，如果实在避免不了的话，要保证这些临时表是存在内存中的。如果需要的话并且你有很多group by语句，并且你有很多内存，增大tmp_table_size(和max_heap_table_size)的值。这个变量不适用与用户创建的内存表(memory table).
	#你可以比较内部基于磁盘的临时表的总数和创建在内存中的临时表的总数(Created_tmp_disk_tables和Created_tmp_tables)，一般的比例关系是:
	#Created_tmp_disk_tables/Created_tmp_tables<5%
	#max_heap_table_size
	#这个变量定义了用户可以创建的内存表(memory table)的大小.这个值用来计算内存表的最大行数值。这个变量支持动态改变，即set @max_heap_table_size=#  ,但是对于已经存在的内存表就没有什么用了，除非这个表被重新创建(create table)或者修改(alter table)或者truncate table。服务重启也会设置已经存在的内存表为全局max_heap_table_size的值。
	#这个变量和tmp_table_size一起限制了内部内存表的大小。
	 
	#log settings
	log_error = /var/log/mysql/mysql-error.log
	#显示日志中的时间参数
	log_timestamps = SYSTEM
	 
	#密码加密方式
	default_authentication_plugin = cahing_sha2_password
	#服务能处理的请求包最大大小如果过小可能会出现“信息包过大”错误
	max_allowed_packet = 512M
	#设置最大包，限制server接受的数据包大小，避免出现超长sql的执行问题，默认值16M
	slave_max_allowed_packet = 512M
	 
	#打开的文件描述符限制，控制mysqld进程能使用的最大文件描述（FD）数量，最小值1024
	open_files_limit = 65536
	 
	#配置时区
	default-time_zone = '+8:00'   
	 
	#通用查询日志是否开启 默认关闭 OFF关闭 ON开启
	general_log=OFF
	#查询日志地址
	general_log_file=/var/log/mysql/query/mysql_general.log
	 
	#开启二进制日志 正常情况必须开启 ON开启 OFF关闭
	log-bin=ON
	#binlog的日志存放地址
	log_bin_basename=/var/log/mysql/binlog/binlog
	# mysql binlog日志文件保存的过期时间，过期后自动删除 一般不启用，主从中更加不能启用
	#expire_logs_days = 5
	#用于标识数据库实例，防止在链试主从，多主多从的拓扑中导致sql语句的无线循环 具有唯一性
	server_id = 1
	#二进制文件大小
	binlog_expire_logs_seconds = 604800
	#事务级别的参数，指定存储整个事务生成的binlog event的内存大小，对于大事务来讲很可能会超过这个参数的设置，则需要开启binlog临时文件用于存储 1048576
	binlog_cache_size=10480
	#二进制非事务语句的缓存大小
	binlog_stmt_cache_size=1024
	#Mysql二进制日志缓存参数：
	#binlog_cache_size     //事务缓存大小
	#binlog_cahce_use      //事务缓存使用次数
	#binblog_cache_disk_use  //事务缓存磁盘使用次数(内存缓存设置过小不够用时)
	#binlog_stmt_cache_size     //非事务语句缓存大小
	#binlog_stmt_cache_use    //非事务语句缓存使用次数
	#binlog_stmt_cache_disk_use  //非事务语句磁盘缓存使用次数
	#MySQL 的二进制日志（binary log）同步到磁盘的频率（刷新二进制日志到磁盘），默认是0，意味着mysql并不刷新，由操作系统自己决定什么时候刷新缓存到持久化设置，如果这个值比0大，它指定了两次刷新到磁盘的动作之间间隔多少次二进制日志写操作。
	 
	 
	sync_binlog=100
	#sync_binlog=0，当事务提交之后，MySQL不做fsync之类的磁盘同步指令刷新binlog_cache中的信息到磁盘，而让Filesystem自行决定什么时候来做同步，或者cache满了之后才同步到磁盘。这个是性能最好的。
	#sync_binlog=1，当每进行1次事务提交之后，MySQL将进行一次fsync之类的磁盘同步指令来将binlog_cache中的数据强制写入磁盘。
	#sync_binlog=n，当每进行n次事务提交之后，MySQL将进行一次fsync之类的磁盘同步指令来将inlog_cache中的数据强制写入磁盘。
	#如果没有设置它为1，那么崩溃后可能导致二进制日志没有同步事务数据，有可能binlog中最后的语句丢失。要想防止这种情况，你可以使用sync_binlog全局变量(1是最安全的值，但也是最慢的)，使binlog在每N次binlog写入后与硬盘 同步。即使sync_binlog设置为1,出现崩溃时，也有可能表内容和binlog内容之间存在不一致性。如果使用InnoDB表，MySQL服务器 处理COMMIT语句，它将整个事务写入binlog并将事务提交到InnoDB中。如果在两次操作之间出现崩溃，重启时，事务被InnoDB回滚，但仍 然存在binlog中。可以用--innodb-safe-binlog选项来增加InnoDB表内容和binlog之间的一致性。(注释：在MySQL 5.1中不需要--innodb-safe-binlog；由于引入了XA事务支持，该选项作废了），该选项可以提供更大程度的安全，使每个事务的 binlog(sync_binlog =1)和(默认情况为真)InnoDB日志与硬盘同步，该选项的效果是崩溃后重启时，在滚回事务后，MySQL服务器从binlog剪切回滚的 InnoDB事务。这样可以确保binlog反馈InnoDB表的确切数据等，并使从服务器保持与主服务器保持同步(不接收 回滚的语句)。
	#注：大多数情况下，对数据的一致性并没有很严格的要求，所以并不会把 sync_binlog 配置成 1. 为了追求高并发，提升性能，可以设置为 100 或直接用 0。而和 innodb_flush_log_at_trx_commit 一样，对于支付服务这样的应用，还是比较推荐 sync_binlog = 1.
	 
	 
	#二进制启用后，变量则启用，控制是否可以信任存储函数创建者，不会创建写入二进制日志引起不安全时间的存储函数，默认值为0，用户不得创建或修改存储函数，除非create routine 或 alter routinet特权之外的super权限，设置为0还强制使用delerministic特性或reads sql data 或 no sql 特性声明函数限制，如果变量为1，则不会对创建存储函数实施这些限制。变量也适用于触发器的创建
	log_bin_trust_function_creators = 1
	 
	#开启慢查询日志
	show_query_log=ON
	#慢查询日志文件存放地址
	show_query_log_file = /var/log/mysql/mysql_show_query.log
	#慢查询数据库时间为5秒
	show_query_time = 5
	# 检索的行数必须达到此值才可被记为慢查询
	#min_examined_row_limit = 100
	#控制未使用索引的查询是否写入慢查询日志 ON 开启 OFF关闭 ，启用不以为不适用索引，使用完整索引扫描的查询使用索引但会诶记录，因为索引不会限制行数
	log_queries_not_using_indexes=ON
	#set long_query_time=1; 动态设置慢查询时间1秒
	#set global slow_query_log=on; #动态开启慢查询日志
	#show global status like 'slow_queries'; #显示慢查询次数
	#show variables like 'long_query_time'; #显示慢查询时间
	#show variables like 'show_query_log';  #显示慢查询日志是否开启
	#show variables like '%query%';  #显示慢查询日志信息
	 
	 
	# 作为从库时生效,从库复制中如何有慢sql也将被记录
	#log_slow_slave_statements = 1
	#主从主库配置
	#server-id = 1
	#log-bin=mysql-bin
	#binlog-ignore-db = mysql,information_schema #忽略写入binlog日志的库
	#log-slave-updates = 1 #从库的写操作记录到
	#bin-logexpire_logs_days = 30 #日志存在的天数，30天
	#auto-increment-increment = 2 #字段变化增量值
	#auto-increment-offset = 1 #初始字段ID为1，从库为2
	#slave-skip-errors = all    #跳过所有主从复制中，报错的语句
	 
	#主从从库配置
	#[mysqld]
	#server-id = 2
	#log-bin=mysql-bin
	#binlog-ignore-db = mysql,information_schema
	#log-slave-updates = 1 
	#expire_logs_days = 30 
	#auto-increment-increment = 2
	#auto-increment-offset = 2
	#slave-skip-errors = all
	 
	
	#skip-name-resolve
	#禁止 MySQL 对外部连接进行 DNS 解析，使用这一选项可以消除 MySQL 进行 DNS 解析的时间。但需要注意，如果开启该选项，则所有远程主机连接授权都要使用 IP 地址方式，否则 MySQL 将无法正常处理连接请求！
	 
	# Custom config should go here 调用/ect/mysql/conf.d下的配置文件
	!includedir /etc/mysql/conf.d/
	```
7. 实际配置
	   vim /export/data/docker/mysql/conf/my.cnf
	   进入之后先用:set paste  防止粘贴注释时注释给所有信息添加注释。
	```conf
	[mysqld]
	pid-file        = /var/run/mysqld/mysqld.pid
	socket          = /var/run/mysqld/mysqld.sock
	datadir         = /var/lib/mysql
	secure-file-priv= NULL
	 
	#管理多因素身份认证功能
	authentication_policy=caching_sha2_password
	 
	 
	 
	#server级别字符集，服务器安装时指定的默认编码格式，不要人为定义，让系统自己定义
	character-set-server = utf8mb4
	#设置字段编码
	collation-server = utf8mb4_general_ci
	#设置初始化连接编码SET NAMES utf8mb4
	init_connect='SET NAMES utf8mb4'
	 
	 
	#不区分数据大小写
	lower_case_table_names = 1
	#innodb使用后台线程处理数据页的读取IO（输入输出请求），根据cpu核数来更改默认是4
	innodb_read_io_threads = 4
	#数据库落盘脏页个数
	innodb_io_capacity = 400
	 
	#定义innodb存储引擎的表数据和索引数据的最大内存缓冲区,看机器内存情况定
	innodb_buffer_pool_size = 2G
	#每个日志文件的大小，综合大小到缓冲池大小的5%~100%，避免日志覆写上不必要的缓冲池刷新行为。注意一个大的日志文件大小会增加恢复进程所需要的时间
	innodb_log_file_size = 128M
	#独立表空间模式，每个数据库的没表表都会生成一个数据空间
	innodb_file_per_table = 1
	 
	 
	#设置innodb线程的并发数
	innodb_thread_concurrency=4
	 
	#innodb存储引擎下 Buffer Pool缓存大小，一般为物理内存的60%-70%存的60%-70%
	innodb_buffer_pool_size=2G
	 
	#innodb存储引擎下，行锁锁定时间
	innodb_lock_wait_timeout=10
	 
	#每次事务提交的时候会把log buffer刷到文件系统中去，但并不会立即刷写到磁盘。如果只是MySQL数据库挂掉了，由于文件系统没有问题数据不会丢失，减少由事务日志引起的磁盘 I/O
	innodb_flush_log_at_trx_commit = 2
	 
	 
	 
	#索引缓冲区大小
	key_buffer_size = 512M
	 
	#禁用 local-infile选项
	local-infile = on
	 
	#指定链接空闲多长时间断开
	lock_wait_timeout = 3600
	 
	 
	#链接十次数据库服务不正常，会锁住IP安全设置
	max_connect_errors = 10
	 
	 
	#表描述符的缓存大小
	table_open_cache = 20000
	 
	#数据字典缓存中打开的表数量软限制
	table_definition_cache = 2000
	 
	#每个线程的内存大小
	thread_stack = 512k
	 
	 
	#每个需要排序的线程分配该大小的一个缓冲空间。增加该值可以加速ORDER BY或GROUP BY操作。不宜过大，占内存
	sort_buffer_size = 2M
	 
	#用于表关联缓存空间（缓存块嵌套循环连接） 可以避免多次的内表扫描，从而提高性能
	join_buffer_size=2M
	 
	 
	 
	#线程池缓存大小
	thread_cache_size = 256
	 
	#关闭一个交互链接之前所需要等待的时间秒
	interactive_timeout = 600
	#关闭一个非交互链接之前所需要等待的时间秒
	wait_timeout = 600
	 
	#最大进程连接数
	max_connections = 6000
	#用户的最大链接数量，剩余链接数用于DBA管理
	max_user_connections = 5800
	# 暂存的等待的链接数量
	back_log = 1024
	 
	#默认存储引擎 5.5以上默认就是InnoDB
	default-storage-engine=InnoDB
	 
	#临时表的内存缓存大小
	tmp_table_size = 32M
	 
	#临时表的最大值
	max_heap_table_size = 512M
	 
	 
	 
	#log settings 错误日志存放地址
	#log_error = /var/log/mysql/error/mysql-error.log
	#通用查询日志是否开启 默认关闭 OFF关闭 ON开启
	#general_log=OFF
	#查询日志地址
	#general_log_file = /var/log/mysql/query/mysql_general.log
	 
	 
	 
	 
	#开启二进制日志 正常情况必须开启 ON开启 OFF关闭
	log-bin=ON
	#binlog的日志存放地址
	#log_bin_basename=/var/log/mysql/binlog/binlog
	# mysql binlog日志文件保存的过期时间，过期后自动删除 一般不启用，主从中更加不能启用
	#expire_logs_days = 5
	 
	#显示日志中的时间参数
	log_timestamps = SYSTEM
	 
	#配置时区
	default-time_zone = '+8:00'   
	 
	#密码加密方式
	default_authentication_plugin = cahing_sha2_password
	 
	#服务能处理的请求包最大大小
	max_allowed_packet = 512M
	 
	#设置最大包，限制server接受的数据包大小
	slave_max_allowed_packet = 512M
	 
	#打开的文件描述符限制
	open_files_limit = 65536
	 
	 
	 
	#标识数据库
	server_id = 1
	#二进制文件大小
	binlog_expire_logs_seconds = 604800
	 
	#存储整个事务生成的binlog event的内存大小
	binlog_cache_size=10480
	#二进制非事务语句的缓存大小
	binlog_stmt_cache_size=1024
	 
	#sync_binlog：是MySQL 的二进制日志（binary log）同步到磁盘的频率。当每进行1次事务提交之后，MySQL将进行一次fsync之类的磁盘同步指令来将binlog_cache中的数据强制写入磁盘。保证数据不丢失。
	sync_binlog = 1
	 
	 
	#二进制启用后，变量则启用，控制是否可以信任存储函数创建者，1 不会对创建存储函数实施做控制
	log_bin_trust_function_creators = 1
	 
	 
	# 检索的行数必须达到此值才可被记为慢查询
	#min_examined_row_limit = 100
	 
	# 作为从库时生效,从库复制中如何有慢sql也将被记录
	#log_slow_slave_statements = 1
	 
	 
	# Custom config should go here 调用/ect/mysql/conf.d下的配置文件
	!includedir /etc/mysql/conf.d/
	```
8. 再次运行mysql8
	```shell
	docker rm -f mysql8
	#运行mysql8容器并关联本地文件
	docker run \
	-p 3306:3306 \
	--name mysql8 \
	-e MYSQL_ROOT_PASSWORD=123456 \
	-e TZ=Asia/Shanghai \
	-v /export/data/docker/mysql/data:/var/lib/mysql \
	-v /export/data/docker/mysql/logs:/var/log/mysql \
	--privileged=true \
	--restart=always \
	-d mysql:8.0 \
	--lower_case_table_names=1
	
	# 每一行作用
	docker run \
	-p 3306:3306 \                                        #端口号
	--name mysql8 \                                       #容器名称
	-e MYSQL_ROOT_PASSWORD=123456 \                       #root密码
	-e TZ=Asia/Shanghai \                                 #容器时区
	-v /export/data/docker/mysql/conf:/etc/mysql \        #mysql配置文件引用
	-v /export/data/docker/mysql/data:/var/lib/mysql \    #mysql数据存储引用
	-v /export/data/docker/mysql/logs:/var/log/mysql \    #mysql日志引用
	--privileged=true \                                   #赋予这个容器和主机一样的权限
	--restart=always \                                    #开机启动容器
	-d mysql:8.0 \                                        #调用的镜像
	--lower_case_table_names=1                            #mysql表名称不区分大小写，必须放最后
	#区分大小写是对数据库进行操作，不放最后会导致报错，容器命令无法识别
	```
9. 配置数据库外部访问
	```sh
	#关闭防火墙
	systemctl stop firewalld
	systemctl disable firewalld
	 
	#进入mysql8容器
	docker exec -it mysql8 /bin/bash
	进入mysql数据库
	mysql -u root -p
	123456
	 
	#进入mysql数据库下
	use mysql;
	#查看用户信息 看root的host是不是% 所有地址都可以访问，如果不是则需要改一下
	select host,user from user;
	#修改host
	update user set host='%' where user='root';
	#刷新mysql配置
	flush privileges;
	#修改root权限开启外部访问
	#alter user root@'%' identified with mysql_native_password by '密码'；
	alter user root@'%' identified with mysql_native_password by '123456';
	#刷新mysql配置
	flush privileges;
	```
10. 开启慢查询日志
	```sh
	#进入mysql里面进行配置
	#查看慢查询配置信息
	show global variables like '%query%';
	#slow_query_log   控制开启关闭（OFF关闭，ON开启）
	#slow_query_log_file 慢查询日志存放地址
	#long_query_time 执行多长时间的sql算是慢查询  单位秒
	#配置sql执行5秒以上时间算是慢查询
	set global long_query_time=5;
	#控制未使用索引的查询是否写入慢查询日志 ON 开启 OFF关闭 ，启用不以为不适用索引，使用完整索引扫描的查询使用索引但会诶记录，因为索引不会限制行数
	set global log_queries_not_using_indexes=on;
	#开启慢查询日志
	set global slow_query_log='ON';
	#开启之后如果有sql执行超过五秒的都会存放在 /var/lib/mysql/慢查询文件.log下
	 
	#慢查询日志的存储格式
	# Time: 231009 10:59:03			执行时间
	# User@Host: root[root] @ localhost [127.0.0.1] 执行SQL的主机信息
	# Query_time: 19.242655  Lock_time: 0.000000 Rows_sent: 11  Rows_examined: 3761986	
	#执行的信息  执行时间 发送行数 扫描行数 ↑
	```
11. 开启查询语句日志记录
	```sh
	#查看查询日志信息 是否开启 和日志地址
	show variables like '%general%';
	#开启查询日志记录 OFF关闭  ON开启
	set global general_log='ON';
	#修改存储地址 文件需要有mysql权限   可以不修改直接查这个文件
	set global general_log_file='/var/lib/mysql/general_log.log'
	```


## MySQL

MySQL8.0版本在Ubuntu系统中安装

1. 如果安装过MySQL，需要卸载仓库信息
```shell
apt remove -y mysql-client=5.7* mysql-community-server=5.7*

dpkg -l | grep mysql | awk '{print $2}' | xargs dpkg -P
```
2. 更新apt仓库信息
```shell
apt update
```
3. 安装mysql
```shell
apt install -y mysql-server
```
4. 启动mysql
```shell
/etc/init.d/mysql start   #启动
/etc/init.d/mysql stop    #停止
/etc/init.d/mysql status  #状态
```
5. 登录mysql设置密码
```shell
mysql
```
6. 设置密码
```shell
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';
```
7. 退出mysql控制台
```shell
exit
```
8. 对mysql进行初始化
```shell
mysql_secure_installation
```
输入密码；
是否开启密码验证插件，需要输入y回车，不需要直接回车；（直接回车）
是否更改root密码，需要输入y回车，不需要直接回车；（直接回车）
是否移除匿名用户，移除输入y回车，不移除直接回车；（输入y回车）
是否禁止root用户远程登录，禁止输入y回车，不禁止直接回车；（直接回车）
是否移除自带的测试数据库，移除输入y回车，不移除直接回车；（直接回车）
是否刷新权限，刷新输入y回车，不需要直接回车；（输入y回车）

9. 重新登录mysql（用更改后的密码）
```shell
mysql -uroot -p123456
```

## Java

1. 下载JDK软件-[网址](https://www.oracle.com/cn/java/technologies/downloads)，找到X64 Compressed Archive
2. 登录Linux系统，切换到root用户
3. 上传JDK安装包
4. 创建文件夹,用来部署JDK,将JDK和Tomcat都安装部署到:/export/server 内
```shell
mkdir -p /export/server
```
5. 解压缩JDK安装文件
```shell
tar -zxvf jdk-xxx-linux-x64.tar.gz -C /export/server
```
6. 配置JDK的软链接
```shell
ln -s /export/server/jdkxxx /export/server/jdk
```
7. 配置JAVA_HOME环境变量,以及将$JAVA_HOME/bin文件夹加入PATH环境变量中
```shell
vim /etc/profile
# 编辑/etc/profile文件
export JAVA_HOME=/export/server/jdk
export PATH=$PATH:$JAVA_HOME/bin
```
8. 生效环境变量
```shell
source /etc/profile
```
9. 配置java执行程序的软链接
```shell
# 删除系统自带的java程序
rm -f /usr/bin/java
# 软链接到自己安装的java程序
ln -s /export/server/jdk/bin/java /usr/bin/java
```

## Tomcat

tomcat建议使用非root用户安装并启动，可以创建一个用户tomcat用以部署

前置：[[Linux#Java安装配置|Java环境配置]]

1. 首先,放行tomcat需要使用的8080端口的外部访问权限

> CentOS系統默认开启了防火墙,阻止外部网络流量访问系统内部，所以，如果想要Tomcat可以正常使用，需要对Tomcat默认使用的8080端口进行放行，放行有两种操作方式:
> 第一个：关闭防火墙（推荐）
> 第二个配置防火墙规则,放行端口 

```shell
# 方式一:关闭防火墙
systemctl stop firewalld        # 关闭防火墙
systemctl disable firewalld     # 停止防火墙开机自启

#方式二:放行8080端口的外部访问
firewall-cmd -- add-port=8080/tcp -- permanent
# -- add-port=8080/tcp表示放行8080端口的tcp访问, -- permanent表示永久生效
firewall-cmd -- reload    # 重新载入防火墙规则使其生效
```
2. 以root用户操作,创建tomcat用户
```shell
# 使用root用户操作
useradd tomcat
# 可选,为tomcat用户配置密码
passwd tomcat
```
3. 上传或下载Tomcat安装包-[链接]()
```shell
# 使用root用户操作
wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.0.27/bin/apache-tomcat-10.0.27.tar.gz
# 如果出现https相关错误，可以使用--no-check-certificate选项
wget --no-check-certificate https://dlcdn.apache.org/tomcat/tomcat-10/v10.0.27/bin/apache-tomcat-10.0.27.tar.gz
```
4. 解压Tomcat安装包
```shell
# 切换root用户操作
cd /home/tomcat/
tar -zxvf apache-tomcat-10.0.27.tar.gz -C /export/server
```
5. 创建Tomcat软链接
```shell
ln -s /export/server/apache-tomcat-10.0.27 /export/server/tomcat
```
6. 修改tomcat安装目录权限
```shell
# 切换root用户操作
sudo su - root
chown -R tomcat:tomcat /export/server/*tomcat*
```
7. 切换到tomcat用户
```shell
su - tomcat
```
8. 启动tomcat
```shell
/export/server/tomcat/bin/startup.sh
```
9. tomcat启动在8080端口，可以检查是否正常启动成功
```
ssh 
```

## Nginx

切换到root身份，执行下列命令

### centos安装nginx

1. 安装yum依赖程序
```shell
# root执行
yum install -y yum-utils
```
2. 手动配置Nginx仓库
```shell
vim /etc/yum.repos.d/nginx.repo

[nginx-stable]
name=nginx stable repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=1
enabled=1
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true

[nginx-mainline]
name=nginx mainline repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=1
enabled=0
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true
```

3. 通过yum安装最新稳定版的nginx
```shell
yum install -y nginx
```

4. 启动
```shell
systemctl start nginx       # 启动
systemctl stop nginx        # 停止
systemctl status nginx      # 运行状态
systemctl enable nginx      # 开机自启
systemctl disable nginx     # 关闭开机自启
```

5. 配置防火墙放行
```shell
systemctl stop firewalld       # 关闭
systemctl disable firewalld    # 关闭开机自启
```

6. 访问默认网页：通过在Web浏览器中输入服务器IP地址或者localhost（本机）来访问Nginx默认的欢迎页面。

### ubuntu安装nginx

Nginx文件位置
- /usr/sbin/nginx：主程序
- /etc/nginx：存放配置文件
- /usr/share/nginx：存放静态文件
- /var/log/nginx：存放日志

1. 安装Nginx：打开终端并输入以下命令来安装Nginx。
```shell
sudo apt update
sudo apt install nginx
```

2. 启动并检查Nginx的状态。
```shell
service nginx start               # 启动nginx
service nginx reload              # 重新加载nginx配置文件

nginx -s reopen                   # 重启nginx
nginx -s stop                     # 停止nginx
systemctl status nginx
```
如果显示"active (running)"表示Nginx已经正常运行了。

3. 访问默认网页：通过在Web浏览器中输入服务器IP地址或者localhost（本机）来访问Nginx默认的欢迎页面。

4. Nginx的主要配置文件位于/etc/nginx/nginx.conf路径下。

5. 重新加载Nginx配置：当你对Nginx配置文件进行更改后，需要重新加载配置才能生效。使用以下命令来完成此任务。
```shell
sudo systemctl reload nginx
```

6. 设置Nginx为系统服务：将Nginx添加到系统服务列表中，这样每次系统启动时都会自动启动Nginx。
```shell
sudo systemctl enable nginx
```

7. /etc/nginx/sites-available/目录下的配置文件来创建自定义站点、反向代理等。然后使用以下命令来启用相应的配置文件。
```shell
sudo ln -s /etc/nginx/sites-available/your_config_file /etc/nginx/sites-enabled/
```

8. 测试Nginx配置：使用以下命令来检查Nginx配置文件语法错误。
```shell
sudo nginx -t
```

9. 重启Nginx服务：如果你对Nginx进行了任何更改，最好重新启动Nginx服务以使更改生效。
```shell
sudo service nginx restart
```

## 集群化前置

1. [[Linux#01 VMware虚拟机安装|创建一个虚拟机]]
2. 克隆虚拟机
3. [[Linux#主机名|更改主机名]]（每一台服务器都执行）
4. [[Linux#ssh|ssh配置]]（每一台服务器都执行）
5. [[Linux#Java|Java环境配置]]（每一台服务器都执行）
6. 关闭防火墙和SELinux（每一台服务器都执行）
```shell
# 关闭防火墙
systemctl stop firewalld
systemctl disable firewalld

# 关闭selinux
vim /etc/sysconfig/selinux
# 将SELINUX=enforcing改为
SELINUX=disabled
# 保存退出后，重启虚拟机即可
```


```
ssh node1@192.168.220.131
hostnamectl set-hostname node2
vim /etc/netplan/00-installer-config.yaml
192.168.220.131 node1
192.168.220.132 node2
192.168.220.133 node3
```

```shell
	mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
	wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo
	nameserver 202.96.134.133
	nameserver 202.96.128.166
	vim /etc/resolv.conf
	vi /etc/sysconfig/network-scripts/ifcfg-ens33
	
	IPADDR="192.168.147.128"
	NETMASK="255.255.255.0"
	GATEWAY="192.168.147.1"
	
	GATEWAY=192.168.220.2
	IPADDR=192.168.220.100
	
	IPADDR="192.168.1.160"
	NETMASK="255.255.255.0"
	GATEWAY="192.168.1.1"
	DNS1="223.5.5.5"
	DNS2="8.8.8.8"
	git@192.168.220.100:root/git-test.git
```

## ZooKeeper

1. [[Linux#集群化前置|集群化前置]]
2. 【node1】上传或下载ZooKeeper安装包，并解压
```shell
# 上传 
rz
# 下载
wget

# 确保下列目录存在，不存在就创建
mkdir -p /export/servers
# 解压
tar -zxvf zookeeper-x.x.x.tar.gz
```
3. 【node1】创建软连接
```shell
ln -s /export/servers/zookeeper-x.x.x /export/servers/zookeeper
```
4. 【node1】修改zoo.cfg配置文件
```sh
vim /export/servers/zookeeper/conf/zoo.cfg

#
tickTime=2000
#zookeeper数据存储目录
dataDir=/export/servers/zookeeper/data
clientPort=2181
initLimit=5
syncLimit=2
server.1=node1:2888:3888
server.2=node2:2888:3888
server.3=node3:2888:3888
```
5. 【node1】配置myid
```sh
# 创建zookeeper的数据目录存储
mkdir /export/servers/zookeeper/data

# 创建文件，并填入1
vim /export/servers/zookeeper/data/myid
# 填入1即可
```
6. 【node1】创建logs文件夹，并配置log文件
```sh
mkdir /export/servers/zookeeper/logs
cd /export/servers/zookeeper/logs
touch zookeeper.log

vim /export/servers/zookeeper/conf/log4j.properties
# 修改以下内容

zookeeper.log.dir=/export/servers/zookeeper/logs
zookeeper.tracelog.dir=/export/servers/zookeeper/logs
```
7. 【node2和node3】创建servers文件夹
```sh
mkdir -p /export/servers
```
8. 【node1】将zookeeper复制到node2和node3
```sh
cd /export/servers

scp -r zookeeper-x.x.x node2:$PWD
scp -r zookeeper-x.x.x node2:$PWD
```
9. 【node2和node3】
```sh
# 创建软链接
ln -s /export/servers/zookeeper-x.x.x /export/server/zookeeper

# node2就填入2，node3就填入3
vim /export/servers/zookeeper/data/myid
```
10. 【node1、node2和node3】启动zookeeper
```sh
zkServer.sh start
```
11. 【node1、node2和node3】检查zookeeper
```sh
jps
# 结果中找到有：QuorumPeeMain进程即可
```
12. 【node1】验证zookeeper
```sh
/export/servers/zookeeper/zkCli.sh

# 进入到zookeeper控制台后，执行
ls /
# 如无报错则配置成功
```

## Hadoop

### 1. Hadoop 作用

Hadoop HDFS 提供分布式海量数据存储能力
Hadoop YARN 提供分布式集群资源管理能力
Hadoop MapReduce 提供分布式海量数据计算能力

### 2. Hadoop 生态

Hadoop生态体系中总共会出现如下进程角色:

1. Hadoop HDFS的管理角色:Namenode进程(仅需1个即可(管理者一个就够))
2. Hadoop HDFS的工作角色:Datanode进程(需要多个(工人,越多越好,一个机器启动一个))
3. Hadoop YARN的管理角色:ResourceManager进程(仅需1个即可(管理者一个就够))
4. Hadoop YARN的工作角色:Nodellanager进程(需要多个(工人,越多越好,一个机器启动一个))
5. Hadoop 历史记录服务器角色:HistoryServer进程(仅需1个即可(功能进程无需太多1个足够))
6. Hadoop 代理服务器角色:WebProxyServer进程(仅需1个即可(功能进程无需太多1个足够))
7. Zookeeper的进程:QuorumPeerMain进程(仅需1个即可(Zookeeper的工作者,越多越好))

### 3. 角色和节点分配

角色分配如下:

1. node1:Namenode, Datanode, ResourceManager, NodeManager, HistoryServer, WebProxyServer, QuorumPeerMain
2. node2:Datanode. NodeManager, QuorumPeerMain
3. node3:Datanode, NodeManager, QuorumPeerMain

### 4. Hadoop集群部署

前置：
[[Linux#集群化前置|集群化前置]]
调整虚拟机内存，node1：4GB以上，node2：2GB以上，node3：2GB以上;
[[Linux#ZooKeeper|ZooKeeper集群部署]]

Hadoop集群部署

1. 【node1】下载或上传Hadoop安装包，解压，配置软链接
	```sh
	# 上传本地安装包
	rz
	# 网络下载安装包
	wget http://archive.apache.org/dist/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz
	
	# 解压
	tar -zxvf hadoop-3.3.0.tar.gz -C /export/servers/
	
	# 构建软链接
	ln -s /export/servers/hadoop-3.3.0 /export/servers/hadoop
	```
	
2. 【node1】配置：`hadoop-env.sh`
	```sh
	# 配置文件都在该文件夹中
	cd /export/servers/hadoop/etc/hadoop
	
	# 配置Java安装路径
	export JAVA_HOME=/export/servers/jdk
	# 配置Hadoop安装路径
	export HADOOP_HOME=/export/servers/hadoop
	# Hadoop hdfs配置文件路径
	export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
	# Hadoop yarn配置文件路径
	export YARN_CONF_DIR=$HADOOP_HOME/etc/hadoop
	# Hadoop hdfs日志文件夹
	export HADOOP_LOG_DIR=$HADOOP_HOME/logs/hdfs
	# Hadoop yarn日志文件夹
	export YARN_LOG_DIR=$HADOOP_HOME/logs/yarn
	
	# Hadoop的使用启动用户配置
	export HDFS_NAMENODE_USER=root
	export HDFS_DATANODE_USER=root
	export HDFS_SECONDARYNAMENODE_USER=root
	export YARN_RESOURCEMANAGER_USER=root
	export YARN_NODEMANAGER_USER=root
	export YARN_PROXYSERVER_USER=root
	```
	
3. 【node1】配置：`core-site.xml`
	```xml
	<configuration>
		<property>
			<name>fs.defaultFS</name>
			<value>hdfs://node1:8020</value>
			<description></description>
		</property>
		
		<property>
			<name>io.file.buffer.size</name>
			<value>131072</value>
			<description></description>
		</property>
	</configuration>
	```

4. 【node1】配置：`hdfs-site.xml`
	```xml
	<configuration>
		<property>
			<name>dfs.datanode.data.dir.perm</name>
			<value>700</value>
		</property>
		
		<property>
			<name>dfs.namenode.name.dir</name>
			<value>/export/data/hadoop/nn</value>
			<description>Path on the local filesystem where the NameNode stores the namespace and transactions logs persistently.</description>
		</property>
		
		<property>
			<name>dfs.namenode.hosts</name>
			<value>node1,node2,node3</value>
			<description>List of permitted DataNodes.</description>
		</property>
		
		<property>
			<name>dfs.blocksize</name>
			<value>268435456</value>
			<description></description>
		</property>
		
		<property>
			<name>dfs.namenode.handler.count</name>
			<value>100</value>
			<description></description>
		</property>
		
		<property>
			<name>dfs.datanode.data.dir</name>
			<value>/export/data/hadoop/dn</value>
		</property>
	</configuration>
	```
	
5. 【node1】配置：`mapred-env.sh`
	```sh
	# 在文件的开头加入如下环境变量设置
	export JAVA_HOME=/export/servers/jdk
	export HADOOP_JOB_HISTORYSERVER_HEAPSIZE=1000
	export HADOOP_MAPRED_ROOT_LOGGER=INFO,RFA
	```

6. 【node1】修改配置文件：`mapred-site.xml`
	```xml
	<configuration>
		<property>
			<name>mapreduce.framework.name</name>
			<value>yarn</value>
			<description></description>
		</property>
		
		<property>
			<name>mapreduce.jobhistory.address</name>
			<value>node1:10020</value>
			<description></description>
		</property>
		
		<property>
			<name>mapreduce.jobhistory.webapp.address</name>
			<value>node1:19888</value>
			<description></description>
		</property>
		
		<property>
			<name>mapreduce.jobhistory.intermediate-done-dir</name>
			<value>/export/data/hadoop/mr-history/tmp</value>
			<description></description>
		</property>
		
		<property>
			<name>mapreduce.jobhistory.done-dir</name>
			<value>/export/data/hadoop/mr-history/done</value>
			<description></description>
		</property>
		
		<property>
			<name>yarn.app.mapreduce.am.env</name>
			<value>HADOOP_MAPRED_HOME=$HADOOP_HOME</value>
		</property>
		
		<property>
			<name>mapreduce.map.env</name>
			<value>HADOOP_MAPRED_HOME=$HADOOP_HOME</value>
		</property>
		
		<property>
			<name>mapreduce.reduce.env</name>
			<value>HADOOP_MAPRED_HOME=$HADOOP_HOME</value>
		</property>
	</configuration>
	```

7. 【node1】配置：`yarn-env.sh`
	```sh
	# 在文件的开头加入如下环境变量设置
	export JAVA_HOME=/export/servers/jdk
	export HADOOP_HOME=/export/servers/hadoop
	export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
	export YARN_CONF_DIR=$HADOOP_HOME/etc/hadoop
	export YARN_LOG_DIR=$HADOOP_HOME/logs/yarn
	export HADOOP_LOG_DIR=$HADOOP_HOME/logs/hdfs
	```

8. 【node1】配置：`yarn.site.xml`
	```xml
	<configuration>
		
		<!-- Site specific YARN configuration properties -->
		<property>
			<name>yarn.log.server.url</name>
			<value>http://node1:19888/jobhistory/logs</value>
			<description></description>
		</property>
		
		<property>
			<name>yarn.web-proxy.address</name>
			<value>node1:8089</value>
			<description>proxy server hostname and port</description>
		</property>
	
		<!-- 是否将对容器实施物理内存限制。-->
		<property>
			<name>yarn.nodemanager.pmem-check-enabled</name>
			<value>false</value>
		</property>
		
		<!-- 是否将对容器实施虚拟内存限制。-->
		<property>
			<name>yarn.nodemanager.vmem-check-enabled</name>
			<value>false</value>
		</property>
	
		<property>
			<name>yarn.log-aggregation-enable</name>
			<value>true</value>
			<description>Configuration to enable or disable log aggregation</description>
		</property>
		
		<property>
			<name>yarn.nodemanager.remote-app-log-dir</name>
			<value>/tmp/logs</value>
			<description>Configuration to enable or disable log aggregation</description>
		</property>
		
		
		<!-- Site specific YARN configuration properties -->
		<property>
			<name>yarn.resourcemanager.hostname</name>
			<value>node1</value>
			<description></description>
		</property>
		
		<property>
			<name>yarn.resourcemanager.scheduler.class</name>
			<value>org.apache.hadoop.yarn.server.resourcemanager.scheduler.fair.FairScheduler</value>
			<description></description>
		</property>
		
		<property>
			<name>yarn.nodemanager.local-dirs</name>
			<value>/export/data/hadoop/nm-local</value>
			<description>Comma-separated list of paths on the local filesystem where intermediate data is written.</description>
		</property>
		
		<property>
			<name>yarn.nodemanager.log-dirs</name>
			<value>/export/data/hadoop/nm-log</value>
			<description>Comma-separated list of paths on the local filesystem where logs are written.</description>
		</property>
		
		
		<property>
			<name>yarn.nodemanager.log.retain-seconds</name>
			<value>10800</value>
			<description>Default time (in seconds) to retain log files on the NodeManager Only applicable if log-aggregation is disabled.</description>
		</property>
		
		<property>
			<name>yarn.nodemanager.aux-services</name>
			<value>mapreduce_shuffle</value>
			<description>Shuffle service that needs to be set for Map Reduce applications.</description>
		</property>
	</configuration>
	```

9. 【node1】修改workers文件
	```shell
	# 全部内容如下
	node1
	node2
	node3
	```

10. 【node1】分发hadoop到其它机器
	```shell
	# 在node1执行
	cd /export/servers
	
	scp -r hadoop-3.3.0 node2:$PWD
	scp -r hadoop-3.3.0 node2:$PWD
	```

11. 【node2，node3】创建软链接
	```shell
	ln -s /export/servers/hadoop-3.3.0 /export/servers/hadoop
	```

12. 创建所需目录
	在node1执行：
	```shell
	mkdir -p /export/data/hadoop/nn; mkdir -p /export/data/hadoop/dn; mkdir -p /export/data/hadoop/nm-log; mkdir -p /export/data/hadoop/nm-local;
	```
	
	在node2和node3分别执行：
	```shell
	mkdir -p /export/data/hadoop/dn; mkdir -p /export/data/hadoop/nm-log; mkdir -p /export/data/hadoop/nm-local;
	```

13. 配置环境变量
	在node1、node2、node3修改/etc/profile
	```shell
	vim /etc/profile
	
	export HADOOP_HOME=/export/servers/hadoop
	export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
	
	# 执行source /etc/profile生效
	source /etc/profile
	```

14. 【node1】格式化NameNode
	```shell
	hadoop namenode -format
	```

15. 【node1】启动hadoop的hdfs和yarn集群
	```shell
	start-dfs.sh; start-yarn.sh;
	# 如需停止可以执行
	stop-dfs.sh; stop-yarn.sh
	```

16. 启动历史和web代理服务器
	```shell
	mapred --daemon start historyserver
	mr-jobhistory-daemon.sh start historyserver; 
	yarn-daemon.sh start proxyserver;
	
	# 停止
	mapred --daemon stop historyserver
	mr-jobhistory-daemon.sh stop historyserver
	yarn-daemon.sh start proxyserver
	```

### 5. 验证Hadoop集群运行情况

1. 在node1、node2、node3上通过jps验证进程是否都启动成功

2. 验证HDFS
	浏览器打开：http://node1:9870, 创建文件test.txt，随意填入内容，并执行：
	```shell
	hadoop fs -put test.txt /test.txt
	
	hadoop fs -cat /test.txt
	```

3. 验证YARN，浏览器打开：http://node1:8088
	```shell
	# 创建文件words.txt，填入如下内容
	hello world what
	hello what 
	
	# 将文件上传到HDFS中
	hadoop fs -put words.txt /words.txt
	
	# 执行如下命令验证YARN是否正常
	hadoop jar /export/servers/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.0.jar wordcount -Dmapred.job.queue.name=root.root /words.txt /output
	```

## Spark

前置：[[Linux#Hadoop|Hadoop集群部署]]

1. 【node1】上传或下载，并解压
	```shell
	wget https://archive.apache.org/dist/spark/spark-2.4.5/spark-2.4.5-bin-hadoop2.7.tgz
	
	# 解压
	tar -zxvf spark-3.5.1-bin-hadoop3.tgz -C /export/server/
	
	# 设置软链接
	ln -s /export/servers/spark-3.5.1-bin-hadoop3 /export/server/spark
	```

2. 【node1】修改配置文件名称
	```shell
	# 改名
	cd /export/server/spark/conf
	mv spark-env.sh.template spark-env.sh
	mv workers.template workers
	```

3. 【node1】配置：`spark-env.sh`
	```shell
	## 设置JAVA安装目录
	JAVA_HOME=/export/servers/jdk
	
	## HADOOP软件配置文件目录，读取HDFS上文件和运行YARN集群
	HADOOP_CONF_DIR=/export/servers/hadoop/etc/hadoop
	YARN_CONF_DIR=/export/servers/hadoop/etc/hadoop
	
	## 指定spark老大Master的IP和提交任务的通信端口
	export SPARK_MASTER_HOST=node1
	export SPARK_MASTER_PORT=7077
	
	SPARK_MASTER_WEBUI_PORT=8080
	SPARK_WORKER_CORES=1
	SPARK_WORKER_MEMORY=1g
	```

4. 【node1】配置：`workers`
	```shell
	node1
	node2
	node3
	```

5. 【node1】分发到其他机器上
	```shell
	cd /export/servers
	scp -r spark-3.5.1-bin-hadoop3 node2:$PWD
	scp -r spark-3.5.1-bin-hadoop3 node3:$PWD
	```

6. 【node2，node3】设置软链接
	```shell
	ln -s /export/servers/spark-3.5.1-bin-hadoop3 /export/servers/spark
	```

7. 【node1】启动Spark集群
	```shell
	/export/servers/spark/sbin/start-all.sh
	
	# 如需停止，可以
	/export/servers/spark/sbin/stop-all.sh
	```

8. 打开Spark监控页面，浏览器打开：http://node1:8081

9. 【node1】提交测试任务
	```shell
	/export/servers/spark/bin/spark-submit --master spark://node1:7077 --class org.apache.spark.examples.SparkPi /export/server/spark/examples/jars/spark-examples_2.11-2.4.5.jar
	```

## HBase

1. HBase依赖Zookeeper、JDK、Hadoop（HDFS）
   - [[Linux#集群化前置|集群化软件前置准备（JDK）]]
   - [[Linux#ZooKeeper|Zookeeper]]
   - [[Linux#Hadoop|Hadoop]]

2. 【node1】下载HBase安装包
   ```shell
   # 下载
   wget http://archive.apache.org/dist/hbase/2.1.0/hbase-2.1.0-bin.tar.gz
   
   # 解压
   tar -zxvf hbase-2.1.0-bin.tar.gz -C /export/servers
   
   # 配置软链接
   ln -s /export/servers/hbase-2.1.0 /export/servers/hbase
   ```
   
3. 【node1】修改`hbase/conf/hbase-env.sh`文件
   ```shell
   # 在28行配置JAVA_HOME
   export JAVA_HOME=/export/servers/jdk
   # 在126行配置：
   # 不使用HBase自带的Zookeeper，而是用独立Zookeeper
   export HBASE_MANAGES_ZK=false
   # 在任意行，添加如下内容：
   export HBASE_DISABLE_HADOOP_CLASSPATH_LOOKUP="true"
   ```

4. 【node1】修改`conf/hbase-site.xml`文件
   ```xml
   # 将文件的全部内容替换成如下内容：
   <configuration>
	   <!-- HBase数据在HDFS中的存放的路径 -->
	   <property>
		   <name>hbase.rootdir</name>
		   <value>hdfs://node1:8020/hbase</value>
	   </property>
	   <!-- Hbase的运行模式。false是单机模式，true是分布式模式。若为false,Hbase和Zookeeper会运行在同一个JVM里面 -->
	   <property>
		   <name>hbase.cluster.distributed</name>
		   <value>true</value>
	   </property>
	   <!-- ZooKeeper的地址 -->
	   <property>
		   <name>hbase.zookeeper.quorum</name>
		   <value>node1,node2,node3</value>
	   </property>
	   <!-- ZooKeeper快照的存储位置 -->
	   <property>
		   <name>hbase.zookeeper.property.dataDir</name>
		   <value>/export/servers/apache-zookeeper-3.6.0-bin/data</value>
	   </property>
	   <!--  V2.1版本，在分布式情况下, 设置为false -->
	   <property>
		   <name>hbase.unsafe.stream.capability.enforce</name>
		   <value>false</value>
	   </property>
   </configuration>
   ```

5. 【node1】修改`conf/regionservers`文件
   ```shell
   # 填入如下内容
   node1
   node2
   node3
   ```

6. 【node1】分发hbase到其它机器
   ```shell
   cd /export/servers
   
   scp -r hbase-2.5.8 node2:$PWD
   scp -r hbase-2.5.8 node3:$PWD
   ```

7. 【node2、node3】配置软链接
   ```shell
   ln -s /export/servers/hbase-2.5.8 /export/servers/hbase
   ```

8. 【node1、node2、node3执行】，配置环境变量
   ```shell
   # 配置在/etc/profile内，追加如下两行
   export HBASE_HOME=/export/servers/hbase
   export PATH=$HBASE_HOME/bin:$PATH
   
   source /etc/profile
   ```

9. 【node1】启动HBase
   > 请确保：Hadoop HDFS、Zookeeper是已经启动了的
   
   ```shell
   start-hbase.sh
   
   # 如需停止可使用
   stop-hbase.sh
   ```

10. 验证HBase
    浏览器打开：http://node1:16010，即可看到HBase的WEB UI页面

11. 简单测试使用HBase
    【node1】
    ```shell
    hbase shell
    
    # 创建表
    create 'test', 'cf'
    
    # 插入数据
    put 'test', 'rk001', 'cf:info', 'itheima'
    
    # 查询数据
    get 'test', 'rk001'
    
    # 扫描表数据
    scan 'test'
    ```

## Kafka

1. 确保已经安装并部署了JDK和Zookeeper服务

2. 【node1】下载并上传Kafka的安装包
   ```shell
   #上传
   rz
   # 下载安装包
   wget http://archive.apache.org/dist/kafka/2.4.1/kafka_2.12-2.4.1.tgz
   ```

3. 【node1】解压
	```shell
   mkdir -p /export/servers		# 此文件夹如果不存在需先创建
   
   # 解压
   tar -zxvf kafka_2.12-2.4.1.tgz -C /export/servers/
   
   # 创建软链接
   ln -s /export/servers/kafka_2.12-2.4.1 /export/servers/kafka
   ```

4. 【node1】修改kafka/config/`server.properties`文件
   ````shell
   cd /export/servers/kafka/config
   # 指定broker的id
   broker.id=1
   # 指定 kafka的绑定监听的地址
   listeners=PLAINTEXT://node1:9092
   # 指定Kafka数据的位置
   log.dirs=/export/server/kafka/data
   # 指定Zookeeper的三个节点
   zookeeper.connect=node1:2181,node2:2181,node3:2181
   ````

5. 【在node1操作】将node1的kafka复制到node2和node3
   ```shell
   cd /export/server
   
   # 复制到node2同名文件夹
   scp -r kafka_2.12-2.4.1 node2:`pwd`/
   # 复制到node3同名文件夹
   scp -r kafka_2.12-2.4.1 node3:$PWD
   ```

6. 【在node2操作】
   ```shell
   # 创建软链接
   ln -s /export/server/kafka_2.12-2.4.1 /export/server/kafka
   
   cd /export/server/kafka/config
   # 指定broker的id
   broker.id=2
   # 指定 kafka的绑定监听的地址
   listeners=PLAINTEXT://node2:9092
   # 指定Kafka数据的位置
   log.dirs=/export/server/kafka/data
   # 指定Zookeeper的三个节点
   zookeeper.connect=node1:2181,node2:2181,node3:2181
   ```

7. 【node3操作】
   ```shell
   # 创建软链接
   ln -s /export/server/kafka_2.12-2.4.1 /export/server/kafka
   
   cd /export/server/kafka/config
   # 指定broker的id
   broker.id=3
   # 指定 kafka的绑定监听的地址
   listeners=PLAINTEXT://node3:9092
   # 指定Kafka数据的位置
   log.dirs=/export/server/kafka/data
   # 指定Zookeeper的三个节点
   zookeeper.connect=node1:2181,node2:2181,node3:2181
   ```

8. 启动kafka
   ```shell
   # 请先确保Zookeeper已经启动了
   
   # 方式1：【前台启动】分别在node1、2、3上执行如下语句
   /export/server/kafka/bin/kafka-server-start.sh /export/server/kafka/config/server.properties
   
   # 方式2：【后台启动】分别在node1、2、3上执行如下语句
   nohup /export/server/kafka/bin/kafka-server-start.sh /export/server/kafka/config/server.properties 2>&1 >> /export/server/kafka/kafka-server.log &
   ```

9. 验证Kafka启动
   ```shell
   # 在每一台服务器执行
   jps
   ```