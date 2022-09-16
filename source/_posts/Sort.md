---
title: Sort
date: 2022-09-16 15:25:00
author: XueYisheng
img: https://s1.ax1x.com/2022/09/16/vzLAR1.jpg
top: true
hide: false
cover: true
coverImg: https://s1.ax1x.com/2022/09/16/vzLAR1.jpg
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: false
mathjax: false
summary: 所谓排序，就是使一串记录，按照其中的某个或某些关键字的大小，递增或递减的排列起来的操作
categories: 数据结构
tags:
  - 排序
---

## 1.排序的概念及其运用
### 1.1排序的概念
- 排序：所谓排序，就是使一串记录，按照其中的某个或某些关键字的大小，递增或递减的排列起来的操作。
- 稳定性：假定在待排序的记录序列中，存在多个具有相同的关键字的记录，若经过排序，这些记录的相对次序保持不变，即在原序列中，r[i]=r[j]，且r[i]在r[j]之前，<font color='red'>而在排序后的序列中，r[i]仍在r[j]之前，则称这种排序算法是稳定的 text </font>；否则称为不稳定的。
- 内部排序：数据元素全部放在内存中的排序。
- 外部排序：数据元素太多不能同时放在内存中，根据排序过程的要求不能在内外存之间移动数据的排序。
### 1.2 常见的排序算法


<a href="https://imgse.com/i/vzhzr9"><img src="https://s1.ax1x.com/2022/09/16/vzhzr9.png" alt="排序归类" border="0" /></a>   

其中基数排序是比较特殊的一类，它是分类拆开后按顺序合并，以此类推，反复几次。

## 2.常见排序算法的实现
### 2.1 插入排序
#### 2.1.1基本思想：
直接插入排序是一种简单的插入排序法，其基本思想是：把待排序的记录按其关键码值的大小逐个插入到一个已经排好序的有序序列中，直到所有的记录插入完为止，得到一个新的有序序列。实际中我们玩扑克牌时，就用了插入排序的思想。

<a href="https://imgse.com/i/vz4LdI"><img src="https://s1.ax1x.com/2022/09/16/vz4LdI.jpg" alt="扑克牌示例" border="0" /></a>
```
void InsertSort(int* a, int n)
{
	for (int i = 0; i < n - 1; ++i)
	{
		// [0,end]有序，把end+1位置的值插入，保持有序
		int end = i;
		int tmp = a[end + 1];
		while (end >= 0)
		{
			if (tmp < a[end])
			{
				a[end + 1] = a[end];
				--end;
			}
			else
			{
				break;
			}
		}
		a[end + 1] = tmp;
	}
}
```

#### 2.1.2直接插入排序：
当插入第i(i>=1)个元素时，前面的array[0],array[1],…,array[i-1]已经排好序，此时用array[i]的排序码与array[i-1],array[i-2],…的排序码顺序进行比较，找到插入位置即将array[i]插入，原来位置上的元素顺序后移。  
直接插入排序的特性总结：
1. 元素集合越接近有序，直接插入排序算法的时间效率越高
2. 时间复杂度：O(N^2)
3. 空间复杂度：O(1)，它是一种稳定的排序算法
4. 稳定性：稳定

### 2.1.3 希尔排序( 缩小增量排序 )
希尔排序法又称缩小增量法。希尔排序法的基本思想是：先选定一个整数，把待排序文件中所有记录分成个组，所有距离为的记录分在同一组内，并对每一组内的记录进行排序。然后，取重复上述分组和排序的工
作。当到达=1时，所有记录在统一组内排好序。

<a href="https://imgse.com/i/vzIFje"><img src="https://s1.ax1x.com/2022/09/16/vzIFje.png" alt="希尔排序示例图" border="0" /></a> 

```
//平均：O(N^1.3）
void ShellSort(int* a,int n)
{
  int gap = n;
  while(gap > 1)
  {
    gap = gap / 3 + 1;
    for(int i=0;i<n-gap;i++)
    {
      int end = i;
      int temp = a[end + gap];
      while(end >= 0)
      {
        if(temp < a[end]>)
        {
          a[end + gap] = a[end];
          end = end - gap;
        }
        else{
          break;
        }
      }
      a[end + gap] = temp;
    } 
  }
}
```

希尔排序的特性总结：
1. 希尔排序是对直接插入排序的优化。
2. 当gap > 1时都是预排序，目的是让数组更接近于有序。当gap == 1时，数组已经接近有序的了，这样就
会很快。这样整体而言，可以达到优化的效果。我们实现后可以进行性能测试的对比。
3. 希尔排序的时间复杂度不好计算，因为gap的取值方法很多，导致很难去计算。
## 2.2 选择排序
### 2.2.1基本思想：
每一次从待排序的数据元素中选出最小（或最大）的一个元素，存放在序列的起始位置，直到全部待排序的
数据元素排完 。
### 2.2.2 直接选择排序:
在元素集合array[i]--array[n-1]中选择关键码最大(小)的数据元素
若它不是这组元素中的最后一个(第一个)元素，则将它与这组元素中的最后一个（第一个）元素交换在剩余的array[i]--array[n-2]（array[i+1]--array[n-1]）集合中，重复上述步骤，直到集合剩余1个元素。

```
void SelectSort(int* a, int n)
{
	assert(a);
	int begin = 0, end = n - 1;
	while (begin < end)
	{
		int mini = begin, maxi = begin;
		for (int i = begin + 1; i <= end; ++i)
		{
			if (a[i] < a[mini])
				mini = i;

			if (a[i] > a[maxi])
				maxi = i;
		}
		Swap(&a[begin], &a[mini]);

    //如果begin和maxi重叠，那么要修正一下maxi的位置
    //即就是begin的位置就是最大值的位置，但之前begin位置的值已经和mini交换了，所以要把maxi再换回成mini的位置的值。
		if (begin == maxi)
		{
			maxi = mini;
		}

		Swap(&a[end], &a[maxi]);
		++begin;
		--end;
	}
}
```

