

地址
---------
https://www.runoob.com/cplusplus/cpp-basic-syntax.html （入门教程）
https://www.runoob.com/w3cnote/cpp-keyword-intro.html (保留关键字说明)
https://shengchangjian.github.io/2016/09/cpp-multifile.html 





C++ 变量作用域
----------
作用域是程序的一个区域，一般来说有三个地方可以定义变量：
```
局部变量
在函数或一个代码块内部声明的变量，称为局部变量。它们只能被函数内部或者代码块内部的语句使用。

全局变量
在所有函数外部定义的变量（通常是在程序的头部），称为全局变量。全局变量的值在程序的整个生命周期内都是有效的。
全局变量可以被任何函数访问。也就是说，全局变量一旦声明，在整个程序中都是可用的。


初始化局部变量 和 全局变量
当局部变量被定义时，系统不会对其初始化，您必须自行对其初始化。定义全局变量时，系统会自动初始化为下列值：
数据类型	初始化默认值
int	    0
char	'\0'
float	0
double	0
pointer	NULL

正确地初始化变量是一个良好的编程习惯，否则有时候程序可能会产生意想不到的结果。
```


C++ 常量
------------
常量是固定值，在程序执行期间不会改变。这些固定的值，又叫做字面量。
常量可以是任何的基本数据类型，可分为整型数字、浮点数字、字符、字符串和布尔值。

常量就像是常规的变量，只不过常量的值在定义后不能进行修改。

整数常量
整数常量可以是十进制、八进制或十六进制的常量。前缀指定基数：0x 或 0X 表示十六进制，0 表示八进制，不带前缀则默认表示十进制。

整数常量也可以带一个后缀，后缀是 U 和 L 的组合，U 表示无符号整数（unsigned），L 表示长整数（long）。后缀可以是大写，也可以是小写，U 和 L 的顺序任意。

下面列举几个整数常量的实例：
```
212         // 合法的
215u        // 合法的
0xFeeL      // 合法的
078         // 非法的：8 不是八进制的数字
032UU       // 非法的：不能重复后缀
```

以下是各种类型的整数常量的实例：
```
85         // 十进制
0213       // 八进制 
0x4b       // 十六进制 
30         // 整数 
30u        // 无符号整数 
30l        // 长整数 
30ul       // 无符号长整数
```


浮点常量
浮点常量由整数部分、小数点、小数部分和指数部分组成。您可以使用小数形式或者指数形式来表示浮点常量。

当使用小数形式表示时，必须包含整数部分、小数部分，或同时包含两者。当使用指数形式表示时， 必须包含小数点、指数，或同时包含两者。带符号的指数是用 e 或 E 引入的。

下面列举几个浮点常量的实例：
```
3.14159       // 合法的 
314159E-5L    // 合法的 
510E          // 非法的：不完整的指数
210f          // 非法的：没有小数或指数
.e55          // 非法的：缺少整数或分数
```

布尔常量
布尔常量共有两个，它们都是标准的 C++ 关键字：
```
true 值代表真。
false 值代表假。
```
我们不应把 true 的值看成 1，把 false 的值看成 0。


字符常量
字符常量是括在单引号中。如果常量以 L（仅当大写时）开头，则表示它是一个宽字符常量（例如 L'x'），此时它必须存储在 wchar_t 类型的变量中。否则，它就是一个窄字符常量（例如 'x'），此时它可以存储在 char 类型的简单变量中。

字符常量可以是一个普通的字符（例如 'x'）、一个转义序列（例如 '\t'），或一个通用的字符（例如 '\u02C0'）。

在 C++ 中，有一些特定的字符，当它们前面有反斜杠时，它们就具有特殊的含义，被用来表示如换行符（\n）或制表符（\t）等。下表列出了一些这样的转义序列码：
```
转义序列	含义
\\	\ 字符
\'	' 字符
\"	" 字符
\?	? 字符
\a	警报铃声
\b	退格键
\f	换页符
\n	换行符
\r	回车
\t	水平制表符
\v	垂直制表符
\ooo	一到三位的八进制数
\xhh . . .	一个或多个数字的十六进制数
```

字符串常量
字符串字面值或常量是括在双引号 "" 中的。一个字符串包含类似于字符常量的字符：普通的字符、转义序列和通用的字符。

您可以使用空格做分隔符，把一个很长的字符串常量进行分行。

下面的实例显示了一些字符串常量。下面这三种形式所显示的字符串是相同的。
```
"hello, dear"

"hello, \

dear"

"hello, " "d" "ear"
```


定义常量
在 C++ 中，有两种简单的定义常量的方式：
使用 #define 预处理器。
使用 const 关键字。
```
#define 预处理器
下面是使用 #define 预处理器定义常量的形式：
#define identifier value

const 关键字
您可以使用 const 前缀声明指定类型的常量，如下所示：
const type variable = value;
```




sizeof() 函数来获取各种数据类型的大小
---------
```
cout << "bool: \t\t" << "所占字节数：" << sizeof(bool);  
cout << "\t最大值：" << (numeric_limits<bool>::max)();  
cout << "\t\t最小值：" << (numeric_limits<bool>::min)() << endl;  

cout << "char: \t\t" << "所占字节数：" << sizeof(char);  
cout << "\t最大值：" << (numeric_limits<char>::max)();  
cout << "\t\t最小值：" << (numeric_limits<char>::min)() << endl;  
```


typedef 声明
----------
您可以使用 typedef 为一个已有的类型取一个新的名字。下面是使用 typedef 定义一个新类型的语法：
typedef type newname; 

例如，下面的语句会告诉编译器，feet 是 int 的另一个名称：
typedef int feet;

