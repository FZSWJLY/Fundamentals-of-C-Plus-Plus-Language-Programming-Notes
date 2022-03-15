## 第4章 类与对象

### 类和对象

#### 类和对象的定义

对象是现实中的对象在程序中的模拟

类是同一类对象的抽象

对象是类的实例

定义类的对象，才可以通过对象使用类中定义的功能。

#### 类定义的语法形式

```c++
class 类名称
{
    public:
    	公有成员（外部接口）
    private:
    	私有成员
    protected:
    	保护性成员
}；
```

- 为数据成员设置类内初始值
- 用于初始化数据成员

#### 类内初始值举例

![在这里插入图片描述](https://img-blog.csdnimg.cn/a0acb31eccb142179c6f8433d511abd8.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


#### 类成员的访问控制

- 公有类型成员
- 私有类型成员
- 保护类型成员

#### 公有类型成员

- 在关键字public后面声明，它们是类与外部的接口，任何外部函数都可以访问公有类型数据和函数。

#### 私有类型成员

- 在关键字private后面声明，只允许本类中的函数访问，而类外部的任何函数都不能访问。
- 如果紧跟在类名称的后面声明私有成员，则关键字private可以省略。

#### 保护类型成员

- 与private类似，其差别表现在继承与派生时对派生类的影响不同，详见第七章。

- 对象定义的语法

  类名 对象名;

- 例：

  `Clock myClock;`

类中成员之间直接使用成员名互相访问

从类外访问成员使用“对象名.成员名”方式访问public成员

#### 类的成员函数

- 在类中声明函数原型；
- 可以在类外给出函数体实现，并在函数名前使用类名加以限定；
- 也可以直接在类中给出函数体，形成内联成员函数；
- 允许声明重载函数和带默认参数值的函数。

#### 内联成员函数

- 为了提高运行时的效率，对于较简单的函数可以声明为内联形式。
- 内联函数体中不要有复杂结构（如循环语句和switch语句）。
- 在类中声明内联函数的方式：
  - 将函数体放在类的声明中
  - 使用inline关键字

### 类和对象的程序举例

```c++
#include<iostream>
using namespace std;
class Clock{
public:
    void setTime(int newH = 0, int newM = 0, int newS = 0);
    void showTime();
private:
    int hour, minute, second;
};
void Clock::setTime(int newH, int newM, int newS){
    hour = newH;
    minute = newM;
    second = newS;
}
void Clock::showTime(){
    cout << hour << ":" << minute << ":" << second;
}
int main(){
    Clock myClock;
    myClock.setTime(8, 30 ,30);
    myClock.showTime();
    return 0;
}
```

```
8:30:30
```

### 构造函数

#### 构造函数基本概念

##### 构造函数

- 类中的特殊函数
- 用于描述初始化算法

#### 构造函数的作用

- 在对象被创建时使用特定的值构造对象，将对象初始化为一个特定的初始状态。
- 例如：
  - 希望构造一个Clock类对象时，将初始时间设为0：0：0，就可以通过构造函数来设置。

#### 构造函数的形式

- 函数名与类名相同
- 不能定义返回值类型，也不能有return语句
- 可以有形式参数，也可以没有形式参数
- 可以是内联函数
- 可以重载
- 可以带默认参数值

#### 构造函数的调用时机

- 在对象创建时被自动调用

- 例如：

  `Clock myClock(0, 0, 0)`

#### 默认构造函数

- 调用时可以不需要实参的构造函数
  - 参数表为空的构造函数
  - 全部参数都有默认值的构造函数

下面两个都是默认构造函数，如在类中同时出现，将产生编译错误；

```c++
Clock();
```

```c++
Clock(int newH = 0, int newM = 0, int newS = 0);
```

#### 隐含生成的构造函数

- 如果程序中未定义构造函数，编译器将自动生成一个**默认构造函数**
  - 参数列表为空，不为数据成员设置初始值；
  - 如果类内定义了成员的初始值，则以默认方式初始化；
  - 基本类型的数据默认初始化的值是不确定的。

#### “=default”

- 如果程序中已定义构造函数，默认情况下编译器就不再隐含生成默认构造函数。**如果此时依然希望编译器隐含生成默认构造函数，可以使用“=default”。**

- 例：

  ```c++
  class Clock{
  public:
      Clock() = default;//指示编译器提供默认构造函数
      Clock(int newH, int newM, int newS);//构造函数
  private:
      int hour, minute, second;
  };
  ```

#### 构造函数例题（1）——例4-1

```c++
class Clock{
public:
    setTime(int newH, int newM, int newS);//构造函数
    void showTime();
private:
    int hour, minute, second;
};
//构造函数的实现：
Clock::Clock(int newH, int newM, int newS){
    hour(newH), minute(newM), second(newS){
}
//其他函数实现同4_1
int main(){
    Clock c(0, 0, 0);//自动调用构造函数
    c.showtime();
    return 0;
}
```

#### 构造函数例题（2）——例4-2

```c++
class Clock{
public:
    Clock(int newH, int newM, int newS);//构造函数
    Clock();//默认构造函数
    setTime(int newH, int newM, int newS);
    void showTime();
private:
    int hour, minute, second;
};
Clock::Clock():hour(0), minute(0), second(0){
}
//默认构造函数
//其他函数实现同前
int main(){
    Clock c1(0, 0, 0);//调用有参数的构造函数
    Clock c2;//调用无参数的构造函数
    ......
}
```

#### 委托构造函数

- 委托构造函数使用类的其他构造函数执行初始化过程

- 例如：

  ```c++
  Clock(int newH, int newM, int newS)：
  hour(newH), MINUE(NewM), second(newS){
      
  }
  Clock():Clock(0, 0, 0){}
  ```

#### 复制构造函数

##### 复制构造函数定义

- 复制构造函数是一种特殊的构造函数，其形参为本类的对象引用。作用是用一个已存在的对象去初始化同类型的新对象。

- ```c++
  class 类名{
  public:    
      类名(形参);//构造函数
      类名(const 类名 &对象名);//复制构造函数
      //...
  };
  类名::类(const 类名 &对象名)//复制构造函数的实现
  {函数体}
  ```

##### 复制构造函数被调用的三种情况

- 定义一个对象时，以本类另一个对象作为初始值，发生复制构造；
- 如果函数的形参是类的对象，调用函数时，将使用实参对象初始化形参对象，发生复制构造；
- 如果函数的返回值是类的对象，函数执行完成返回主调函数时，将使用return语句中的对象初始化一个临时无名对象，传递给主调函数，此时发生复制构造。
  - 这种情况也可以通过移动构造避免不必要的复制（第6章介绍）

##### 隐含的复制构造函数

- 如果程序员没有为类声明拷贝初始化构造函数，则编译器自己生成一个隐含的复制构造函数。
- 这个构造函数执行的功能是：用初始化对象的每个数据成员，初始化将要建立的对象的对应数据成员。

##### “=delete”

如果不希望对象被复制构造

- C++98做法：将复制构造函数声明为private，并且不提供函数的实现。

- C++11做法：**用“=delete”指示编译器不生成默认复制构造函数。**

  - 例：

    ```c++
    class Point{//Point类的定义
    public:
        Point(int xx = 0, int yy = 0){x = xx; y = yy;}//构造函数，内联
        Point(const Point& p) = delete;//指示编译器不生成默认复制构造函数
    private:
        int x, y;//私有数据
    };
    ```

#### 复制构造函数调用举例

```c++
#include <iostream>
using namespace std;
class Point{
public:
     Point(int xx = 0, int yy =0){
        x = xx;
        y = yy;
    }
    Point(Point &p);
    int getX(){
        return x;
    }
    int getY(){
        return y;
    }
private:
    int x, y;
};
Point::Point(const Point &p){
    x = p.x;
    y = p.y;
    cout << "Calling the copy constructor" << endl;
}
void fun1(Point p){
    cout << p.getX() << endl;
}
Point fun2(){
    Point a;
    return a;
}
int main(){
    Point a;
    Point b(a);
    cout << b.getX() << endl;
    fun1(b);
    b = fun2();
    cout << b.getX() << endl;
    return 0;
}
```

### 析构函数

析构函数完成对象被删除前的一些清理工作

如果程序中未声明析构函数，编译器将自动产生一个默认的析构函数，其函数体为空。

- 析构函数的原型 `~类名();`
- 析构函数没有参数，没有返回类型

```c++
#include <iostream>
using namespace std;
class Point{
public:
    Point(int xx, int yy);
    ~Point();
    //...原型
private：
    int x, y;
};
Point::Point(int xx, int yy){
    x = xx;
    y = yy;
}
Point::~Ponit{
    
}
//...其他函数的实现略
```

### 类的组合

#### 类的组合

**组合的概念**

- 类中的成员是另一个类的对象。
- 可以在已有抽象的基础上实现更复杂的抽象。

##### 类组合的构造函数设计

- 原则：不仅要对本类的基本类型成员数据初始化，也要对对象成员初始化。

- 声明形式：

  ```c++
  类名::类名(对象成员所需的形参, 本类成员形参):
  	对象1(参数), 对象2(参数),......
  {
  	//函数体其他语句
  }
  ```

##### 构造组合类对象时的初始化次序

- 首先对构造函数初始化列表中列出的成员（包括基本类型成员和对象成员）进行初始化，初始化次序是成员在类体中定义的次序。
  - 成员对象构造函数调用顺序：按对象成员的定义顺序，先声明先构造。
  - 初始化列表中未出现的成员对象，调用默认构造函数（即无形参的）初始化
- 处理完初始化列表之后，再执行构造函数的函数体。

#### 类的组合程序举例

```c++
#include <iostream>
#include <cmath>
using namespace std;
class Point{
public:
    Point(int xx = 0, int yy =0){
        x = xx;
        y = yy;
    }
    Point(Point &p);
    int getX(){
        return x;
    }
    int getY(){
        return y;
    }
private:
    int x, y;
};
Point::Point(Point &p){
    x = p.x;
    y = p.y;
    cout << "Calling the copy constructor of Point" << endl;
}
class Line{
public:
    Line(Point xp1, Point xp2);
    Line(Line &l);
    double getLen(){
        return len;
    }
private:
    Point p1, p2;
    double len;
};
Line::Line(Point xp1, Point xp2){
    cout << "Calling the copy constructor of Line" << endl;
    double x = static_cast<double>(p1.getX() - p2.getX());
    double y = static_cast<double>(p1.getY() - p2.getY());
    len = sqrt(x * x + y * y);
}
Line::Line(Line &l): p1(l.p1), p2(l.p2){
    cout << "Calling the copy constructor of Line" << endl;
    len = l.len;
}
int main(){
    Point myp1(1, 1), myp2(4, 5);
    Line line(myp1, myp2);
    Line line2(line);
    cout << "The length of the line is: ";
    cout << line.getLen() << endl;
    cout << "The length of the line2 is: ";
    cout << line2.getLen() << endl;
    return 0;
}
```

### 前向引用声明

- 类先声明，后使用
- 如果需要在某个类的声明之前，引用该类，则应进行前向引用声明。
- 前向引用声明只为程序引入标识符，但具体声明在其他地方。

例：

```c++
class B;//前向引用声明
class A{
public:
    void f(B b);
};
class B{
public:
    void g(A a);
};
```

#### 前向引用声明注意事项

- 在提供一个完整的类声明之前，不能声明该类的对象，也不能在内联成员函数中使用该类的对象。
- 当使用前向引用声明时，只能使用被声明的符号，而不能涉及类的任何细节。

例：

```c++
class Fred;//前向引用声明
class Barney{
    Fred x;//错误：类Fred的声明尚不完善
};
class Fred{
    Barney y;
};
```

### UML简介

#### UML有三个基本的部分

- 事物（Things）
- 关系（Relationships）
- 图（Diagrams）

#### 类图

举例

- Clock类的完整表示

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/654699f240f44c0f8d761c2f4dc5bb97.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


- Clock类的简洁表示

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/87f41208a5fe4d78817cac8a696dde1a.png#pic_center)


#### 对象图

举例

- Clock类对象的完整表示

![在这里插入图片描述](https://img-blog.csdnimg.cn/8befc3e803ab42adb8e82911df918e55.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


- Clock类对象的简洁表示

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/6afc339de00f402b92a0b579189ee1d2.png#pic_center)


#### 依赖关系

![在这里插入图片描述](https://img-blog.csdnimg.cn/ecead10bb7cd44cea4e75e751c23a06e.png#pic_center)


#### 作用关系——关联

![在这里插入图片描述](https://img-blog.csdnimg.cn/eb3dca713ee74511bb18d6c1b25a0edd.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


#### 包含关系——聚集

![在这里插入图片描述](https://img-blog.csdnimg.cn/0141aa26d9694b5681c5300811154a3a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


- 共享聚集：部分可以参加多个整体。
- 组成聚集（组合）：整体拥有各个部分，整体与部分共存，如果整体不存在了，部分也就不存在了。

例4-5 用UML描述例4-4中Line类和Point类的关系。

![在这里插入图片描述](https://img-blog.csdnimg.cn/aac3a46a1aac46f3976f0e7bdc0e9747.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


#### 继承关系——泛化

![在这里插入图片描述](https://img-blog.csdnimg.cn/527acfe4ccc44df98682753696d099e2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_18,color_FFFFFF,t_70,g_se,x_16#pic_center)


#### 注释

![在这里插入图片描述](https://img-blog.csdnimg.cn/d103d07fe45f44a0b71b85ecd6710deb.png#pic_center)


例4-6 带有注释的Line类和Point类的关系

![在这里插入图片描述](https://img-blog.csdnimg.cn/cc65c9cbd08044d9b1e0f763f5a2b9bb.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


### 结构体与联合体

#### 结构体（例4-7）

- 结构体是一种特殊形态的类。
- 与类的唯一区别：
  - 类的缺省访问权限是private，结构体的缺省访问权限public。
- 什么时候用结构体而不用类
  - 定义主要用来保存数据、而没有什么操作的类型。
  - 人们习惯将结构体的数据成员设为公有，因此这时用结构体方便。

##### 结构体定义

```c++
struct 结构体名称{
    公有成员
protected:
    保护性成员
private:
    私有成员
};
```

结构体中可以有数据成员和函数成员

##### 结构体的初始化

如果：

- 一个结构体的全部数据成员都是公共成员；
- 没有用户定义的构造函数；
- 没有基类和虚函数（基类和虚函数第7章介绍）

这个结构体的变量可以用下面的语法形式初始化：

**类型名 变量名 = {成员数据1初值， 成员数据2初值， ......}；**

```c++
#include <iostream>
#include <iomanip>
#include <string>
using namespace std;
struct Student{
    int num;
    string name;
    char sex;
    int age;
};
int main(){
    Student stu = {97001, "Lin Lin,", 'F', 19};
    cout << "Num: " << stu.num << endl;
    cout << "Name: " << stu.name << endl;
    cout << "Sex: " << stu.sex << endl;
    cout << "Age: " << stu.age << endl;
    return 0;
}
```

```
Num: 97001
Name: Lin Lin,
Sex: F
Age: 19
```

#### 联合体（例4-8）

##### 定义形式

```c++
union 结构体名称{
    公有成员
protected:
    保护性成员
private:
    私有成员
};
```

##### 特点

- 成员共用同一组内存单元
- 任何两个成员不会同时有效

##### 联合体的内存分配

举例说明：

```c++
union Mark{
    char grade;
    bool pass;
    int percent;
}
```

##### 无名联合

例：

```c++
union{
    int i;
    float f;
}
```

在这个程序中可以这样使用

```c++
i = 10;
f = 2.2;
```

例4-8使用联合体保存成绩信息，并且输出。

```c++
#include <string>
#include <iostream>
using namespace std;
class ExamInfo{
private:
    string name;
    enum{GRADE, PASS, PERCENTACE} mode;
    union{
        char grade;
        bool pass;
    	int percent;
    }
public:
    ExamInfo(string name, char grade):name(name), mode(GRADE), grade(grade){ }
    ExamInfo(string name, bool pass):name(name), mode(PASS), pass(pass){ }
    ExamInfo(string name, int percent):name(name), mode(PERCENTACE), percent(percent){}
    void show();
}
void ExamInfo::show(){
    cout << name << ": ";
    switch(mode){
        case GRADE: cout << grade;break;
        case PASS: cout << (pass ? "PASS" : "FAIL");break;
        case PERCENTACE: cout << percent;break;
    }
    cout << endl;
}
int main(){
    ExamInfo course1("English", 'B');
    ExamInfo course2("Calculus", true);
    ExamInfo course3("C++ Programming", 85);
    course1.show();
    course2.show();
    course3.show();
    return 0;
}
```

```
English: B
Calculus: PASS
C++ Programming: 85
```

### 枚举类

#### 枚举类定义

- 语法形式

  `enum class 枚举类型名:底层类型{枚举值列表};`

- 例：

  ```c++
  enum class Type{General, Light, Medium, Heavy};
  enum class Type:char {General, Light, Medium, Heavy};
  enum class Category{General = 1, Pistol, MachineGun, Cannon};
  ```

#### 枚举类的优势

- 强作用域，其作用值限制在枚举类中。

  - 例：使用Type的枚举值General：

    ​        Type::General

- 转换限制，枚举类对象不可以与整型隐式的互相转换。

- 可以指定底层类型

  - 例：

    ```c++
    enum classType:char {General, Light, Medium, Heavy};
    ```

```c++
#include <iostream>
using namespace std;
enum class Side{Right, Left};
enum class Thing{Wrong, Right};//不冲突
int main(){
    Side s = Side::Right;
    Thing w = Thing::Wrong;
    cout << (s == w) << endl;//编译错误，无法直接比较不同枚举类
    return 0;
}
```

### 实验四（上）

例题一

声明一个CPU类，包含等级（rank）、频率（frequency）、电压（voltage）等属性，有两个公有成员函数run、stop。

其中：

rank为枚举类型CPU_Rank，声明为`enum CPU_Rank {P1 = 1, P2, P3, P4, P5, P6, P7}`,frequency为单位是MHz的整型数，voltage为浮点型的电压值。

注意不同访问属性的成员访问方式，并观察构造函数和析构函数的调用顺序。

```c++
#include <iostream>
using namespace std;
enum CPU_Rank {P1 = 1, P2, P3, P4, P5, P6, P7};
class CPU{
private:
    CPU_Rank rank;
    int frequency;
    float voltage;
public:
    CPU(CPU_Rank r, int f, float v){
        rank = r;
        frequency = f;
        voltage = v;
        cout << "构造了一个CPU!" << endl;
    }
    ~CPU(){cout << "析构了一个CPU!" << endl;}
    CPU_Rank GetRank() const {return rank;}
    int GetFrequency() const {return frequency;}
    float GetVoltage() const {return voltage;}
    void SetRank(CPU_Rank r){rank = r;}
    void SetFrequency(int f){frequency = f;}
    void SetVoltage(float v){voltage = v;}
    void Run(){cout << "CPU开始运行!" << endl;}
    void Stop(){cout << "CPU停止运行!" << endl;}
};
int main(){
    CPU a(P6, 300, 2.8);
    a.Run();
    a.Stop();
    return 0;
}
```

扩展练习：

类似的，声明RAM类、CDROM类。为实验四下半部分基于类的组合来构建Computer类打下一个基础。

提示：

1. RAM类的主要参数包括：容量、类型和主频；类型建议用枚举类型（DDR4/DDR3/DDR2...）。
2. CD-ROM类的主要参数包括：接口类型、缓存容量、安装方式；接口类型建议用枚举类型（SATA、USB...），安装方式建议用枚举类型（external/built-in）。

### 实验四（下）

例题一

在实验四（上）中声明的CPU类、RAM类、CDROM类基础之上，再声明Computer类。

要求：

1. 其中声明私有数据成员cpu、ram、cdrom，声明公有成员函数run、stop，可在其中输出提示信息。
2. 在main()函数中声明一个Computer类的对象，调用其函数成员。

```c++
#include <iostream>
using namespace std;
enum CPU_Rank {P1 = 1, P2, P3, P4, P5, P6, P7};
class CPU{
private:
    CPU_Rank rank;
    int frequency;
    float voltage;
public:
    CPU(CPU_Rank r, int f, float v){
        rank = r;
        frequency = f;
        voltage = v;
        cout << "构造了一个CPU!" << endl;
    }
    ~CPU(){cout << "析构了一个CPU!" << endl;}
    CPU_Rank GetRank() const {return rank;}
    int GetFrequency() const {return frequency;}
    float GetVoltage() const {return voltage;}
    void SetRank(CPU_Rank r){rank = r;}
    void SetFrequency(int f){frequency = f;}
    void SetVoltage(float v){voltage = v;}
    void Run(){cout << "CPU开始运行!" << endl;}
    void Stop(){cout << "CPU停止运行!" << endl;}
};
enum RAM_Type{DDR2 = 2, DDR3, DDR4};
class RAM{
private:
    enum RAM_Type type;
    unsigned int frequency;
    unsigned int size//GB
public:
    RAM(RAM_Type t, unsigned int f, unsigned int s){
        type = t;
        frequency = f;
        size = s;
        cout << "构造了一个RAM!" << endl;
    }
    ~RAM(){cout << "析构了一个RAM!" << endl;}
    RAM_Type GetType() const {return type;}
    unsigned int GetFrequency() const {return frequency;}
    unsigned int GetSize() const {return size;}
    void Setype(RAM_Type t){type = t;}
    void SetFrequency(unsigned int f){frequency = f;}
    void SetSize(unsigned int s){size = s;}
	void Run(){cout << "RAM开始运行!" << endl;}
    void Stop(){cout << "RAM停止运行!" << endl;}
};
enum CDROM_Interface{SATA, USB};
enum CDROM_Install_type{external, built_in};
class CD_ROM{
private:
    enum CDROM_Interface interface_type;
    unsigned int cache_size;//MB 
    CDROM_Install_type install_type;
public:
    CD_ROM(CDROM_Interface i, unsigned int s, CDROM_Install_type it){
        interface_type = i;
        cache_size = s;
        install_type = it;
        cout << "构造了一个CD_ROM!" << endl;
    }
    ~CD_ROM(){cout << "析构了一个CD_ROM!" << endl;}
    CDROM_Interface GetInterfaceType() const {return interface_type;}
    unsigned int GetSize() const {return cache_size;}
    CDROM_Install_type GetInstall_type() const {return install_type;}
    void SetInterfaceType(DROM_Interface i){interface_type = i;}
    void SetSize(unsigned int s){cache_size = s;}
    void SetInstall_type(CDROM_Install_type it){install_type = it;}
    void Run(){cout << "CD_ROM开始运行!" << endl;}
    void Stop(){cout << "CD_ROM停止运行!" << endl;}
};
class Computer{
private:
    CPU myCPU;
    RAM myRAM;
    CD_ROM mycdrom;
    unsigned int storage_size;//GB
    unsigned int bandwidth;//MB
public:
    Computer(CPU c, RAM r, CD_ROM cd, unsigned int s, unsigned int b);
    ~Computer(){cout << "析构了一个CD_ROM!" << endl;}
    void Run(){
    	mycpu.Run();
    	myram.Run();
		mycdrom.Run();
    	cout << "COMPUTER开始运行!" << endl;
	}
    void Stop(){
    	mycpu.Stop();
    	myram.Stop();
		mycdrom.Stop();
    	cout << "COMPUTER停止运行!" << endl;
	}    
};
COMPUTER::COMPUTER(CPU c, RAM r, CD_ROM cd, unsigned int s, unsigned int b):my_cpu(c), my_ram(r), my_cdrom(cd){
    storage_size = s;
    bandwidth = b;
    cout << "构造了一个COMPUTER!" << endl;
}
int main(){
    CPU a(P6, 300, 2.8);
    a.Run();
    a.Stop();
    cout << "*************************\n";
    RAM b(DDR3, 1600, 8);
    b.Run();
    b.Stop();
    cout << "*************************\n";
    CD_ROM c(SATA, 2, built-in);
    c.Run();
    c.Stop();
    cout << "*************************\n";
    COMPUTER my_computer(a, b, c, 128, 10);
    cout << "*************************\n";
    my_computer.Run();
    my_computer.Stop();
    cout << "*************************\n";
    return 0;
}
```


