## 第5章 数据的共享与保护

### 标识符的作用域与可见性

#### 作用域分类

- 函数原型作用域
- 局部作用域（块作用域）
- 类作用域
- 文件作用域
- 命名空间作用域（详见第10章）

##### 函数原型作用域

- 函数原型中的参数
- 其作用域始于“(”，结束于“)”

##### 函数原型作用域举例

![在这里插入图片描述](https://img-blog.csdnimg.cn/1c8342b24e7e43c09f1a6f23713abfb6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_11,color_FFFFFF,t_70,g_se,x_16#pic_center)


##### 局部作用域

- 函数的形参、在块中声明的标识符；
- 作用域自声明处起，限于块中。

##### 局部作用域举例

![在这里插入图片描述](https://img-blog.csdnimg.cn/30dcc45fb3e0441cad2008299149a419.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


##### 类作用域

- 类的成员具有类作用域，其范围包括类体和成员函数体。
- 在类作用域以外访问类的成员：
  - 静态成员：通过类名，或者该类的对象名、对象引用访问。
  - 非静态成员：通过类名，或者该类的对象名、对象指针访问。

##### 文件作用域

- 不在前述各个作用域中出现的声明，就具有文件作用域；
- 其作用域开始于声明点，结束于文件尾。

##### 可见性

- 可见性是从对标识符的引用的角度来谈的概念
- 可见性表示从内层作用域向外层作用域“看”时能看见什么。
- 如果标识符在某处可见，就可以在该处应用此标识符。

![在这里插入图片描述](https://img-blog.csdnimg.cn/4c314ff34a55464fb41a5db8104f148a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_19,color_FFFFFF,t_70,g_se,x_16#pic_center)


- 如果某个标识符在外层声明，且在内层中
- 没有同一标识符的声明，则该标识符在内层可见。
- 对于两个嵌套的作用域，如果在内层作用域内声明了与外层作用域中同名的标识符，则外层作用域的标识符在内层不可见。

```c++
#include <iostream>
using namespace std;
int i;
int main(){
    i = 5;
    {
        int i;
        i = 7;
        cout << "i = " << i << endl;
    }
    cout << "i = " << i << endl;
    return 0;
}
```

```
i = 7
i = 5
```

### 对象的生存期

#### 对象的生存期

- 对象从产生到结束的这段时间就是他的生成期。
- 在对象生成期内，对象将保持它的值，直到被更新为止。
- 静态生存期
- 动态生存期

##### 静态生存期

- 这种生存期与程序的运行期相同。
- 在文件作用域中声明的对象具有这种生存期。
- 在函数内部声明静态生存期对象，要冠以关键字static。

##### 动态生存期

- 开始于程序执行到声明点时，结束于命名该标识符的作用域结束处。
- 块作用域中声明的，没有用static修饰的对象是动态生存期的对象（习惯称局部生存期对象）。

```c++
#include <iostream>
using namespace std;
int i = 1;
void other(){
    static int a = 2;
    static int b;
    int c = 10;
    a += 2;i += 32;c += 5;
    cout << "---OTHER---\n";
    cout << "i: " << i << "  a: " << " b: " << b << " c: " << c << endl;
    b = a;
}
int main(){
    static int a;
    int  b = -10;
    int c = 0;
    cout << "---MAIN---\n";
    cout << "i: " << i << "  a: " << " b: " << b << " c: " << c << endl;
    c += 8;other();
    cout << "---MAIN---\n";
    cout << "i: " << i << "  a: " << " b: " << b << " c: " << c << endl;
    i += 10;other();
    return 0;
}
```

```
---MAIN---
i: 1  a: 0 b: -10 c: 0
---OTHER---
i: 33  a: 4 b: 0 c: 15
---MAIN---
i: 33  a: 0 b: -10 c: 8
---OTHER---
i: 75  a: 6 b: 4 c: 15
```

### 类的静态成员

#### 静态数据成员（例5-4）

##### 静态数据成员

- 用关键字static声明
- 为该类的所有对象共享，静态数据成员具有静态生存期。
- 必须在类外定义和初始化，用（::）来指明所属的类。

例5-4 具有静态数据成员的Point类

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-K1UIHGPG-1647359813894)(C:\Users\linyo\Pictures\4.png)]

```c++
#include <iostream>
using namespace std;
class Point{
public:
    Point(int x = 0, int y = 0):x(x), y(y){
        count++;
    }
    Point (Point &p){
        x = p.x;y = p.y;count++;
    }
    ~Point(){count--;};
    int getX(){return x;}
    int getY(){return y;}
    void showCount(){
        cout << " Object count = " << count << endl;
    }
private:
    int x, y;
    static int count;
};
int Point::count = 0;
int main(){
    Point a(4,5);
    cout << "PointA: " << a.getX() << ", " << a.getY();
    a.showCount();
    Point b(a);
    cout << "PointB: " << a.getX() << ", " << a.getY();
    b.showCount();
    return 0;
}
```

```
PointA: 4, 5 Object count = 1
PointB: 4, 5 Object count = 2
```

#### 静态函数成员（例5-5）

静态函数成员主要用于处理该类的静态数据

静态函数成员如果要访问非静态成员，要通过对象来访问。

例5-5 具有静态数据、函数成员的Point类

![在这里插入图片描述](https://img-blog.csdnimg.cn/d7ae6081118748dd8ba434f840787139.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_13,color_FFFFFF,t_70,g_se,x_16#pic_center)


```c++
#include <iostream>
using namespace std;
class Point{
public:
    Point(int x = 0, int y = 0):x(x), y(y){count++;}
    Point (Point &p){
        x = p.x;
        y = p.y;
        count++;
    }
    ~Point(){count--;};
    int getX(){return x;}
    int getY(){return y;}
    static void showCount(){
        cout << " Object count = " << count << endl;
    }
private:
    int x, y;
    static int count;
};
int Point::count = 0;
int main(){
    Point a(4,5);
    cout << "PointA: " << a.getX() << ", " << a.getY();
    Point::showCount();
    Point b(a);
    cout << "PointB: " << a.getX() << ", " << a.getY();
    Point::showCount();
    return 0;
}    
```

### 类的友元

- 友元是C++提供的一种破坏数据封装和数据隐藏的机制。
- 通过将一个模块声明为为另一个模块的友元，一个模块能够引用到另一个模块中本是被隐藏的信息。
- 可以声明友元函数和友元类。
- 为了确保数据的完整性，及数据封装与隐藏的原则，建议慎用友元。

#### 友元函数

- 友元函数是在类声明中由关键字friend修饰说明的非成员函数，在它的函数体中能够通过对象名访问private和protected成员.
- 作用：增加灵活性，使程序员可以在封装和快速性方面做合理选择。
- 访问对象中的成员必须通过对象名。

例5-6 使用友元函数计算两点间的距离

```c++
#include <iostream>
#include <cmath>
using namespace std;
class Point{
public:
    Point (int x = 0, int y = 0):x(x), y(y){}
    int getX(){return x;}
    int getY(){return y;}
    friend float dist(Point &a, Point &b);
private:
    int x, y;
};
float dist(Point &a, Point &b){
    double x = a.x - b.x;
    double y = a.y - b.y;
    return static_cast<float>(sqrt(x * x + y * y));
}
int main(){
    Point p1(1, 1), p2(4, 5);
    cout << "The distance is: ";
    cout << dist(p1, p2) << endl;
    return 0;
}
```

```
The distance is: 5
```

#### 友元类

- 若一个类为另一个类的友元，则此类的所有成员都能访问对方类的私有成员。
- 声明语法：将友元类名在另一个类中使用friend修饰说明。

```c++
class A{
    friend class B;
public:
    void display(){
        cout << x << endl;
    }
private:
    int x;
};
class B{
public :
    void set(int i);
    void display();
private:
    A a;
};
void B::set(int i){
    a.x = i;
}
void B::display(){
    a.display();
}
```

类的友元关系是单向的：

声明B类是A类的友元$$A类是B类的友元

### 共享数据的保护

#### 常类型

- 常对象：必须进行初始化，不能被更新。

  ```c++
  const 类名 对象名;
  ```

- 常成员：

  用**const**进行修饰的成员：常数据成员和常函数成员。

- 常引用：被引用的对象不能被更新。

  ```c++
  const 类型说明符 &引用名
  ```

- 常数组：数组元素不能被更新（详见第6章）。

  ```c++
  类型说明符 const 数组名[大小]...
  ```

- 常指针：指向常量的指针（详见第6章）。

#### 常对象

- 用const修饰的对象

- 例：

  ```c++
  class A{
  public:
      A(int i, int j){x = i; y = j;}
      ...
  private:
      int x, y;
  };
  //...
  A const a(3, 4);
  ```

#### 常成员：

用const修饰的对象成员

- 常成员函数

  - 使用const关键字说明的函数。

  - 常成员函数不更新的数据成员。

  - 常成员函数说明格式：

    ```c++
    类型说明符 函数名（参数表) const;
    ```

    这里，const是函数类型的一个组成部分，因此在实现部分也要带const关键字。

  - const关键字可以被用于参与对重载函数的区分

  - 通过常对象只能调用它的常成员函数。

- 常数据成员

  - 使用const说明的数据成员。

例5-7 常成员函数举例

```c++
#include <iostream>
using namespace std;
class R{
public:
    R(int r1, int r2):r1(r1), r2(r2){}
    void print();
    void print() const;
private:
    int r1, r2;
};
void R::print(){
    cout << r1 << ":" << r2 << endl;
}
void R::print() const{
    cout << r1 << ";" << r2 << endl;
}
int main(){
    R a(5, 4);
    a.print();
    const R b(20, 52);
    b.print();
    return 0;
}
```

```
5:4
20:52
```

例5-8 常数据成员举例

```c++
#include<iostream>
using namespace std;
class A{
public:
    A(int i);
    void print();
private:
    const int a;
    static const int b;
};
const int A::b = 10;
A::A(int i):a(i){}
void A::print(){
    cout << a << ":" << b << endl;
}
int main(){
    A a1(100), a2(0);
    a1.print();
    a2.print();
    return 0;
}
```

```
100:10
0:10
```

#### 常引用

在友元函数中用常引用做参数，既能获得较高的执行效率，又能保证实参的安全性。

例5-9 常引用作形参

```c++
#include <iostream>
#include <cmath>
using namespace std;
class Point{
public:
    Point (int x = 0, int y = 0):x(x), y(y){}
    int getX(){return x;}
    int getY(){return y;}
    friend float dist(Point &p1, Point &p2);
private:
    int x, y;
};
float dist(Point &p1, Point &p2){
    double x = p1.x - p2.x;
    double y = p1.y - p2.y;
    return static_cast<float>(sqrt(x * x + y * y));
}
int main(){
    Point myp1(1, 1), myp2(4, 5);
    cout << "The distance is: ";
    cout << dist(myp1, myp2) << endl;
    return 0;
}
```

### 多文件结构和预编译命令

#### C++程序的一般组织结构

- 一个工程可以划分为多个源文件，例如
  - 类声明文件（.h文件）
  - 类实现文件（.cpp文件）
  - 类的使用文件（main()所在的cpp文件）
- 利用工程来组合各个文件

例5-10 多文件的工程

```c++
class Point{
public:
    Point(int x = 0, int y = 0):x(x), y(y){}
    Point(const Point &p);
    ~Point(){count--;};
    int getX(){return x;}
    int getY(){return y;}
    static void showCount();
private:
    int x, y;
    static int count;
};
```

```c++
#include "Point.h"
#include <iostream>
using namespace std;
int Point::count(const Point &p):x(p.x), y(p.y){
    count++;
}
void Point::showCount(){
    cout << "Object count = " << count << endl;
}
```

```c++
#include "Point.h"
#include <iostream>
using namespace std;
int main(){
    Point a(4,5);
    cout << "PointA: " << a.getX() << ", " << a.getY();
    Point::showCount();
    Point b(a);
    cout << "PointB: " << a.getX() << ", " << a.getY();
    Point::showCount();
    return 0;
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/cff9ec24b955439ea910bd35983e9f77.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA56iL5bqP5ZGY5bCP5YuH,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)


#### 外部变量

- 除了在定义它的源文件中可以使用外，还可以被其他文件使用。
- 文件作用域中定义的变量，默认情况下都是外部变量
- 在其他文件中如果需要使用，需要用extern关键字声明。

#### 外部函数

- 在所有类之外声明的函数（也就是非成员函数），都是具有文件作用域的。
- 这样的函数都可以在不同的编译单元中调用
- 只要在调用之前进行引用性声明（即声明函数原型）即可。

#### 将变量和函数限制在编译单元内

- 在匿名命名空间中定义的变量和函数，都不会暴露给其他的编译单元。

  ```c++
  namespace{//匿名的命名空间
      int n;
      void f(){
          n++;
      }
  }
  ```

#### 标准C++库

- 标准C++类库是一个极为灵活并可扩展的可重用软件模块的集合。

  标准C++类与组件在逻辑上分为6种类型：

  - 输入/输出类
  - 容器类与抽象数据类型
  - 存储管理类
  - 算法
  - 错误处理
  - 运行环境支持

#### 编译预处理

- #include包含命令
  - 将一个源文件嵌入到当前源文件中该点处。
  - `#include<文件名>`
    - 按标准方式搜索，文件位于C++系统目录的include子目录下
  - `#include"文件名"`
    - 首先在当前目录中搜索，若没有，再按标准方式搜索。
- #define宏定义指令
  - 定义符号常量，很多情况下已被const定义语句取代。
  - 定义带参数宏，已被内联函数取代。
- #undef
  - 删除由#define定义的宏，使之不再起作用。

**条件编译指令**——#if和#endif

```c++
#if 常量表达式
//当”常量表达式“非零时编译
	程序正文
#endif
......
```

**条件编译指令**——#else

```c++
#if 常量表达式
	程序正文1//当”常量表达式“非零时编译
#else
	程序正文2//当”常量表达式“非零时编译
#endif
```

**条件编译指令**——#elif

```c++
#if 常量表达式1
	程序正文1//当”常量表达式1“非零时编译
#elif 常量表达式2
    程序正文2//当”常量表达式2“非零时编译
#else
	程序正文3
#endif
```

**条件编译指令**

```c++
#ifdef 标识符
	程序段1
#else
    程序段2
#endif
```

- 如果“标识符”经#define定义过，且未经undef删除，则编译程序段1
- 否则编译程序段2。

```c++
#ifndef 标识符
	程序段1
#else
    程序段2
#endif
```

- 如果“标识符”未被定义过，则编译程序段1
- 否则编译程序段2。

### 实验五

例题一：

运行下面的程序，观察变量x、y的值。

```c++
#include <iostream>
using namespace std;
void fn1();
int x = 1, y = 2;
int main(){
    cout << "Begin..." << endl;
    cout << "x = " << x << endl;
    cout << "y = " << y << endl;
    cout << "Evaluate x and y in main()..." << endl;
    int x = 10, y = 20;
    cout << "x = " << x << endl;
    cout << "y = " << y << endl;
    cout << "Step into fn1()..." << endl;
    fn1();
    cout << "Back in main()" << endl;
    cout << "x = " << x << endl;
    cout << "y = " << y << endl;
    return 0;
}
void fn1(){
    int y = 200;
    cout << "x = " << x << endl;
    cout << "y = " << y << endl;
}
```

```
Begin...
x = 1
y = 2
Evaluate x and y in main()...
x = 10
y = 20
Step into fn1()...
x = 1
y = 200
Back in main()
x = 10
y = 20
```

例题二：

实现客户机（CLIENT）类：

- 声明字符型静态数据成员ServerName，保存其服务器名称；
- 整型静态数据成员ClientNum，记录已定义的客户数量；
- 定义静态函数ChangeServerName()改变服务器名称。

在头文件client.h中声明类，

在文件client.cpp中实现，

在文件test.cpp中测试这个类，

观察相应的成员变量取值的变化情况。

```c++
#ifndef CLIENT_H_
#define CLENT_H_
class Client{
    static char ServerName;
    static int ClientNum;
public:
    static void ChangeServerName(char name);
    static int getClientNum();
};
#endif//CIENT_H_
```

```c++
#include "client.h"
void Client::ChangeServerName(char name){
    Client::ServerName = name;
    Client::ClientNum ++;
}
int getClientNum(){
    return Client::ClientNum;
}
```

```c++
#include <iostream>
#include "client.h"
using namespace std;
int Client::ClientNum = 0;
char Client::ServerName = 'a';
int main(){
    Client c1;
    c1.ChangeServerName() << endl;
    Client c2;
    c2.ChangeServerName() << endl;
    return 0;
}
```


