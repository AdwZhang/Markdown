## Java命令行参数

        在Java中，每一个Java程序都有一个带String arg[]参数的main方法。这个参数表明main方法将接收一个字符串数组，也就是命令行参数。
---
示例：
ArgsDemo.java
```java
public class ArgsDemo {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		for(String s:args) {
			System.out.println(s);
		}
	}
}
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190726164015649.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODc0NzYw,size_16,color_FFFFFF,t_70)

如图，用javac指令编译，java指令执行，在java + 类名后跟着的字符串将会以命令行参数的形式传入程序中