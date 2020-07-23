
## **时间复杂度为n^2的排序**

* 冒泡排序和选择排序的共同点：每次都是在找剩下元素中最小（大）的元素
* 不同点：冒泡排序存在多次交换，而选择排序每次只存在一次交换序号



```c++
#include<iostream>
using namespace std;
void Insert_sort(int* a, int length);
void Select_sort(int* a, int length);
void Bubble_sort(int* a, int length);

int main() {
	int n;
	cin >> n;
	int* a;
	a = new int[n];
	for (int i = 0; i < n; i++) {
		cin >> a[i];
	}
	Insert_sort(a, n);
	for (int i = 0; i < n; i++) {
		cout << a[i] << " ";
	}
	return 0;
}

//插入排序 时间复杂度	n^2
void Insert_sort(int* a, int length) {
	for (int i = 1; i < length ;i++) {
		int temp = a[i];
		int j = i - 1;
		while (j >= 0 && a[j] > temp) {
			a[j + 1] = a[j];
			j--;
		}
		a[j + 1] = temp;
	}
}


//选择排序 时间复杂度	n^2
void Select_sort(int* a,int length) {
	for (int i = 0; i < length; i++) {
		int min = i;
		for (int j = i + 1; j < length; j++) {
			if (a[j] < a[min]) min = j;
		}
		int temp = a[min];
		a[min] = a[i];
		a[i] = temp;
	}
}

//冒泡排序 时间复杂度	n^2
void Bubble_sort(int* a, int length) {
	for (int i = 0; i < length - 1; i++) {
		for (int j = 0; j < length - i - 1; j++) {
			if (a[j] > a[j+1]) {
				int temp = a[j];
				a[j] = a[j + 1];
				a[j + 1] = temp;
			}
		}
	}
}



```·