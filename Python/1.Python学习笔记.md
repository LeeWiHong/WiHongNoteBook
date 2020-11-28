##Py学习笔记
### Py基础语法

-------

1. Python标识符
在 Python 里，标识符由字母、数字、下划线组成。
在 Python 中，所有标识符可以包括英文、数字以及下划线(_)，但不能以数字开头。

Python 中的标识符是区分大小写的。
以下划线开头的标识符是有特殊意义的。
    以单下划线开头 **_foo 的代表不能直接访问的类属性，需通过类提供的接口进行访问，不能用from xxx import而导入**；
    以双下划线开头的 **__foo 代表类的私有成员**；
    以双下划线开头和结尾的 **__foo__ 代表 Python 里特殊方法专用的标识，如 __init__() 代表类的构造函数**。
Python 可以同一行显示多条语句，方法是用分号 ; 分开，

2. py的输入input如果想给提示可以在input('please input the number')在方法中添加参数进去，需要注意的是，如果用name = input('please input the number')来接受这个输入的数据，这个数据是**字符串类型**的，**就算是输入的数字，这个数字也是字符串**,如果拿输入的数字需要有运算操作需要对他进行转换

3. py可以使用反斜杠'\'来转义很多字符，比如\n表示换行,\t表示制表符,\\表示斜杠\本身
4. 如果字符串里面有很多字符串都需要转义，就需要加入很多\，为了简化py允许`r'字符串'`表示`''`内部字符串不进行转义
5. 如果字符串内部有很多换行，可以用'''...'''的格式表示多行内容
6. py的布尔值只有True 和 False两种，需要注意这里的大小写，布尔值可以有and or not 三种运算
7. py的空值用None表示，不能理解为0，他是一个特殊的值
8. 在py中用字母的大写表示一个常量，必入PIE 但是这个并不是一个不能改变的量，只是人为的去认为不能改变这个PIE的值
9. py中的除法有`/`跟`//`两种，前面的`/`的到的还是一个浮点数，而`//`所的到的将是一个整数，还可以用%进行求模运算
10. 对于单个字符的编码，Python提供了ord()函数获取字符的整数表示，chr()函数把编码转换为对应的字符：

    ```
    >>> ord('A')
    65
    >>> ord('中')
    20013
    >>> chr(66)
    'B'
    >>> chr(25991)
    '文'
    ```

11. 要计算str包含多少个字符，可以用len()函数：
    
    ```
    >>> len('ABC')
    3
    >>> len('中文')
    2
    ```
12. len()函数计算的是str的字符数，如果换成bytes，len()函数就计算字节数：
    
    ```
    >>> len(b'ABC')
    3
    >>> len(b'\xe4\xb8\xad\xe6\x96\x87')
    6
    >>> len('中文'.encode('utf-8'))
    6
    ```
13. 格式化：%运算符就是用来格式化字符串的。在字符串内部，%s表示用字符串替换，%d表示用整数替换，有几个%?占位符，后面就跟几个变量或者值，顺序要对应好。如果只有一个%?，括号可以省略。跟C不同的是，这里输出语句与变量是用%进行隔开的，而C是用**点号,**分开
    `print('name is %s age is%d' %('weihong',19))`
    
|   占位符 |   替换内容    |
|   --- |   ---     |
|   %d  |   整数  |
|   %f  |   浮点  |
|   %s  |   字符串 |
|   %x  |   十六进制    |
    
14. format()格式化字符串输出
另一种格式化字符串的方法是使用字符串的format()方法，它会用传入的参数依次替换字符串内的占位符{0}、{1}……，不过这种方式写起来比%要麻烦得多：

```
>>> 'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)
'Hello, 小明, 成绩提升了 17.1%'
```
### list与tuple

-------

list是一种有序的集合，可以随时添加和删除其中的元素，相当于数组，需要注意的是list中的元素可以是不同类型，比如第一个可以是字符串，而第二个就是数值，第三个就是布尔值还可以list中存放list

```
>>> classmates = ['Michael', 'Bob', 'Tracy']
>>> classmates
['Michael', 'Bob', 'Tracy']
```
可以通过len()来获取这个list的长度，可以通过list的索引来获取其中的元素
删除list的某一个元素使用pop(i)即可，添加可以用append insert等方法

