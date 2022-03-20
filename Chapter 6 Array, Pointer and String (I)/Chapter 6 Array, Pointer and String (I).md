## 第6章 数组、指针与字符串（一）

### 数组的定义与初始化

#### 数组的定义与使用

数组是具有一定顺序关系的若干相同类型变量的集合体，组成数组的变量成为该数组的元素。

##### 数组的定义

```c++
类型说明符 数组名[常量表达式][常量表达式]......;
```

数组名的构成方法与一般变量名相同。

- 例如：`int a[10];`

  表示a为整型数组，有10个元素：a[0]...a[9]

- 例如：`int a[5][3];`

  表示a为整型二维数组，其中第一维有5个下标（0~4），第二维有3个下标（0~2），数组的元素个数为15，可以用于存放5行3列的整型数据表格。

##### 数组元素的使用

- 数组必须先定义，后使用。

- 可以逐个引用数组元素。

- 例如：

  ```c++
  a[0] = a[5] + a[7] - a[2*3]
  b[1][2] = a[2][3]/2
  ```

例6-1

```c++
#include <iostream>
using namespace std;
int main(){
    int a[10], b[10];
    for(int i = 0; i < 10; i++){
        a[i] = i * 2 - 1;
        b[10 - i - 1] = a[i];
    }
    for(int i = 0; i < 10; i++){
        cout << "a[" << i << "] = " << a[i] << " ";
        cout << "b[" << i << "] = " << b[i] << endl;
    }
    return 0;
}
```

#### 数组的储存与初始化

##### 一维数组的存储

数组元素在内存中顺次存放，它们的地址是连续的。元素间物理地址上的相邻，对应着逻辑次序上的相邻。

例如：