直接选择排序的特性总结：
1. 直接选择排序思考非常好理解，但是效率不是很好。实际中很少使用
2. 时间复杂度：O(N^2)
3. 空间复杂度：O(1)
4. 稳定性：不稳定

## 2.3 交换排序
基本思想：所谓交换，就是根据序列中两个记录键值的比较结果来对换这两个记录在序列中的位置，交换排序的特点是：将键值较大的记录向序列的尾部移动，键值较小的记录向序列的前部移动。
### 2.3.1冒泡排序
```
void BubbleSort(int* a, int n)
{
	assert(a);

	for (int j = 0; j < n - 1; ++j)
	{
		int exchange = 0;
		for (int i = 1; i < n - j; ++i)
		{
			if (a[i - 1] > a[i])
			{
				Swap(&a[i - 1], &a[i]);
				exchange = 1;
			}
		}

		if (exchange == 0)
		{
			break;
		}
	}
}
```
冒泡排序的特性总结：
1. 冒泡排序是一种非常容易理解的排序
2. 时间复杂度：O(N^2) 
3. 空间复杂度：O(1)
4. 稳定性：稳定
### 2.3.2 快速排序
快速排序是Hoare于1962年提出的一种二叉树结构的交换排序方法，其基本思想为：任取待排序元素序列中的某元素作为基准值，按照该排序码将待排序集合分割成两子序列，左子序列中所有元素均小于基准值，右子序列中所有元素均大于基准值，然后最左右子序列重复该过程，直到所有元素都排列在相应位置上为止。  
1. hoare版本   
传统的右边先走，找大；左边先走，找小。顺序不能写反。
```
int PartSort1(int* a, int begin, int end)
{
	int left = begin, right = end;
	int keyi = left;
	while (left < right)
	{
		// 右边先走，找小
        //注意这里一定加上等于，如果不加等于号，
		//那么当左右两边数值相等时，就会死循环，因为交换之后两个数依旧是相等的。

		while (left < right && a[right] >= a[keyi])
		{
			--right;
		}

		// 左边再走，找大
		while (left < right && a[left] <= a[keyi])
		{
			++left;
		}

		Swap(&a[left], &a[right]);
	}
	Swap(&a[keyi], &a[left]);
	keyi = left;
	return keyi;
}
```
加上left<right的判断，否则可能会越界访问，因为当等于的情况下
还是有right--与left++，当key为最小值时，那么right向左移动直到
与key相等，此时是数组最左边，那么经过right--，就会越界。再循环中要加上，left<right的判断。   

2. 挖坑法
先将第一个数据存放在临时变量key中，形成一个坑位。
```
int PartSort2(int* a, int begin, int end)
{
	int key = a[begin];
	int pitI = begin;
	while (begin < end)
	{
		//右边找小，填左边的坑.
		while (begin < end && a[end] >= key)
		{
			end--;
		}
		a[pitI] = a[end];
		pitI = end;
		while (begin < end && a[begin] <= key)
		{
			begin++;
		}
		a[pitI] = a[begin];
		pitI = begin;
	}
	a[pitI] = key;
	return pitI;
}
```
3. 前后指针版本
```
int PartSort3(int* a, int begin, int end)
{
	int prev = begin;
	int cur = begin + 1;
	int keyi = begin;

	// 加入三数取中的优化
	int midi = GetMidIndex(a, begin, end);
	Swap(&a[keyi], &a[midi]);

	while (cur <= end)
	{ 
		// cur位置的值小于keyi位置值
		if (a[cur] < a[keyi] && ++prev != cur)
			Swap(&a[prev], &a[cur]);

		++cur;
	}

	Swap(&a[prev], &a[keyi]);
	keyi = prev;

	return keyi;
}

int GetMidIndex(int* a, int begin, int end)
{
	int mid = (begin + end) / 2;
	if (a[begin] < a[mid])
	{
		if (a[mid] < a[end])
		{
			return mid;
		}
		else if (a[begin] < a[end])
		{
			return end;
		}
		else
		{
			return begin;
		}
	}
```
### 2.3.2 快速排序优化
1. 三数取中法选key
2. 递归到小的子区间时，可以考虑使用插入排序。C++的sort函数实现方法。
```
void QuickSort(int* a, int begin,int end)
{
	//当区间不存在或只有一个值
	if (begin >= end)
	{
		return;
	}
	if (end - begin > 10)
	{
		int keyi = PartSort1(a, begin, end);
		QuickSort(a, begin, keyi - 1);
		QuickSort(a, keyi + 1, end);
	}
	else {
		InsertSort(a + begin, end - begin + 1);
	}
}
```
### 2.3.2 快速排序非递归

```
void QuickSortNonR(int* a, int left, int right)
{
Stack st;
StackInit(&st);
StackPush(&st, left);
StackPush(&st, right);
while (StackEmpty(&st) != 0)
{
 right = StackTop(&st);
 StackPop(&st);
 left = StackTop(&st);
 StackPop(&st);
 
 if(right - left <= 1)
 continue;
 int div = PartSort1(a, left, right);
 // 以基准值为分割点，形成左右两部分：[left, div) 和 [div+1, right)
 StackPush(&st, div+1);
 StackPush(&st, right);
 
 StackPush(&st, left);
 StackPush(&st, div);
}
 
 StackDestroy(&s);
}
```
快速排序的特性总结：
1. 快速排序整体的综合性能和使用场景都是比较好的，所以才敢叫快速排序
2. 时间复杂度：O(N*logN)