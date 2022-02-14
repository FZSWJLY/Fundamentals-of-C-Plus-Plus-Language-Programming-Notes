# 第2章 C++简单程序设计（一）

## 基本数据类型、常量、变量

### C++能够处理的基本数据类型

- 整数类型
- 实数类型
- 字符类型
- 布尔类型

### 程序中的数据

- #### 常量

  - 在源程序中直接写明的数据
  - 其值在整个程序运行期间不可改变

- #### 变量

  - 在程序运行过程中允许改变的数据

### 整数类型

- 基本的整数类型：int

- 按符号分

  符号的（signed）

  无符号的（unsigned）

- 按照数据范围分

  短整数（short）

  长整数（long）

  长长整数（long long）

ISO C++标准并没有没明确规定每种数据类型的字节数和取值范围，它只是规定它们之间的字节数大小顺序满足：

（signed/unsigned）signed char≤（unsigned）short int≤（unsigned）int≤（unsigned）long int≤long long int

### 字符类型（char）

- 容纳单个字符的编码
- 实质上存储的也是整数

### 浮点数类型

- 单精度（float）
- 双精度（double）
- 扩展精度（long double）（详见第6章）

### 字符串类型

- 有字符串常量
- 基本类型中没有字符串变量
- 采用字符数组存储字符串（C风格的字符串）
- 标准C++类库中的String类（C风格的字符串）（详见第6章）

### 布尔类型（bool）

- 只有两个值：true（真）、false（假）
- 常用来表示关系比较、相等比较或逻辑运算的结果

