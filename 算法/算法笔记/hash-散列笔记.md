## **散列基础与整数散列**
-   散列（hash哈希）的基本思想——“将元素通过一个函数转换为整数，使该整数可以尽量唯一地代表这个元素”。其中把这个转换函数称为散列函数H，元素在转换前为key，转换后是一个整数H(key)。

- 所用的数据结构——map映射

- 常用于处理字符子串重复问题

### <center>1029 旧键盘 (20 分)</center>

    旧键盘上坏了几个键，于是在敲一段文字的时候，对应的字符就不会出现。现在给出应该输入的一段文字、以及实际被输入的文字，请你列出肯定坏掉的那些键。
---    
    输入格式：
    输入在 2 行中分别给出应该输入的文字、以及实际被输入的文字。每段文字是不超过 80 个字符的串，由字母 A-Z（包括大、小写）、数字 0-9、以及下划线 _（代表空格）组成。题目保证 2 个字符串均非空。

    输出格式：  
    按照发现顺序，在一行中输出坏掉的键。其中英文字母只输出大写，每个坏键只输出一次。题目保证至少有 1 个坏键。
---
    输入样例：
        7_This_is_a_test
        _hs_s_a_es
    输出样例：
        7TI

代码如下：
```c++
#include<iostream>
#include<algorithm>
#include<string>
#include<map>
using namespace std;
string toUp(string s);
int main(){
	map<char,int> map1;
	string s1,s2;
	cin>>s1>>s2;
	s1=toUp(s1);
	s2=toUp(s2);
	for(int i=0;i<s1.length();i++){
		map1[s1[i]]=1;
	}
	for(int i=0;i<s2.length();i++){
		map1[s2[i]]=0;
	}
	for(int i=0;i<s1.length();i++){
		if(map1[s1[i]]==1){
			if(s1[i]!='-') cout<<s1[i];
			map1[s1[i]]=0;
		}
    }
	cout<<endl;
	return 0;
} 

//转换大写函数
string toUp(string s){
	for(int i=0;i<s.length();i++){
		if(s[i]<='z' && s[i]>='a'){
			s[i]+='A'-'a';
		}
	}
	return s;
}
```

### <center>1038 统计同成绩学生 (20 分)</center>
    本题要求读入 N 名学生的成绩，将获得某一给定分数的学生人数输出。
---
    输入格式：
    输入在第 1 行给出不超过e5的正整数 N，即学生总人数。随后一行给出 N 名学生的百分制整数成绩，中间以空格分隔。最后一行给出要查询的分数个数 K（不超过 N 的正整数），随后是 K 个分数，中间以空格分隔。

    输出格式：
    在一行中按查询顺序给出得分等于指定分数的学生人数，中间以空格分隔，但行末不得有多余空格。
---
    输入样例：  
    10 
    60 75 90 55 75 99 82 90 75 50 
    3 75 90 88

    输出样例：
    3 2 0


```c++
#include<iostream>
using namespace std;
int main() {
	int a[101] = { 0 };
	int n;
	cin >> n;
	int x;
	for (int i = 0; i < n; i++) {
		cin >> x;
		a[x]++;
	}
	cin >> n;
	for (int i = 0; i < n; i++) {
		cin >> x;
		cout << a[x] ;
        if(i!=n-1) cout<<" ";
	}
	return 0;
}

```
 
 