tuple跟list的区别就是tuple一旦初始化则不可以修改，这个的修改其实是说，tuple的每个元素，指向永远不变。即指向'a'，就不能改成指向'b'，指向一个list，就不能改成指向其他对象，但指向的这个list本身是可变的！tuple如果初始化只有一个元素的时候最好是加上一个逗号以免与传统的()括号混淆
先看看定义的时候tuple包含的3个元素：
![](https://ws3.sinaimg.cn/large/006tNc79gy1fqi1ipm6cmj309q078mxb.jpg)
当我们把list的元素'A'和'B'修改为'X'和'Y'后，tuple变为：
![](https://ws1.sinaimg.cn/large/006tNc79gy1fqi1j8ft6aj309q078mxb.jpg)

循环
在py中循环所使用的不是for i = 0;i < length;i++这样C的循环，而是使用for x in...这样的for in循环
while循环举例如下

```
while n > 0:
    sum = sum + n
    n = n - 2
```
dict与set

```
d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
d['Michael']
```
dict的key必须是不可变对象
set是一组key的集合，不存储value，要创建一个set，需要提供一个list作为输入集合
 
```
>>> s = set([1, 2, 3])
>>> s
{1, 2, 3}
```
通过add(key)方法可以添加元素到set中，可以重复添加，但不会有效果：

```
>>> s.add(4)
>>> s
{1, 2, 3, 4}
>>> s.add(4)
>>> s
{1, 2, 3, 4}
```
通过remove(key)方法可以删除元素：

```
>>> s.remove(4)
>>> s
{1, 2, 3}
```
### 函数

-------

在Python中，定义一个函数要使用def语句，依次写出函数名、括号、括号中的参数和冒号:，然后，在缩进块中编写函数体，函数的返回值用return语句返回。

```
def my_abs(x):
    if x >= 0:
        return x
    else:
        return -x
```
函数体内部的语句在执行时，一旦执行到return时，函数就执行完毕，并将结果返回,他的结果返回是可以返回多个值的，比如坐标x,y只要计算好了得到x,y的值, 那么直接在return x,y再结果那里可以拿到这个值，接受可以用 x,y = func(),这里的func中的return语句为return x,y
如果想定义一个什么事也不做的空函数，可以用pass语句：

```
def nop():
    pass
```
数据类型检查可以用内置函数isinstance()实现：

函数参数
在py中可以设置参数的默认值，比如

```
def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
```
在这个函数里，如果调用的时候没有传N的值，那么将默认n=2，如果传了将是传的那个值

列表生成式
![](https://ws2.sinaimg.cn/large/006tNc79gy1fqmlkogwc9j31cq24awsu.jpg)
生成器
![](https://ws2.sinaimg.cn/large/006tNc79gy1fqmodivw3cj31ce5zq7wh.jpg)
迭代器
![](https://ws1.sinaimg.cn/large/006tNc79gy1fqmojpqekvj31cg2iyh2y.jpg)
像数据类型集合可以用for in这样迭代出数据但是不能用next一直获取数据，所以他是可迭代的，他有这个迭代的特性，但是如果是generator他能一直通过next获取数据出来，所以他是迭代器

### 高阶函数特性

-------
面向函数式编程
![](https://ws1.sinaimg.cn/large/006tNc79gy1fqmor6tdyhj31cm2ly4dz.jpg)
map/reduce
![](https://ws3.sinaimg.cn/large/006tNc79gy1fqmpnwsj9oj31as492e3w.jpg)
filter
![](https://ws3.sinaimg.cn/large/006tNc79gy1fqmpnwsj9oj31as492e3w.jpg)
sort
![](https://ws3.sinaimg.cn/large/006tNc79gy1fqmq6c6ne0j31as2iwwv8.jpg)
返回函数
![](https://ws1.sinaimg.cn/large/006tNc79gy1fqmqaddvwnj31b24ci1gt.jpg)
匿名函数
![](https://ws4.sinaimg.cn/large/006tNc79gy1fqmqd4tsvwj31as0zqjy4.jpg)








