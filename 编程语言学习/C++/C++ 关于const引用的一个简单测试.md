# C++ 关于const引用的测试

      今天学习了《C++ primer》第五版中的const相关内容，书中关于const的部分内容如下：
     
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191115104101498.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODc0NzYw,size_16,color_FFFFFF,t_70)

    由书中内容（P55~P56）可知，const引用有如下几种常见例子：

#### 第一种：
```c++
int i=10;
const int &r1=i;  //输出r1=10
i=20;
cout<<r1;   //输出r1=20
```
    此时const引用r1是变量i的引用，对r1不可进行修改赋值等操作，但是我们可以修改变量i已达到间接修改r1的目的，其原因是r1是一个const引用，const类型不允许进行修改，而i是一个普通int型变量，可进行赋值操作。

#### 第二种：
```c++
double d=10.1234;
const int &r2=d;   //输出r2得到10
d=11.1234;
cout<<r2;   //输出r2得到10
```
    此时修改d的值对r2没有任何影响，因为const引用r2并没有绑定到变量d上面，其原因主要是r2是const int&型的引用，而右边的一般表达式中存在双精度浮点型变量，为保证r2能够得到一个浮点型，编译器将代码修改为如下：

```c++
double d=10.1234;
int temp=d;
const int &r2=temp;   //输出r2得到10
d=11.1234;
cout<<r2;   //输出r2得到10
```
    
    所以其实常量引用r2是绑定到了一个临时创建的未命名变量上
    （上述temp应该只是随便取的名，编译器中不一定是这个）
    所以后续对浮点型变量d的修改都不影响r2的值。

#### 第三种：
```c++
int j=10;
const int &r3=2*j;  //输出r3=20
j=20;
cout<<r3;   //输出r3=20
const int &r4=30;  //输出r4=30
```
    《C++ primer》中并没有详细讲解这种情况，按理说引用应该是绑定到某个对象上，这种初始化方式并没有固定的对象，但结合上述对同样没有具体对象的一般表达式的讲解，推测也是绑定到了某个编译器生成的临时变量上。
