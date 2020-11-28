在js中函数的参数传递其实总共就两种，第一是基本数据类型的传递，第二是object引用类型的传递，第一种基本数据类型的传递毫无疑问是值的传递，包括C语言这样的鼻祖也都是值的传递，但是这里我个人觉得有争议的是object引用类型的传递，在<JavaScript高级程序设计>第三版中P70说到
`ECMAScript中所有函数的参数都是按值传递，也就是说，把函数外部的值复制给函数内部的参数，就和把值从一个变量复制到另一个变量一样。基本数据类型值的传递如同基本类型变量的复制一样，而引用类型值的传递，则如同饮用类型变量的复制一样。。。。`
**说了这么多就是一句话所有参数的传递都是按值传递。**
那么我们先来看看面向对象中java的对象是怎么样传递的，将用toString打印对象的地址
先看下面一段代码

```
public class testjava {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		person p2 = new person();
		setName1(p2);
		System.out.println(p2.name);
		System.out.println(p2.toString());
	}
	public static void setName1(person p) {
		p.name = "weihong";
		System.out.println(p.toString());
	}
}
class person {
	String name;
}
```
输出结果:

```
person@33909752
weihong
person@33909752
```
这里是没毛病的，这个地方你不管对象是传值还是说他传的引用其实都能得到一个正确的结论，但是请看下面的这段代码

```
public class testjava {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		person p2 = new person();
		System.out.println("aaa--"+p2.toString());
		setName1(p2);
		System.out.println("bbb--"+p2.name);
		System.out.println("ccc--"+p2.toString());
	}
	public static void setName1(person obj) {
		obj.name = "weihong";
		System.out.println("ddd--"+obj.toString());
		obj = new person();
		obj.name = "hello world";
		System.out.println("eee--"+obj.toString());
		System.out.println("fff--"+obj.name);
	}
}
class person {
	String name;
}
```
输出结果为:
```
aaa--person@33909752
ddd--person@33909752
eee--person@55f96302
fff--hello world
bbb--weihong
ccc--person@33909752
```
那么这个地方为什么是这样的，我画个图从内存的分配来说明这个问题
第一步执行`person p2 = new person();`内存分配是这样的
![](https://ws4.sinaimg.cn/large/006tNc79gy1fo1yjoarp7j30r008wwen.jpg)
p2的内存地址是0x0000001指向 person所开辟的空间

**这里包括以下的内存地址为了方便我就只在后面直接+1来做了没有根据实际的分配来表述了。。。。**

第二步初始化函数 setName(person obj){}
那么这里的内存空间是怎么样的呢？请看下图
![](https://ws3.sinaimg.cn/large/006tNc79gy1fo22qz7qx3j30sm0h2mxq.jpg)
在这个地方有一个内存地址0x00000002指向一个函数的空间，在函数的空间中开辟了一个分配person空间的obj

第三步初始化设置obj的name的值
![](https://ws1.sinaimg.cn/large/006tNc79gy1fo230zwlhpj30ro0oamxw.jpg)
所以在这个时候你obj跟p2所指向的地址是一样的,所以也就不奇怪aaa那里打印的和ddd的地址是一样的

第四步obj = new person() obj.name = "hello world"请看如下图
![](https://ws4.sinaimg.cn/large/006tNc79gy1fo23gql9t8j30qu0xajsk.jpg)
这个地方其实是新开辟了一个person的空间地址为0x00000003并且你函数那里的开辟的变量obj这个时候他的值不再指向0x0000001，而是指向0x0000003，所以也就不奇怪ddd那里打印的和eee打印出来的地址是不同的，而且一开始创建的0x00000001那里一直有p2来指向他又没有被系统回收，在执行bbb打印那里的时候他还是存在的，而且位置并没有改变，在函数执行完毕后0x00000002这一整块的内存包括新开辟出来的0x00000003都会被系统给回收掉。
总结：**在函数参数需要传递的参数为对象的时候，这个时候传递的是你对象的地址**
     **在函数参数需要传递的参数为基本数据类型的时候，这个时候传递的是你基本数据的值**
     如果我们非要把这两种不同的方式区分开的话那么我觉得只要是你传递的是地址那么就应该是引用传递，把你所被分配空间的数据全部拷贝传过去的就应该是叫做值传递，因为用这样的模型去理解问题起来更容易。
     
理解了java的这个模型，那么我们接下来该理解一下javascript的参数传递是怎么回事了
首先看如下代码

```
window.onload = function () {
    var person = new Object();
    setName(person);
    alert(person.name);
}

function setName(obj) {
    obj.name = "weihong";
    obj = new Object();
    obj.name = "hello world";
}
```
这里输出的结果为weihong 而不是hello world
为什么？因为在setName的空间中开辟的那一块obj的空间是用来存放地址的，不管是地址也好还是abcd这样的字母也好在计算机中都是按照010101这样的高低电位来存放的(具体深入可以去看<编码的奥秘>这书)，如果给他分配一段一定长度的的空间那么他当然可以存下一些基本数据，所以把那些数字字母拷贝进来是存放的没问题的，但是如果你传对象的话，那么你A对象有name属性，你B对象有age属性，各个对象占用的空间长度可是不一样的，你没法在这里保存的，因此你所能做的就是保持这个对象的一个地址，另外开辟一个空间来保存对象的一些属性和方法，其实利用上面java的那个引用传递来理解这个问题就很容易了。。。。。







