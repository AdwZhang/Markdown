    腾讯会议面试
---
    先是问了些具体情况，如必修课程，毕业时间，期望薪资等等。
---
卡住的题目：

##  1.学过C++编程，了解MFC吗？项目里面用过简单的窗口创建和键盘输入，能说说键盘输入的具体内部过程吗？
---
## 2. 指针函数和函数指针的区别
指针函数：返回值是一个指针的函数，如：
```c++
int *fun(int a,int b);
```
函数指针：指针的指向的是一个函数，如：
```c++
int (*fun)(int a,int b);
```
声明了一个指针fun，fun指向一个函数，该函数的参数为两个int型的变量，函数返回值为一个int型的变量。

使用函数指针：
```c++
int add(int a,int b){
    return a+b;
}

int main(){
    int (*p)(int a,int b);
    p=add;
    cout<<p(3,4);
    return 0;
}
```
---
## 3. C++里内存分配，如何分配到堆栈上
  C++内存分配的基础，一个C++程序运行时所占据的内存空间分成5个部分：
    
* 栈(stack)：
由编译器自动分配释放 ，存放函数的参数值，局部变量的值等。其操作方式类似于数据结构中的栈。
* 堆(heap)：一般由程序员分配释放，即用new、malloc进行分配的空间，若程序员不释放，在程序结束时可能由OS回收。

* 全局/静态存储区：全局变量和静态变量的存储是放在一块的，初始化的
全局变量和静态变量在一块区域， 未初始化的全局变量和未初始化的静态变量在相邻的另
一块区域。 - 程序结束后由系统释放。

* 常量存储区：常量字符串就是放在这里的。一般不允许修改。 程序结束后由系统释放

* 程序代码区：存放函数体的二进制代码。

```c++
这是一个前辈写的，非常详细 
//main.cpp 
int a = 0;  //全局初始化区 
char *p1;   //全局未初始化区 
main() 
{ 
    int b;  //栈 
    char s[] = "abc";   //栈 
    char *p2;   //栈 
    char *p3 = "123456";       //123456\0在常量区，p3在栈上。 
    static int c =0； //全局（静态）初始化区 
    p1 = (char *)malloc(10); 
    p2 = (char *)malloc(20); 
//分配得来得10和20字节的区域就在堆区。 
    strcpy(p1, "123456");   //123456\0放在常量区，编译器可能会将它与p3所指向的"123456"优化成一个地方。 
}
```
---
## 4. 面向对象的特性

    多态、继承、（抽象）、（封装）

**继承：** 
一种联结类的层次模型，并且允许和鼓励类的重用，提供一种明确表达共性的方法。对象的一个新类可以从现有的类中派生，这个过程称为类继承。新类继承了原始类的特性，新类称为原始类的派生类(子类)，原始类称为新类的基类(父类)。派生类可以从它的父类哪里继承方法和实例变量，并且类可以修改或增加新的方法使之更适合特殊的需要。因此可以说，继承为了重用父类代码，同时为实现多态性作准备。

**多态：** 多态是指允许不同类的对象对同一消息做出响应。多态性包括参数化多态性和包含多态性。多态性语言具有灵活/抽象/行为共享/代码共享的优势，很好的解决了应用程序函数同名问题。总的来说，方法的重写，重载与动态链接构成多态性。

**抽象：** 忽略一个主题中与当前目标无关的东西，专注的注意与当前目标有关的方面。

抽象包括两个方面，一个数据抽象，而是过程抽象。

    数据抽象 -->表示世界中一类事物的特征，就是对象的属性。比如鸟有翅膀，羽毛等(类的属性)

    过程抽象 -->表示世界中一类事物的行为，就是对象的行为。比如鸟会飞，会叫(类的方法)

**封装：**
    封装是面向对象的特征之一，是对象和类概念的主要特性。封装就是把过程和数据包围起来，对数据的访问只能通过已定义的界面。如私有变量，用set，get方法获取。

封装保证了模块具有较好的独立性，使得程序维护修改较为容易。对应用程序的修改仅限于类的内部，因而可以将应用程序修改带来的影响减少到最低限度。

## 5. C语言中的字符串拷贝函数
    C语言：strcpy();
    C++：s.substr(); 