![在这里插入图片描述](https://img-blog.csdnimg.cn/6fae725104d8418481a8fcc00211c3df.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


### 常量

- 在程序运行的整个过程中其值始终不可改变的量
- 直接使用符号（文字）表示的值
- 例如：12，3.5，'A'都是常量

### 整数常量

- 十进制

- 八进制

- 十六进制

- 以文字形式出现的整数

- 十进制

  若干个0~9的数字，但数字部分不能以0开头，正数前边的正号可以省略。

- 八进制

  前导0+若干0~7的数字

- 十六进制

  前导0x+若干个0~9的数字及A~F的数字（大小写均可）

- 后缀

  后缀L（或l）表示类型至少是long

  后缀LL（或ll）表示类型至少是long long

  后缀U（或u）表示unsigned类型

### 浮点数常量

- 以文字出现的实数

- 一般形式

  例如，12.5，-12.5

- 指数形式

  例如，0.345E+2，-34.4E+3

  整数部分和小数部分可以省略其一

- 浮点常量默认为double型，如果后缀F（或f）可以使其成为float型

  例如：12.3f

![在这里插入图片描述](https://img-blog.csdnimg.cn/746b799d9ff24535820f9bf4363fbd3a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


### C风格字符串常量

- 一对双引号括起来的字符序列
- 在内存中按串中字符的排列次序顺序存放，每个字符占一个字节
- 在末尾添加'\0'作为结尾标记

![在这里插入图片描述](https://img-blog.csdnimg.cn/2ebe2c421bf64b57bacc22b6c8fdff9e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


**通过添加前缀可以改变字符常量或者字符串常量的类型**

![在这里插入图片描述](https://img-blog.csdnimg.cn/1c89d6d4991343f0adeee90157af7782.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


### 变量

- 在程序的运行过程中其值可变的量

#### 变量定义

- 数据类型

  变量名1，变量名2，...，变量名n

**在定义变量的同时也可以对它初始化**

#### C++语言中提供了多种初始化方式：

例如：

- int a = 0
- int a(0)
- int a = {0}
- int a{0}

其中使用大括号的初始化方式称为**列表初始化**，列表初始化时不允许信息的丢失。例如用double值初始化int变量，就会造成数据丢失

##### 列表初始化

- 使用大括号的初始化方式
- 不允许信息的丢失

例如：

用double值初始化int变量会造成数据丢失

### 符号常量

- 常量定义语句的形式为：

  - const 数据类型说明符 常量名=常量值
  - 或数据类型说明符 const 常量名=常量值

- 例如：定义一个代表圆周率的符号常量

  - const float PI = 3.1415926

- 符号常量在定义时一定要初始化

  在程序中间不能改变其值

## 程序举例

### 主要知识点

- #### 常量

  在源程序中直接写明的数据，其值在整个程序运行期间不可改变，这样的数据成为常量。

- #### 变量

  在运行过程中从计算机的外部设备（例如键盘、硬盘）读取的，这些数据的值在程序运行过程中允许改变，这样的数据成为变量。

- #### 从键盘输入数据

  iostream类的对象cin的>>操作，可以从标准输入设备（通常是键盘）读入数据。

- #### 数据的存储

  为了存储数据，需要预先为这些数据分配内存空间。

  变量的定义就是在给变量命名的时候分配内存空间。

### 补充2-1：读入并显示整数（续）

```c++
#include <iostream>
using namespace std;
int main() {
	int radius;
	cout << "Please enter the radius!\n";
	cin >> radius;
	cout << "The radius is:" << radius << '\n';
	cout << "Pi is:" << 3.14 << '\n';
	cout << "Please enter a different radius!\n";
	cin >> radius;
	cout << "Now the radius is changed to:" << radius << '\n';
	return 0;
}
```

```
Please enter the radius!
5
The radius is:5
Pi is:3.14
Please enter a different radius!
7
Now the radius is changed to:7
```

### 补充2-2：为常量命名

主要知识点：符号常量

```c++
#include <iostream>
using namespace std;
int main() {
	const double pi(3.14159);
	int radius;
	cout << "Please enter the radius!\n";
	cin >> radius;
	cout << "The radius is:" << radius << '\n';
	cout << "Pi is:" << pi << '\n';
	cout << "Please enter a different radius!\n";
	cin >> radius;
	cout << "Now the radius is changed to:" << pi << '\n';
	cout << "PI is still:" << pi << '\n';
	return 0;
}
```

```
Please enter the radius!
5
The radius is:5
Pi is:3.14159
Please enter a different radius!
7
Now the radius is changed to:3.14159
PI is still:3.14159
```

```c++
#include <iostream>
using namespace std;
int main() {
	const double pi(3.14159);
	int radius(0);
	cout << "The initial radius is:" << radius << '\n';
	cout << "Pi is:" << pi << '\n';
	cout << "Please enter a different radius!\n";
	cin >> radius;
	cout << "Now the radius is changed to:" << pi << '\n';
	cout << "PI is still:" << pi << '\n';
	return 0;
}
```

# 运算与表达式

## 算术运算与赋值运算

### 基本算术运算符

- +、-、*、/（若整数相除，结果取整）

- % （取余，操作数为整数）

### 优先级与结合级

- 先乘除，后加减，同级自左向右

### ++，--（自增、自减）

- 例：i++；--j

前置的自增自减运算符，首先进行加1或者减1运算，把变量自己的值增1或减1，然后变量继续参与其他的运算。后置的自增自减运算符，先将变量里面的值取一个副本出来，如果它需要参与更大范围的运算用这个，然后自己增或减1。

### 赋值运算：将值赋给变量

**赋值运算符“=”**

### 赋值表达式

- 用赋值运算符连接起来的表达式
- 例：n=5

### 例：n = n + 5

- 表达式的值

  赋值运算符左边对象被赋值后的值

- 表达式的类型

  赋值运算左边对象的类型

### 复合的赋值运算符

- 有10种复合运算符：

  +=，-=，*=，/=，%=，<<=，>>=，&=，^=，|=

- 例：

  a += 3等价于a = a + 3

  x *= y + 8等价于x = x * (y + 8)

## 逗号运算、关系运算、逻辑运算和条件运算

### 逗号运算和逗号表达式

- #### 格式

  表达式1, 表达式2

- #### 求解顺序及结果

  - 先求解表达式1，再求解表达式2
  - 最终结果为表达式2的值

- 例：

  a = 3 * 5 , a * 4 最终结果为60

### 关系运算与关系表达式

- 关系运算是比较简单的一种逻辑运算，优先次序为：

![在这里插入图片描述](https://img-blog.csdnimg.cn/5648671571e546c7aaf0aa1dce21b9f9.png#pic_center)


- 关系表达式是一种最简单的逻辑表达式
  - 其结果类型为bool，值只能为true或false
- 例如：a > b，c <= a + b，x + y ==3

### 逻辑运算与逻辑表达式

**例：判断是否“a>b并且x>y”？“**

**并且——逻辑”与“**

- #### 逻辑运算符

  ​               !（非） &&（与）||（或）

  优先次序：高           →             低    

- 逻辑运算符结果类型：bool，值只能为true或false

- #### 逻辑表达式

  例如：(a > b) && (x > y)

- #### ”&&“的运算规则

  - 两侧表达式都为真，结果为真
  - 有一侧表达式为假，结果为假

- ”&&“的”短路特性“ 表达式1 && 表达式2

  - 先求解表达式1
  - 若表达式1的值为false，则最终结果为false，不再求解表达式2
  - 若表达式1的结果为true，则求解表达式2，以表达式2的结果最为最终结果

- #### ”||“的运算规则

  - 两侧表达式都为假，结果为假
  - 有一侧表达式为真，结果为真

- ”||“的”短路特性“ 表达式1 || 表达式2
  - 先求解表达式1
  - 若表达式1的值为true，则最终结果为true，不再求解表达式2
  - 若表达式1的结果为false，则求解表达式2，以表达式2的结果最为最终结果

### 条件运算与条件表达式

- #### 一般形式

  - 表达式1 ? 表达式2 : 表达式3
  - 表达式1必须是bool类型

- #### 执行顺序

  - 先求解表达式1，

- 若表达式1的值为true，则求解表达式2，表达式2的值为最终结果

- 若表达式1的值为false，则求解表达式3，表达式3的值为最终结果

![在这里插入图片描述](https://img-blog.csdnimg.cn/5a6b4c6c0849479aa63dd11482032828.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/86cb42e008014eadbeef16475fd3249f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


### 条件运算（表达式1 ? 表达式2 : 表达式3）的优先级

- 条件运算符优先级高于赋值运算符，低于逻辑运算符

![在这里插入图片描述](https://img-blog.csdnimg.cn/6f12a914391b4f53ac59af211cef7e02.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_16,color_FFFFFF,t_70,g_se,x_16#pic_center)


- 表达式1是bool类型，表达式2、3的类型可以不同，条件表达式的最终类型为2和3中较高的类型

## Sizeof运算、位运算

### Sizeof运算符

- #### 语法形式

  sizeof (类型名) 或 sizeof 表达式

- 结果值：

  ”类型名“所指定的类型，或”表达式“的结果类型所占的字节数

- 例：

  sizeof(short)

  sizeof x

### 位运算——按位与（&）

- #### 运算规则

  将两个运算量的每一个位进行逻辑与操作

- 举例：计算3&5

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/ddd9fe62ed21463f8551a6938f569320.png#pic_center)


- 用途举例：将某一位置0，其他位不变

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/2e688b59853a42819b112448a7d209f4.png#pic_center)


- 用途举例：取指定位

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/fe427aa6319d470887fc413c96303e93.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


### 位运算——按位与（&）

- #### 运算规则

  将两个运算量的每一个位进行逻辑或操作

- 举例：计算3|5

![在这里插入图片描述](https://img-blog.csdnimg.cn/fbda3f9944e74ef99454b6286540e6bc.png#pic_center)


- #### 用途举例：

  将某些位置1，其他位不变

  例如：将int型变量a的低字节置1：

  ​            a = a|0xff

### 位运算——按位异或（^）

- 运算规则

  两个操作数进行异或：

  若对应位相同，则结果该位为0

  若对应位不同，则结果该位为1

- 举例：计算071^052

![在这里插入图片描述](https://img-blog.csdnimg.cn/6fc5dc225a2f4aae8d61d4a6b4aae14a.png#pic_center)


- 用途举例：

  使特定位翻转（与0异或保持原值，与1异或取反）

  例如：要使01111010低四位翻转：

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/ced55f3df5714ffca2232d39a2d41827.png#pic_center)


### 位运算——取反（~）

- #### 运算规则：

  单目运算符，对一个二进制数按位取反

- 例：

    025：0000000000010101

  ~025：1111111111101010

### 位运算——移位（<<、>>）

- 左移运算（<<）

  左移后，低位补0，高位舍弃

- 右移运算（>>）

  右移后：

  低位：舍弃

  高位：

  ​			无符号数：补0

  ​			有符号数：补”符号位“

### 运算优先级、类型转换

![在这里插入图片描述](https://img-blog.csdnimg.cn/4aa7b32cc65745569bf23943512f76a6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


### 混合运算时数据类型的转换——隐含转换

- 一些二元运算符（算数运算符、关系运算符、逻辑运算符、位运算符和赋值运算符）要求两个操作数的类型要一致
- 在算术运算和关系运算中如果参与运算的操作数类型不一致，编译系统会自动对数据进行转换（即隐式转换），基本原则是将低类型数据转换为高类型数据
![在这里插入图片描述](https://img-blog.csdnimg.cn/175262cb7213487dad54816c5f7e3ed9.png#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/8efbeeb615334a449483b7af81466b99.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


### 混合运算时数据类型的转换

- 将一个非布尔类型的算术值赋值给布尔类型时，算术值为0则结果为false，否则为true
- 将一个布尔值赋给非布尔类型时，布尔值为false则结果为0，布尔值为true则结果为1
- 将一个浮点数赋给整数类型时，结果值将只保留浮点数中的整数部分，小数部分将丢失
- 讲一个整数赋给浮点类型时，小数部分记为0。如果整数所占的空间超过了浮点类型的容量，精度可能有损失

### 混合运算时数据类型的转换——显式转换

- 显式类型转换的作用是将表达式的结果类型转换为类型说明符所指定的类型

- 语法形式

  - 类型说明符(表达式)

  - (类型说明符)表达式

  - **类型转换操作符<类型说明符>(表达式)**——C++的形式

    类型转换操作符可以是：

    const_cast、dynamic_cast、reinterpret_cast、**static_cast**

    例：int(z)，(int)z，static_cast<int>(z)三种完全等价

## 实验二：简单程序设计（上）

**适当地使用注释，能够提高程序的可读性，还能让部分代码片段暂时不用。**

### 注释方法：

#### 方法一

沿用C语言方法，使用”/* “和”*/“括起注释文字；

#### 方法二

使用”//“，从”//“开始，直到它所在行的行尾，所有字符都被作为注释处理。

### 辅助调试工具：

利用辅助调试工具，可以实现单步运行、设置断点、观察变量和表达式的值等功能

### 实验一

```c++
#include <iostream>
using namespace std;
int main() {
	cout << "The size of an int is:\t\t" << sizeof(int) <<"bytes.\n";
	return 0;
}
```

```
The size of an int is:          4bytes.
```

```c++
#include <iostream>
using namespace std;
int main() {
	cout << "The size of an int is:\t\t" << sizeof(int) <<"bytes.\n";
	cout << "The size of a long is:\t\t" << sizeof(long) << "bytes.\n";
	return 0;
}
```

```
The size of an int is:          4bytes.
The size of a long is:          4bytes.
```

```c++
#include <iostream>
using namespace std;
int main() {
	/*cout << "The size of an int is:\t\t" << sizeof(int) << "bytes.\n";*/
	cout << "The size of a long is:\t\t" << sizeof(long) << "bytes.\n";
	return 0;
}
```

```
The size of a long is:          4bytes.
```

```c++
#include <iostream>
using namespace std;
int main() {
	//cout << "The size of an int is:\t\t" << sizeof(int) << "bytes.\n";
	cout << "The size of a long is:\t\t" << sizeof(long) << "bytes.\n";
	return 0;
}
```

```
The size of a long is:          4bytes.
```

**测试一下字节长度，以确保数据不会溢出**

```c++
#include <iostream>
using namespace std;
int main() {
	cout << "The size of an int is:\t\t" << sizeof(int) << "bytes.\n";
	cout << "The size of a short is:\t\t" << sizeof(short) << "bytes.\n";
	cout << "The size of a long is:\t\t" << sizeof(long) << "bytes.\n";
	cout << "The size of a char is:\t\t" << sizeof(char) << "bytes.\n";
	cout << "The size of a float is:\t\t" << sizeof(float) << "bytes.\n";
	cout << "The size of a double is:\t\t" << sizeof(double) << "bytes.\n";
	return 0;
}
```

```
The size of an int is:          4bytes.
The size of a short is:         2bytes.
The size of a long is:          4bytes.
The size of a char is:          1bytes.
The size of a float is:         4bytes.
The size of a double is:                8bytes.
```

### 实验二

```c++
#include <iostream>
using namespace std;
int main() {
	unsigned int x;
	unsigned int y = 100;
	unsigned int z = 50;
	x = y - z;
	cout << "Difference is: " << x;
	x = z - y;
	cout << "\n Now difference is: " << x << endl;
	return 0;
}
```

```
Different is: 50
 Now different is: 4294967246
```

```c++
#include <iostream>
using namespace std;
int main() {
	int x;
	unsigned int y = 100;
	unsigned int z = 50;
	x = y - z;
	cout << "Difference is: " << x;
	x = z - y;
	cout << "\n Now difference is: " << x << endl;
	return 0;
}
```

```
Difference is: 50
 Now difference is: -50
```

### 实验三

```c++
#include <iostream>
using namespace std;
int main() {
	int a, b, x;
	cout << "input value of a : \n";
	cin >> a;
	cout << "input value of b : \n";
	cin >> b;
	x = (a - b) > 0 ? (a - b) : (b - a);
	cout << "Now difference of a and b is:\t\t" << x;
	return 0;
}
```

```
input value of a :
2022
input value of b :
0214
Now difference of a and b is:           1808
```