现在，下面的声明是完全合法的，它创建了一个整型变量 distance：
feet distance;



string 与 char 互转
---------
将  char *    或者  char []   转换为  string
```
可以直接赋值，转换。
//char *x = "hello world";
char x[] = "hello world";
string str = x;
cout << str << endl;
```

将   string   转换为 char *    或者    char []   
```
string 是c++标准库里面其中一个，封装了对字符串的操作 
把string转换为char* 有  3种方法： 
1.  调用  string   的   data   函数 
如： 
string str="abc"; 
char *p=str.data(); 


2.调用  string   的  c_str   函数 
如：
string str="gdfd"; 
char *p=str.c_str(); 


3 调用  string   的  copy   函数 
如: 
string str="hello"; 
char p[40]; 
str.copy(p,5,0); //这里5，代表复制几个字符，0代表复制的位置
*(p+5)='/0';     //要手动加上结束符
cout < <p;
```

string 转 int
------------
```
char* s = "1234";
string str("5678");

int intS = atoi(s);

//此写法会报错
//int intStr = atoi(str);
//需先将string转成char*
int intStr = atoi(str.c_str());

cout << "char* 转int:    " << intS << endl;
cout << "string 转int:    " << intStr << endl;
```


int 转 string
------------
```
int id = 13;
string str = std::to_string(id);

cout << str << endl;
```


获取数组长度
------------
C、C++中没有提供 直接获取数组长度的函数，对于存放字符串的字符数组提供了一个strlen函数获取长度，那么对于其他类型的数组如何获取他们的长度呢？其中一种方法是使 用sizeof(array) / sizeof(array[0]), 在C语言中习惯上在 使用时都把它定义成一个宏，比如#define GET_ARRAY_LEN(array,len) {len = (sizeof(array) / sizeof(array[0]));} 。而在C++中则可以使用模板 技术定义一个函数，比如：
```
template <class T>
int getArrayLen(T& array)
{
	return (sizeof(array) / sizeof(array[0]));
}
```
这样对于不同类型的数 组都可以使用这个宏或者这个函数来获取数组的长度了。以下是两个Demo程序，一个C语言的，一个C++的：

P.S：若数组为存储 字符串的字符数组，则所求得的长度还需要减一，即对于宏定义： #define GET_ARRAY_LEN(array,len) {len = (sizeof(array) / sizeof(array[0]) - 1 );} ，对于函数定义：
```
template <class T>
int getArrayLen(T& array)
{
	return (sizeof(array) / sizeof(array[0]) - 1);
}
```



虚方法 virtual
---------
```
class Pet
{
public:
	Pet(std::string theName);
	void eat();
	virtual void play();
}

class Cat:public Pet
{
public:
	Cat(std::string theName);
	void play();
}

void Pet::eat()
{
	std::cout << name << "正在吃";
}

void Pet::play()
{
	std::cout << name << "正在玩";
}

void Cat::play()
{
	std::cout << name << "玩线球";
}

Pet *cat = new Cat;
cat->play();
```
假设子类cat中重写的play方法，如果cat中的play方法是普通方法，则上面执行的是Pet中的play方法。如果Pet中的play为虚方法，则执行的是cat中的play方法。





防止重复引入
-----------
```
#ifndef HEADER_H
#define HEADER_H

在这时写代码

#endif

```


函数模板
-----------
```
#include <iostream>
#include <string>

template <class T>
void swap(T &a, T &b)
{
	T tmp = a;
	a = b;
	b = tmp;
}

int main()
{
	int i1 = 100;
	int i2 = 200;
	std::count << "交换前，i1=" << i1 << ", i2=" << i2 << endl;
	swap(i1, i2);
	//swap<int>(i1, i2);
	std::count << "交换前，i1=" << i1 << ", i2=" << i2 << endl;

	std::string s1 = "张三";
	std::string s2 = "李四";
	std::count << "交换前，s1=" << s1 << ", s2=" << s2 << endl;
	swap(s1, s2);
	std::count << "交换前，s1=" << s1 << ", s2=" << s2 << endl;
}
```



类模板
----------
```
template <class T>
class Stack
{
public:
	Stack(unsigned int size=100);
	~Stack();
	void push(T value);
	T pop();

private:
	unsigned int size;
	unsigned int sp;
	T *data;
};

template <class T>
Stack<T>::Stack(unsigned int size)
{
	this->size = size;
	data = new T[size];
	sp = 0;
}

template <class T>
Stack<T>::~Stack()
{
	delete []data;
}

template <class T>
Stack<T>::~Stack()
{
	delete []data;
}

template <class T>
void Stack<T>::push(T value)
{
	data[sp++] = value;
}

template <class T>
T Stack<T>::pop()
{
	return data[--sp];
}

int main()
{
	Stack<int> intStack(100);
	intStack.push(1);
	intStack.push(2);
	intStack.push(3);

	std::cout << intStack.pop() << endl;
	std::cout << intStack.pop() << endl;
	std::cout << intStack.pop() << endl;

	return 0;
}
```


类的内联模板
-----------
```
template <class T>
class Stack
{
public:
	Stack(unsigned int size=100)
	{
		this->size = size;
		data = new T[size];
		sp = 0;
	}

	~Stack()
	{
		delete []data;
	}

	void push(T value)
	{
		data[sp++] = value;
	}

	T pop()
	{
		return data[--sp];
	}

private:
	unsigned int size;
	unsigned int sp;
	T *data;
};

int main()
{
	Stack<int> intStack(100);
	intStack.push(1);
	intStack.push(2);
	intStack.push(3);

	std::cout << intStack.pop() << endl;
	std::cout << intStack.pop() << endl;
	std::cout << intStack.pop() << endl;

	return 0;
}
```

