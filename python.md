####  一、基本语法及其变量

###### 1.1python标识符

> ​          用来标识变量、函数、类或其他对象的。标识符以英文大小写或下划线”_”开始，后可跟0个或多个字母、下划线或数字。不允许在标识符中使用标点符号如%、@、$等等。Python 区分大小写。
>
> 1. 类名以大写字母开始，其他所有标识都以小写字母开始。
> 2. 私有标识符以单个下划线“_”开始。
> 3. 强私有符以两个下划线”__”开始。
> 4. 语言定义的特殊名字以两个下划线开始并以两个下划线结尾。
>
> 在python源程序中定义标识符（如变量或常量）时，任何标识符都不能与Python的保留关键字相同。即不可为and 、exec、not、assert、finally、or、break、for、pass、yield、lambda、except、with、del、def、while、elif、raise、continue、global等
>
> 

###### 1.2缩进

> ​       其他语言的缩进只是为了增加代码的易读性，可有可无。Python是用缩进来标识程序块的，同一个块中的所有缩进空格数必须完全相同。

###### 1.3 变量

> ​    所谓变量只是为了存储某个值而预留的内存位置（空间），仅此而已。
>
> 一个值赋予多个变量
>
> ```python
> >>> fool1 = fool2 = fool3 = 250
> ```
>
> 多对多
>
> ```python
> >>> fool1,fool2,fool3 = 250,38,'wow'
> ```
>
> ###### 另外：软件工程 信息系统开发与设计——添加注释，方便你我他

1.4 输出Python变量的值

> python是使用“+”来组合拼接**文字和变量**的
>
> ```python
> >>> s = 'is our best friend.'
> >>> print ("Dog " + s)
> Dog is our best friend.
> ```
>
> ```python
> >>> c = 'Cat '
> >>> print (c + s)
> Cat is our best friend.
> ```
>
> 若在print中使用+来组合数字或数字变量，效果就同数学的加法运算符
>
> 用print语句中利用+将字符串和数字不可组合，两者数据类型不同。

###### 1.4 注释

1. #
2. ‘’‘    …    ’‘’
3. “ “ ”    …  “ ” “

##### 二、Python数字和字符串及类型转换

###### 2.1数字型数据

> 1. int 整数
> 2. float 浮点数
> 3. complex 复数：是实数的延伸，它使任何一个多项式方程都有根。复数中有一个“虚数位” i，它的定义是-1的平方根，及i^2^=-1。任何一个复数都可以表达为x+yi,其中 x 和 y 均为实数，他们分别也被称为实部和虚部。最初的虚部是想象出来的数，i就是imaginary的首字母。在Python中，复数的虚部使用 j 来表示。

###### 2.2数据类型的转换

> 1. int(x)
>
> ```python
> >>> x=int(3.8)
> >>>print(x,type(x))
> 3 <class 'int'>
> 直接舍弃小数点后的数据，并没有进行四舍五入操作
> ```
>
> 1. float(x)  
> 2. str(x)
>
> **why necessary?**
>
> 因为一个变量可能是在几千行甚至几万行代码之前创建的，当引用时可能并不知道也很难知道之前定义的数据类型，这时使用强制类型准换就灰常方便。

###### 2.3字符串

> - **==字符数组的下标从0开始。==**
> - print（s.upper()）改大写           print（s.lower()）改小写
> - print (len()) 获取字符长度           print（s.strip()）删除开始或结尾不需要的空格
> - 以某字符为界分成两个较小的字符串(**子字符串**)print(s.split(','))
>
> ```python
> >>>s='python is an easy to learn,powerful programming language.'
> >>>print(s.split(','))
> ['python is an easy to learn', 'powerful programming language.']
> ```
>
> - 替换字符print(s.replace('old str', 'new'))

##### 三、python基本运算符 