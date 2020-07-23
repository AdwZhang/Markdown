2-1 

    用插入排序优化归并排序,代码如下：

```c++
#include<iostream>
using namespace std;
void merge(int* a, int left, int mid, int right);
void merge_sort(int* a, int left, int right);
void insert_sort(int* a, int left, int right);
int k = 3;


int main() {
	int n;
	cin >> n;
	int* a = new int[n];
	for (int i = 0; i < n; i++)
		cin >> a[i];
	merge_sort(a, 0, n - 1);
	for (int i = 0; i < n; i++)
		cout << a[i] << " ";
	return 0;
}

void merge_sort(int* a, int left, int right) {
	if (left < right) {
		int mid = (left + right) / 2;
		if (right - left + 1 <= k) {
			insert_sort(a, left, mid);
			insert_sort(a, mid + 1, right);
		}
		else {
			merge_sort(a, left, mid);
			merge_sort(a, mid + 1, right);
		}
		merge(a, left, mid, right);
	}
}

void merge(int* a, int left, int mid, int right) {
	int* temp = new int[right - left + 1];
	int i = left, j = mid + 1, index = 0;
	while (i <= mid && j <= right) {
		if (a[i] <= a[j]) temp[index++] = a[i++];
		else temp[index++] = a[j++];
	}
	while (i <= mid)
		temp[index++] = a[i++];
	while (j <= right)
		temp[index++] = a[j++];
	for (i = 0; i <= right - left; i++) {
		a[left + i] = temp[i];
	}
}

void insert_sort(int* a, int left, int right) {
	for (int i = left + 1; i <= right; i++) {
		int j = i - 1;
		int temp = a[i];
		while (j >= left) {
			if (a[j] > temp) a[j + 1] = a[j];
			else break;
			j--;
		}
		a[j + 1] = temp;
	}
}

```

a. 插入排序的最坏情况，当目标是将数组从小到大进行排序时，**最坏情况即数组原本的顺序为从大到小排序**,此时时间复杂度为$O(n^2)$。因为此时每个子表的输入规模都是k，所以每个子表的最坏时间复杂度为$O(k^2)$,因为一共有n/k个子表，所以此时的时间复杂度$T(n)=n/k*O(k^2)=O(nk)$

b. 合并算法的时间复杂度为固定的$O(n)$,此时一共有n/k个子表，所以一共要进行$lg(n/k)$轮合并,如假设一共有8个子表，需要进行的合并操作就是：8->4->2->1;最后合并为一组，每轮合并的时间复杂度都为$O(n)$——当有n/k个子表时，第一轮一共进行了n/2k次合并，每次的时间复杂度都是$O(2k)$,所以这一轮的总复杂度为$T(n)=n/2k*O(2k)=O(n)$。而一共进行了lg(n/k)轮，所以所有轮加起来的复杂度为$T(n)=lg(n/k)*O(n)=O(nlg(n/k))$

c. 

$nk+nlg(n/k)=nk+nlg(n)-nlg(k)<=nlg(n)$,因为n>=0,所以化简得：$k-lg(k)<=0$

众所周知，n的增长率是大于lgn的，所以当k=lgk时，k最大。

d.