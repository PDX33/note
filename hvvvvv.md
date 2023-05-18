##### IP 

脚本.sh文件

```
cat ip|while read line 

do

ipcalc $line/26 |grep Network|awk ‘{print($2)’}

done 
```

kali里面直接使用的计算IP范围的命令是ipcalc+已知ip

##### 一、应急响应



> 样本、流量、进程、日志、模块、内存、启动项
>
> ![image-20230504125802368](https://cdn.jsdelivr.net/gh/PDX33/image/202305181744573.png)

###### 1.1windows

> 1. **事件类型**
>
>    1.红队木马、APT木马
>
>    2.挖矿木马
>
>    3.勒索病毒
>
>    4.暗链
>
> 2. **后门排查**
>
> 1.账户 隐匿账户  匿名账户 克隆账户 （工具：火绒剑、D盾）
>
> 2.启动项 
>
> ==HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft==\Windows\CurrentVision\****Run****     **RunOnce **     **Policies\Explorer\RUN**这三个地方是可以写启动项的但是是被杀软监控的地方。
>
> 在高亮区下方的Windows NT-CurrentVision下的windows\RUN   winlogo-SHELL键值也可做启动项，之前是未被杀软监控的区域，但是随着使用增多也逐渐被杀软监控。
>
> 3.计划任务（工具：Autoruns）
>
> 在计算机管理—-系统工具—–任务计划程序中查看
>
> Autoruns：此工具内要排查的项目
>
> - 启动项
> - 计划任务
> - office绑定
> - 服务
> -  WMI
>
> **木马该怎么排查？**
>
> 工具：processhacker      proce x 64     火绒剑
>
> 分析：网络行为、进程树、打开的dll文件
>
> 手动排查法：netstat
>
> - 看文件（时间，哪些是新建的）
>
> - 白加黑：一个白名单的exe文件+恶意的dll文件
>
> - 隐藏文件（通过  CLSID（桌面图标通过此ID定位，可以修改文件夹名字为相应ID即显示为相应图标）方法、unicode编码显示为一个没有名字的文件夹，给文件夹替换一个空的图标，达到隐藏效果。
>
>   ![image-20230507160537455](https://cdn.jsdelivr.net/gh/PDX33/image/202305181746277.png3456)

> process Explorer可以右键将进程发送到Check VirusTotal（Check VT）中直接进行检测。看网络不方便，只能看收发流量的大小不能看IP。



###### 1.2 Linux

| 内核信息  | uname -a                | 系统信息                 | cat /etc/os-release |
| --------- | ----------------------- | ------------------------ | ------------------- |
| centOS 下 | cat /etc/redhat-release | 有些回把系统信息保存在这 | cat /etc/issue      |
| ubuntu下  | lsb_release -a          |                          |                     |

| 特权账户           | awk  -F: ‘{if(\$3==0)print \$}’  /etc /passwd     | 可登录账户             | cat /etc/passwd \| grep ‘/bin/bash’                       |
| ------------------ | ------------------------------------------------- | ---------------------- | --------------------------------------------------------- |
| 无密码用户         | awk  -F: ‘length($2)==0{print \$1}’  /etc /passwd | 查看登录信息           | w（在线用户查看，有IP的就是远程登录，没有IP就是本地登录） |
| 公钥               | .ssh 下的authorized_keys                          | 进程导出为文件慢慢分析 | ps -ef  >x.txt(一般以时间来命名例如ps-log-5-7 19：28)     |
| 用户计划任务       | /var/spool/cron (centos)                          | 用户计划任务           | /var/spool/cron/crontabs (debian)                         |
| 敏感目录           | /usr/tmp          /tmp                            | /usr/bin               | /usr/sbin    ~/.ssh                                       |
| 进程排查           | ps -aux      netstat   -antp                      | 登录成功               | last                                                      |
| 登录失败           | lastb                                             | 登录成功用户           | lastlog                                                   |
| 日志路径           | /var/log/auth.log                                 | centOS                 | /var/log/secure                                           |
| 向bash_history追加 | history -a                                        | ~/.bash_history        | history  -c  清除（history是实时的，bash_history非        |
| 防火墙             | iptables -L(主要是看是否有隧道)                   |                        |                                                           |

```html
Linux自启动总结
1. chkconfig + init.d
​ 1、 使用systemctl （适用CentOS）

​ cd /etc/init.d

​ vim 脚本文件名，文件内容必须加上声明

#!/bin/sh    
#
#chkconfig: 345 80 20    
#description: test       

脚本执行内容
exit 0
    chmod 777 文件
    service 1.sh start   #测试效果
    systemctl enable 1.sh  #添加自启动
或
    chkconfig --add 服务名
2. /etc/rc.local 文件
存在 rc.local 时

cd /etc/rc.d
chmod 777 rc.local    
ln -s /etc/rc.d/rc.local /etc/rc.d/rc3.d/S99local  #建立软链接(非必要)

vim rc.local
    执行脚本绝对路径
    exit 0
不存在 rc.local (适用Ubuntu)

vim /etc/rc.local
chmod 777 /etc/rc.local
systemctl enable rc-local.service
3. /etc/profile.d 文件夹
​ 用户登陆时启用

CentOS可用 Ubuntu 高版本可用

​ 将脚本文件放入 profile.d 即可

4. bashrc
​ 系统启动时启用

编辑用户目录下的 .bashrc 文件即可
```

> - linux的文件就相当于Windows的dll文件
> - Linux常见的后门  1.ssh软链接后门  2. LD_preload  linux加载so文件首先访问的就是LD_preload,即如果你构造一个恶意的LD文件就可以…

==tty1    CTRL+ALT+F1==  虚拟机内部终端登录

==tty2    CTRL+ALT+F2==

> chattr修改文件属性（+i 属性 锁定文件）
>
> lasttr显示文件属性 （ls -l 无法显示 i 属性）
>
> ctime文件创建时间 
>
> mtime修改时间   ==- 表示几天以内  +表示几天以前==
>
> atime访问时间
>
> 举例：find /  ==-mmin==  -30    查看30min以内  Attention：/ 后空格 
>
> ​                            |
>
> ​              min前的参数改为a、c 、m即可
>
>  工具：whohk  GScan-master （python脚本）上述注意项都可自动进行分析
>
> ![image-20230508121141061](https://cdn.jsdelivr.net/gh/PDX33/image/202305181747238.png) 
>
>   FireKylin（1.给777权限 2.   ./运行   3.start  4.生成fkld文件   5.GUI加载fkld文件并分析。

​                      

 



diff -c文件差异

busybox unhide

检测木马Clam AV

#### 二、系统加固

##### 2.1 Linux加固

1.禁用无用账号

2.检查特殊账号

3.添加口令策略

4.限制FTP登录

5.限制用户su

6.关闭不必要的服务

7.检查SSH服务

8.检查NFS共享

9.网络参数

10.Bash历史命令

11.设置登录超时

12.syslogd日志

##### windows加固

1.补丁安装

2.账号口令

3.服务网络

4.文件系统

5.日志审核

6.注册表安全

![image-20230506090520335](https://cdn.jsdelivr.net/gh/PDX33/image/202305181748026.png)



##### 数据库加固

1.补丁安装

2.账号默认密码_弱口令

3.匿名账户

4.数据库授权

5.禁止网络链接

6.数据库文件安全

7.日志审核

8.MySQL运行账号

##### 

cc攻击：针对网站服务器的攻击，实质上就是Ddos 攻击。挑战黑洞安全服务器

#####   MSF与CS

> $$
> 
> $$
>
> 

#### 三、内存马

> 现有内存马主要有四个类型：Listener、Filter（固定一些参数）、Servlet(Java的一个组件，处理一些http请求)以及Agent型。在用户请求网站时，前三个马的触发顺序为Listener–>Fi—>Ser
>
> 运行方法就是获取class 文件，执行class文件，把class文件里的内容加载到内存中，需要使用时就在内存中获取响应的函数地址利用函数。在JAVA中你可以自己重写组件从而使用你写的组件，不使用原来的组件。实现方法是在内存中修改而不是在硬盘中修改故而叫内存马（硬盘也可以改一下class包，重新加载，java程序重新运行才生 效），写在内存中立即生效。  
>
> tomcat和spring
>
> tomcat内存马分Listener、Filter、Servlet。三个组件中的一个重写并且加之webshell功能，相当源里面安插后门，只是这个工作在内存中完成。
>
> tomcat的组件catalina组件中会封装一些Servlet。
>
> 注册动态的filter并把其放在最前面，这样就可以最先执行了，并且也成为一个动态webshell。实现动态注册Filter，需要两个步骤，1.先达到能获取request和response；2.通过request和response去注册。
>
> 内存马虽说重启是有效的方法但是在应急中，先收集一些证据，然后再重启。
>
> 怎么查？
>
> - java工具MBeans：有内存马的Value值为空（why？因为正常的是从硬件中加载文件，而你写了内存马直接从内存加载所以为空）可以查看Filter和Servlet，Listener不可查看。
> - arthas（阿里开发的内存马查杀工具）jdk运行 命令Java -jar arthas-boot.jar   PID 
> - tomcat-memshell-scanner-master（jsp脚本放在网页根目录下运行就可）可以查三种马，但是是jsp的，如果是spring就无法查。
>
> 