```c++
int a[10];
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/a879a40a2a2449ada8ab1670f1ca970a.png#pic_center)


##### 一维数组的初始化

- 列出全部元素的初始值

  例如：`static int a[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};`

- 可以只给一部分元素指定初值

  例如：`static int a[10] = {0, 1, 2, 3, 4};`

- 列出全部数组元素初值时，可以不指定数组长度

  例如：`static int a[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};`

##### 二维数组的存储

- 按行存放

  例如：`float a[3][4];`

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/714d183f90384197a61e4df5ec6a4651.png#pic_center)


  其中数组a的存储顺序为：

  a00 a01 a02 a03 a10 a11 a12 a13 a20 a21 a22 a23

##### 二维数组的初始化

- 将所有初值写在一个{}内，按顺序初始化

  例如：`static int a[3][4] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12};`

- 分行列出二维数组元素的初值

  例如：`static int a[3][4] = {{1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12};`

- 可以只对部分元素初始化

  例如：`static int a[3][4] = {{1}, {0, 6}, {0, 0, 11}};`

- 列出全部初始值时，第一维下标个数可以省略

  例如：`static int a[][4] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12};`

  或`static int a[][4] = {{1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12};`

- 如果不做任何初始化，局部作用域的非静态数组中存在垃圾数据，static数组中的数据默认初始化为0

- 如果只对部分元素初始化，剩下的未显式初始化的元素，将自动被初始化为零

例：求Fibonacci数列的前20项，将结果存放于数组中

```c++
#include <iostream>
using namespace std;
int main(){
    int f[20] = {1, 1};
    for(int i = 2; i < 20; i++)
        f[i] = f[i - 2] + f[i - 1];
    for(int i = 0; i < 20; i++){
        if(i % 5 == 0) cout << endl;
        cout.width(12);//设置输出宽度为12
        cout << f[i];
    }
    return 0;
}
```

```
           1           1           2           3           5
           8          13          21          34          55
          89         144         233         377         610
         987        1597        2584        4181        6765
```

#### 一维数组应用举例

- 循环从键盘读入若干组选择题答案，计算并输出每组答案的正确率，直到输入ctrl+z为止。
- 每组连续输入5个答案，每个答案可以是‘a’..‘d’。

```c++
#include <iostream>
using namespace std;
int main(){
    const char key[ ]{'a', 'c', 'b', 'a', 'd'};
    const int NUM_QUES = 5;
    char c;
    int ques = 0, numCorrect = 0;
    cout << "Enter the " << NUM_QUES << " question test:" << endl;
    while(cin.get(c)){
        if(c != '\n'){
            if( c == key[ques]){
                numCorrect++; cout <<" ";
            }else
                cout << "*";
            ques++;
        }else{
            cout << " Score " << static_cast<float>(numCorrect)/NUM_QUES*100 << "%";
            ques = 0; numCorrect = 0;cout << endl;
        }
    }
    return 0;
}
```

```
Enter the 5 question test:
acbba
   ** Score 60%
acbad
      Score 100%
abbda
 * ** Score 40%
bdcba
***** Score 0%
```

### 数组作为函数的参数

- 数组元素作实参，与单个变量一样。
- 数组名作参数，形、实参数都应是数组名，类型要一样，传送的是数组首地址。对形参数组的改变会直接直接影响到实参数组。

例6-2 使用数组名作为函数参数

主函数中初始化一个二维数组，表示一个矩阵，并将每个元素都输出，然后调用子函数，分别计算每一行的元素之和，将和直接存放在每行的第一个元素中，返回主函数之后输出各行元素的和。

```c++
#include <iostream>
using namespace std;
void rowSum(int a[][4], int nRow){
    for(int i = 0, i < nRow; i++){
        for(int j = 1; j < 4; j++){
            a[i]a[0] += a[i]a[j];
        }
    }
}
int main(){
    int table[3][4] = {{1, 2, 3, 4}, {2, 3, 4, 5}, {3, 4,5, 6}};
    for(int i = 0, i < 3; i++){
        for(int j = 0; j < 4; j++)
            cout << table[i][j] << " ";
            cout << endl;
    }
    rowSum(table, 3);
    for(int i = 0; i < 3; i++)
        cout << "Sum of row" << i << "is" << table[i][0] << endl;
    return 0;
}
```

### 对象数组

#### 对象数组的定义与访问

- 定义对象数组

  类名 数组名[元素个数];

- 访问对象数组元素

  访问下标访问：数组名[下标].成员名

#### 对象数组初始化

- 数组中每一个元素对象被创建时，系统都会调用类构造函数初始化该对象。

- 通过初始化列表赋值。

  例：`Point a[2] = {Point(1, 2), Point(3, 4)};`

- 如果没有为数组元素指定显式初始值，数组元素便使用默认值初始化（调用默认构造函数）。

#### 数组元素的构造和析构

- 构造数组时，元素所属的类未声明构造函数，则采用默认构造函数。
- 各元素对象的初值要求为相同的值时，可以声明具有默认形参值的构造函数。
- 各元素对象的初值要求为不同的值时，需要声明带形参的构造函数。
- 当数组中每一个对象被删除时，系统都要调用一次析构函数。

例6-3 对象数组应用举例

```c++
//Point.h

#ifndef _POINT_H
#define _POINT_H

class Point{
public:
    Point();
    Point(int x, int y);
    ~Point();
    void move(int newX, int newY);
    int getX() const{return x;}
    int getY() const{return y;}
    static void showCount();
private:
    int x, y;
};

#endif //_POINT_H

```

```c++
//Point.cpp
#include <iostream>
#include "Point.h"
using namespace std;
Point::Point(): x(0), y(0){
    cout << "Default Constructor called." << endl;
}
Point::Point(int x, int y): x(x), y(y){
    cout << "Constructor called." << endl;
}
Point::~Point(){
    cout << "Destructor called." << endl;
}
void Point::move(int newX, int newY) {
    cout << "Moving the Point to (" << newX << ", " << newY << ")" << endl;
    x = newX;
    y = newY;
}
```

```c++
//6-3.cpp
#include "Point.h"
#include <iostream>
using namespace std;
int main(){
    cout << "Entering main.." << endl;
    Point a[2];
    for(int i = 0; i < 2; i++)
        a[i].move(i + 10, i + 20);
    cout << "Exiting main.." << endl;
    return 0;
}
```

```
Entering main..
Default Constructor called.
Default Constructor called.
Moving the Point to (10, 20)
Moving the Point to (11, 21)
Exiting main..
Destructor called.
Destructor called.
```

### 基于范围的for循环

```c++
int main(){
    int array[3] = {1, 2, 3};
    int *p;
    for(p = array; p < array + sizeof(array) / sizeof(int); ++p)
    {
        *p += 2;
        std::cout << *p << std:endl;
    }
	return 0;
}
```

```c++
int main(){
    int array[3] = {1, 2, 3};
    for(int & e: array)
    {
        e += 2;
        std::cout << e << std:endl;
    }
	return 0;
}
```

### 指针的定义和运算

#### 指针的概念、定义和指针运算

##### 内存空间的访问方式：

- 通过变量名访问

- 通知地址访问

##### 指针的概念

- 指针：内存地址，用于间接访问内存单元
- 指针变量：用于存放地址的变量

##### 指针变量的定义

- 例：

  ```c++
  static int i;
  ```

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/a3d0926157274397b945d7424d8127a2.png#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/8b64b523733e440a8c97c37575efc475.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_9,color_FFFFFF,t_70,g_se,x_16#pic_center)


- 例：

  ```c++
  *ptr = 3;
  ```

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/fc5f2c527a2c46e28957a58a77043070.png#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/8deef1c3bc53443aa64195a06698323e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_8,color_FFFFFF,t_70,g_se,x_16#pic_center)


##### 与地址相关的运算—“*”和“&”

- 指针运算符：*
- 地址运算符：&

#### 指针的初始化和赋值

##### 指针变量的初始化

- 语法形式

  存储类型 数据类型 *指针名 = 初始地址;

- 例：

  ```c++
  int *pa = &a;
  ```

- 注意事项

  用变量地址作为初值时，该变量必须在指针初始化之前已经声明过，且变量类型应与指针类型一致。

  可以用一个已有合法值的指针去初始化另一个指针变量。

  不要用一个内部非静态变量去初始化static指针。

##### 指针变量的赋值运算

- 语法形式 指针 = 地址

- 注意：

  “地址”中存放的数据类型与指针类型必须相符

  向指针变量赋的值必须是地址常量或变量，不能是普通整数

- 例如：

  通过地址运算“&”求得已定义的变量和对象的起始地址

  动态内存分配成功时返回的地址

- 例外：整数0可以赋给指针，表示空指针。

- 允许定义或声明指向void类型的指针。该指针可以被赋予任何类型对象的地址。

  例：`void *general;`

##### 指针空值nullptr

- C++11使用nullptr关键字，是表达更准确，类型安全的空指针

例6-5 指针的定义、赋值与使用

```c++
#include <iostream>
using namespace std;
int main(){
    int i;
    int *ptr = &i;
    i = 10;
    cout << "i = " << i << endl;
    cout << "*ptr = " << *ptr << endl;
    return 0;
}
```

```
i = 10
*ptr = 10
```

例6-6 void类型指针的使用

```c++
#include <iostream>
using namespace std;
int main(){
	//!void voidObject;错，不能声明void类型的变量
    void *pv;
    int i = 5;
    pv = &i;
    int *pint = static_cast<int *>(pv);
    cout << "*pint = " << *pint << endl;
    return 0;
}
```

##### 指向常量的指针

- const指针

- 不能通过指向常量的指针改变为所指对象的值，但指针本身可以改变，可以指向另外的对象。

- 例：

  ```c++
  int a;
  const int *p1 = &a;
  int b;
  p1 = &b;
  *p1 = 1//编译时出错，不能通过p1改变所指的对象
  ```

##### 指针类型的常量

- 若声明指针常量，则指针本身的值不能被改变。

- 例

  ```c++
  int a;
  int * const p2 = &a;
  p2 = &b;//错误，p2是指针常量，值不能改变
  ```

#### 指针的算术运算、关系运算

##### 指针类型的算术运算

- 指针与整数的加减运算

- 指针++，--运算

  

- 指针p加上或减去n

  - 其意义是指针当前指向位置的前方或后方第n个数据的起始位置。

- 指针的++、--运算

  - 意义是指向下一个或前一个完整数据的起始.

- 运算的结果值取决于指针指向的数据类型，总是指向一个完整数据的起始位置。

- 当指针指向连续存储的同类型数据时，指针与整数的加减运算和自增自减运算才有意义。

###### 指针与整数相加的含义

![在这里插入图片描述](https://img-blog.csdnimg.cn/6574fc353b694eb4bdd2ad65d9c6c5f3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_13,color_FFFFFF,t_70,g_se,x_16#pic_center)


##### 指针类型的关系运算

- 指向相同类型数据的指针之间可以进行各种关系运算。
- 指向相同类型数据的指针，以及指针与一般整数变量之间的关系运算是无意义的。
- 指针可以和零之间进行等于或不等于的关系运算。
  - 例如：`p == 0`或`p != 0`

### 综合实例

个人银行账户管理程序

- 一个活期储蓄账户包括：
  - 信息：
    - 账号（id）、余额（balance）、年利率（rate）等
  - 操作：
    - 显式账户信息（show）、存款（deposit）、取款（withdraw）、结算利息（settle）等

![在这里插入图片描述](https://img-blog.csdnimg.cn/5126af9be53440d7b19993b1f34a6b80.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_14,color_FFFFFF,t_70,g_se,x_16#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/9762cc983c4948798e293275f6018a06.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/020aea668f6b4d01b303da5d6a846588.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


设计难点：利息的计算1

- 实现该类的难点在于利息的计算。由于账户的余额是不断变化的，因此：

  - 余额 × 年利率 = 年利？ NO!

  - 一年当中每天的余额累积起来/一年的总天数=日均余额

    <u>日均余额 × 年利率=年利</u> YES!

- 例如：如果年利率是1.5%，某账户第5天存入5000元，第45天存入5500元，第90天结算利息。

  - 它第5天到第45天之间的余额为5000元（持续40天）
  - 它第45天到第90天之间的余额为10500元（持续45天）
  - 90天的利息是<u>（40×5000 + 45×10500）×1.5% / 365 = 27.64元</u>。

设计难点：利息的计算2

- 为了计算余额的按日累计值，SavingsAccount引入了：

  - 私有数据成员<u>lastDate</u>：存储上一次余额变动的日期
  - 私有数据成员<u>accumulation</u>：存储上次计算利息以后直到最近一次余额变动时余额按日累加的值
  - 私有成员函数<u>accumulation</u>：计算截至指定日期的账户余额按日累计值。

- 当余额变动时，需要做的是将变动前的余额与该余额所持续的天数相乘，累加到accumulation中，再修改lastDate。

  - ```c++
    accumulation + balance * (date - lastDate);
    ```

![在这里插入图片描述](https://img-blog.csdnimg.cn/207c3c078d434bea94d93a2a35147568.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_13,color_FFFFFF,t_70,g_se,x_16#pic_center)


```c++
#include <iostream>
#include <cmath>
using namespace std;
class SavingsAccount {
private:
    int id;
    double balance;
    double rate;
    int lastDate;
    double accumulation;
    void record(int date, double amount);
    double accumulate(int date) const{
      return accumulation + balance * (date - lastDate);
    }
public:
    SavingsAccount (int date, int id, double rate);
    int getId(){return id;}
    double getBalance(){return balance;}
    double getRate(){return rate;}
    void deposit(int date, double amount);
    void withdraw(int  date, double amount);
    void settle(int date);
    void show();
};
SavingsAccount::SavingsAccount(int date, int id, double rate):id(id), balance(0), rate(rate), lastDate(date), accumulation(0){
    cout << date << "\t#" << id << " is created" << endl;
} 
void SavingsAccount ::record(int date, double amount){
    accumulation = accumulate(date);
    lastDate = date;
    amount = floor(amount * 100 + 0.5) / 100;//保留小数点后两位
    balance += amount;
}
...
void SavingsAccount::settle(int date){
        double interest = accumulate(date) * rate / 365
        if(interest != 0){
            record(date, amount);
        accumulation = 0;
        }
}
int main(){
    SavingsAccount sa0(1, 21325302, 0.015);
    SavingsAccount sa1(1, 58320212, 0.015);
    sa0.deposit(5 ,5000);
    sa1.deposit(25 ,10000);
    sa0.deposit(45 ,5500);
    sa1.withdraw(60 ,4000);
    sa0.settle(90);
    sa1.settle(90);
    sa0.show(); cout << endl;
    sa1.show(); cout << endl;
    return 0;
}
```

### 实验六(上)

例题一：

编写矩阵转置函数，输入参数为3×3整型数组。

编写main()函数实现输入、输出。

提示;

使用循环语句实现矩阵元素的行列对调，注意在循环语句中究竟需要对哪些元素进行操作

```c++
#include <iostream>
using namespace std;
void swap(int& a, int& b){
    int temp = a;
    a = b;
    b = temp;
}
int main(){
    int a[3][3];
    cout << "输入9个整数作为矩阵元素值" << endl;
    for(i = 0; i < 3; i++)
        for(int j = 0; j < 3; j++)
            cin >> a[i][j];
        cout << "初始矩阵 : " << endl;
    for(i = 0; i < 3; i++){
        for(int j = 0; j < 3; j++)
            cout << a[i][j] << ' ';
        cout << endl;
    }
    for(i = 0; i < 3; i++){
        for(int j = 0; j < 3; j++)
            swap(a[i][j], a[j][i]);
    cout << "转置后的矩阵 : " <<  endl;
    for(i = 0; i < 3; i++){
        for(int j = 0; j < 3; j++)
            cout << a[i][j] << ' ';
        cout << endl;
    }
    return 0;
}
```

```
输入9个整数作为矩阵元素值
1 2 3 4 5 6 7 8 9
初始矩阵 :
1 2 3
4 5 6
7 8 9
转置后的矩阵 :
1 4 7
2 5 8
3 6 9
```

例题二：

声明一个Employee类，其中包括姓名、街道地址、城市和邮编等属性，以及change_name()和display()等函数。

display()显式姓名、街道地址和邮编等属性；

change_name()改变对象的姓名属性，实现并测试这个类。

```c++
//employee.h
#ifndef EMPLOYEE_H_
#def EMPLOYEE_H_

#include <iostream>
using namespace std;

class Employee{
    char* name;
    char* address;
    char* city;
    char* code;
public:
    Employee(char* n = " ", char* add = " ",  char* ct = " ", char* cd = " "): name(n), address(add), city(ct), code(cd){}
    void display(){
        cout << "name: " << name << endl;
        cout << "address: " << address << endl;
        cout << "city: " << city << endl;
        cout << "code: " << code << endl;
    }
    void change_name(char* nm){
        name = nm;
    }
};

#endif
```

```c++
#include <iostream>
#include employee.h
using namespace std;
int main(){
    Employee e("Wang Er", "Haidian", "Beijing", "100084");
    e.display();
    e.change_name("Li San");
    e.display();
    return 0;
}
```


