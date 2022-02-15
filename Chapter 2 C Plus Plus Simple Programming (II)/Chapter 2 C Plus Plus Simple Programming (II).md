# 第2章 C++简单程序设计（二）

## 数据的输入和输出

### I/O流

- 在C++中，将数据从一个对象到另一个对象的流动抽象为”流“。流在使用前要被建立，使用后要被删除。
- 数据的输入与输出是通过I/O流来实现的，cin和cout是预定义的流类对象。cin用来处理标准输入，即键盘输入。cout用来处理标准输出，即屏幕输出。
- 从流中获取数据的操作称为提取操作，向流中添加数据的操作称为插入操作。

#### 预定义的插入和提取符

- ”<<“是预定义的插入符，作用在流类对象cout上便可以实现像标准输出设备输出。
  - cout << 表达式 << 表达式...
- 标准输入是将提取符作用在流类对象cin上。
  - cin >> 表达式 >> 表达式...
- 提取符可以连续写多个，每个后面跟一个表达式，该表达式通常是用于存放输入值的变量。例如：
  - int a, b;
  - cin >> a >> b; 

#### 常用的I/O流类库操纵符

![在这里插入图片描述](https://img-blog.csdnimg.cn/e5115c13cfbc467c8b7f32cb2a1819be.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


例：cout << setw(5) << setprecision(3) << 3.1415

## 选择结构

### if语句

#### IF语句的语法形式

- ###### if(表达式) 语句

  例：if(x > y) cout << x;

- if(表达式) 语句1 else 语句2

  例：if(x > y) cout << x;

  ​        else cout << y;

- if(表达式1) 语句1 

  else if (表达式2) 语句2

  else if (表达式3) 语句3

  ...

  else 语句n

![在这里插入图片描述](https://img-blog.csdnimg.cn/5819cf50522d403a8f8d3d2c5d279415.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


##### 多重选择结构——嵌套的if结构

例2-3：输入两个整数，比较两个数的大小。

```c++
#include <iostream>
using namespace std;
int main() {
	int x, y;
	cout << "Enter x and y:";
	cin >> x >> y;
	if (x != y)
		if (x > y)
			cout << "x > y" << endl;
		else
			cout << "x < y" << endl;
	else 
		cout << "x = y" << endl;
	return 0;
}
```

```
Enter x and y:5 8
x < y
```

```
Enter x and y:8 8
x = y
```

```
Enter x and y:12 8
x > y
```

##### 嵌套的if结构

- **语法形式：**

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/784d4e28db734f84bc56ba16c0b3efeb.png#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/9da582772a994bcea7009a01b30cb43a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


- **注意：**
  - 语句1、2、3、4可以是复合语句；
  - 每层的if与else配对，或用{}来确定层次关系。

### switch语句

例2-4：输入一个0~6的整数，转换成星期输出

```c++
#include <iostream>
using namespace std;
int main() {
	int day;
	cin >> day;
	switch (day) {
		case 0:cout << "Sunday" << endl; break;
		case 1:cout << "Monday" << endl; break;
		case 2:cout << "Tuesday" << endl; break;
		case 3:cout << "Wednesday" << endl; break;
		case 4:cout << "Thursday" << endl; break;
		case 5:cout << "Friday" << endl; break;
		case 6:cout << "Saturday" << endl; break;
		default:
			cout << "Day out of range Sunday ... Saturday" << endl; break;
	}
	return 0;
}
```

```
3
Wednesday
```

#### switch语句的语法：

- ##### 一般形式：

  **switch语句的语法：**

  switch(表达式){

  ​	case 常量表达式1:语句1

  ​	case 常量表达式2:语句2

  ​	...

  ​	case 常量表达式n:语句n

  ​	default:                  语句n+1

  }

- ##### 执行顺序：

  - 以case中的常量表达式值为入口标号，由此开始顺序执行。因此，每个case分支最后应该加break语句。

- ##### 注意：

  - case分支可包含多个语句，且不用{}。
  - 表达式、判断值都是int型或char型型。
  - 如果若干分支执行内容相同时可共用一组语句。

## 循环结构

### 循环结构——while语句

例2-5求自然数1~10之和

```c++
#include <iostream>
using namespace std;
int main() {
	int i = 0, sum = 0;
	while (i <= 10) {
		sum += i;
		i++;
	}
	cout << "sum = " << sum << endl;
	return 0;
}
```

```
sum = 55
```

- #### while语句的语法形式

  while(表达式) 语句

- #### 执行顺序

  先判断表达式的值，若为true时，执行语句。

![在这里插入图片描述](https://img-blog.csdnimg.cn/9214bca47d114de9a3e3935ffd23cdf1.png#pic_center)


### do-while语句

do 语句

while(表达式)

例2-6：输入一个数，将各位数字翻转后输出

```c++
#include <iostream>
using namespace std;
int main() {
	int n, right_digit, newnum = 0;
	cout << "Enter the number: ";
	cin >> n;
	cout << "The number is reverse order is: ";
	do {
		right_digit = n % 10;
		cout << right_digit;
		n /= 10;
	} while (n != 0);
	cout << endl;
	return 0;
}
```

```
Enter the number: 365
The number is reverse order is: 563
```

- #### do-while语句的语法形式

![在这里插入图片描述](https://img-blog.csdnimg.cn/c5fa4bdd3e304d3eaebf66d5f2688427.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


- #### 执行语句

  先执行循环体语句，后判断条件。

  表达式为true时，继续执行循环体。

例2-7用do-while语句编程，求自然数1~10之和

```c++
#include <iostream>
using namespace std;
int main() {
	int i = 1, sum = 0;
	 do{
		sum += i;
		i++;
	 } while (i <= 10);
	cout << "sum = " << sum << endl;
	return 0;
}
```

### for语句

例2-8：输入一个整数，求出他的所有因子

```c++
#include <iostream>
using namespace std;
int main() {
	int n;
	cout << "Enter a positive integer: ";
	cin >> n;
	cout << "Number " << n << " Factors ";
	for (int k = 1; k <= n; k++) {
		if (n % k == 0)
			cout << k << " ";
	}
	cout << endl;
	return 0;
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/a86107d23b5e4bcca08fe73b0682ba8f.png#pic_center)


#### for语句的另一种形式：

##### 范围for语句：

for(声明：表达式)

​	语句

### 嵌套的控制结构、其他控制语句

#### 循环结构与选择结构的嵌套

- 例2-10

  输入一系列整数，统计出正整数个数i和负整数个数j，读入0则结束。

- 分析：

  - 需要读入一系列整数，但是整数个数不定，要在每次读入之后进行判断，因此使用while循环最为合适。循环控制条件应该是n!=0。
  - 由于要判断数的正负并分别进行统计，所以需要在循环内部嵌入选择结构。

```c++
#include <iostream>
using namespace std;
int main() {
	int i = 0, j = 0, n;
	cout << "Enter some integers please (enter 0 to quit):" << endl;
	cin >> n;
	while (n != 0) {
		if (n > 0) i += 1;
		if (n < 0) j += 1;
		cin >> n;
	}
	cout << "Count of positive integers:" << i << endl;
	cout << "Count of negative integers:" << j << endl;
	return 0;
}
```

#### 其他控制语句

- ##### break语句

  使程序从循环体和switch语句中跳出，继续执行逻辑上的下一条语句。不宜用在别处。

- ##### continue语句

  结束本次循环，接着判断是否执行下一次循环

- goto语句

  使程序的执行流程跳转到语句标号所指定的语句。不提倡使用。

## 自定义类型

### 类型别名：为已有类型另外命名

- typedef 已有类型名 新类型名

  - 例：

    typedef double Area, Volume;

    typedef int Natural;

    Natrual i1,i2;

    Area a;

    Volume v;

- using 新类型名 = 已有类型名

  - 例：

    using Area = double

    using Volume = double

#### 枚举类型

问题：如何表示一星期的七天？

列出整数的子集，定义一个新类型：

0，1，2，3，4，5，6

- ##### 定义方式：

  将全部可取值一一列举出来

- ##### 语法形式：

  enum 枚举类型名 {变量值列表}

  enum Weekday {SUN, MON, TUE, WED, THU, FRI, SAT}

  默认情况下

  SUN=0，MON=1，TUE=2，......，SAT=6

##### C++包含两种枚举类型：

- 不限定作用域枚举类型：

  enum 枚举类型名 {变量值列表}

- 限定作用域的enum类将在后续章节介绍

**不限定作用域枚举类型说明：**

- 枚举元素是常量，不能对它们赋值

  - 例如有如下定义

    enum Weekday {SUN, MON, TUE, WED, THU, FRI, SAT}

- 不能写赋值表达式：SUN = 0

- 枚举元素具有默认值，它们依次为：0，1，2，......

- 也可以在**声明中另行指定枚举元素的值**

  如：enum Weekday {SUN=7, MON=1, TUE, WED, THU, FRI, SAT}

- 枚举值可以进行关系运算

- 整数值不能直接赋给枚举变量

  如需要将整数赋值给枚举变量，应进行强制类型转换

- 枚举值可以赋给整型变量

例2-11

- 设某次体育比赛的结果有四种可能：

  胜（WIN）、负（LOSE）、平局（TIE）、比赛取消（CANSEL）

  编写程序顺序输出这四种情况

- 分析：

  比赛结果只有四种可能，可以声明一个枚举类型

```c++
#include <iostream>
using namespace std;
enum GameResult{WIN, LOSE, TIE, CANSEL};
int main() {
	GameResult result;
	enum GameResult omit = CANSEL;
	for (int count = WIN; count <= CANSEL; count++) {
		result = GameResult(count);
		if (result == omit)
			cout << "The game was cancelled" << endl;
		else {
			cout << "The game was played";
			if (result == WIN) cout << "and we won!";
			if (result == LOSE) cout << "and we lost.";
			cout << endl;
		}
	}
	return 0;
}
```

```
The game was playedand we won!
The game was playedand we lost.
The game was played
The game was cancelled
```

#### auto类型与decltype类型

- auto：编译器通过初始值自动推断变量的类型

  例如：auto val = val1 + val2

  如果val1 + val2是int类型，则val是int类型

  如果val1 + val2是double类型，则val是double类型

- decltype：定义一个变量与某一表达式的类型相同，但并不用该表达式初始化变量

  表示j以2作为初始值，类型与i一致

## 实验二：C++简单程序设计（下）

例题一

```c++
输入并运行例题2-7，即：

用do-while语句编程，求自然数1~10之和。

#include <iostream>
using namespace std;
int main() {
	int i = 1, sum = 0;
	 do{
		sum += i;
		i++;
	 } while (i <= 10);
	cout << "sum = " << sum << endl;
	return 0;
}
```

```c++
#include <iostream>
using namespace std;
int main() {
	int sum = 0;
	for(i = 1; i <=10; i++)
    //
    {
		sum += i;
	}
	cout << "sum = " << sum << endl;
	return 0;
}
```

例题二

编写计算图形的面积。

程序可计算圆形、长方形、正方形的面积，运行时先提示用户选择图形的类型，然后，对圆形要求用户输入半径值，对长方形要求用户输入长和宽的值，对正方形要求用户输入边长的值，计算出面积的值将其显示出来。

```c++
#include <iostream>
using namespace std;
const float PI = 3.1416;
int main() {
	int iType;
	float radius, a, b, area;
	cout << "图形的类型？（1-圆形 2-长方形 3-正方形）：";
	cin >> iType;
	switch (iType) {
	case 1:
		cout << "圆的半径为：";
		cin >> radius;
		area = PI * radius * radius;
		cout << "面积为：" << area << endl;
		break;
	case 2:
		cout << "矩形的长为："; 
		cin >> a;
		cout << "矩形的宽为：";
		cin >> b;
		area = a * b;
		cout << "面积为：" << area << endl;
		break;
	case 3:
		cout << "正方形的边长为：";
		cin >> a;
		area = a * a;
		cout << "面积为：" << area << endl;
		break;
	default:
		cout << "不是合法的输入值！" << endl;
	}
	return 0;
}
```

```
图形的类型？（1-圆形 2-长方形 3-正方形）：2
矩形的长为：2
矩形的宽为：8
面积为：16
```

例题三

声明一个表示时间的结构体

可以精确表示年、月、日、小时、分、秒；

提示用户输入年、月、日、小时、分、秒的值，然后完整地显示出来。

```c++
#include <iostream>
using namespace std;
struct MyTimeStruct {
	unsigned int year;
	unsigned int month;
	unsigned int day;
	unsigned int hour;
	unsigned int min;
	unsigned int sec;
};
int main() {
	MyTimeStruct myTime = { 2022, 2, 14, 22, 19, 0 };
	cout << "please input year: " << endl;
	cin >> myTime.year;
	cout << "please input month: " << endl;
	cin >> myTime.month;
	cout << "please input day: " << endl;
	cin >> myTime.day;
	cout << "please input hour: " << endl;
	cin >> myTime.hour;
	cout << "please input min: " << endl;
	cin >> myTime.min;
	cout << "please input sec: " << endl;
	cin >> myTime.sec;
	cout << "the time is set to :" << myTime.year << "/"
								   << myTime.month << "/"
		                           << myTime.day << " "
		                           << myTime.hour << ":"
		                           << myTime.min << ":"
		                           << myTime.sec << endl;
}
```

```
please input year:
2022
please input month:
2
please input day:
14
please input hour:
22
please input min:
38
please input sec:
0
the time is set to :2022/2/14 22:38:0
```


