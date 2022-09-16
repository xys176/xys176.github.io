---
title: Sort
date: 2022-09-06 09:25:00
author: XueYisheng
img: https://cdn.staticaly.com/gh/xys176/image-hosting@master/6d1ffde61ff84984a225945dd3383da0-(1).3a84fce4inq0.webp
top: true
hide: false
cover: true
coverImg: https://cdn.staticaly.com/gh/xys176/image-hosting@master/6d1ffde61ff84984a225945dd3383da0-(1).3a84fce4inq0.webp
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: false
mathjax: false
summary: 所谓排序，就是使一串记录，按照其中的某个或某些关键字的大小，递增或递减的排列起来的操作
categories: 随笔
tags:
  - 日常
---

## 1.排序的概念及其运用
### 1.1排序的概念
- 排序：所谓排序，就是使一串记录，按照其中的某个或某些关键字的大小，递增或递减的排列起来的操作。
- 稳定性：假定在待排序的记录序列中，存在多个具有相同的关键字的记录，若经过排序，这些记录的相对次序保持不变，即在原序列中，r[i]=r[j]，且r[i]在r[j]之前，<font color='red'>而在排序后的序列中，r[i]仍在r[j]之前，则称这种排序算法是稳定的 text </font>；否则称为不稳定的。
- 内部排序：数据元素全部放在内存中的排序。
- 外部排序：数据元素太多不能同时放在内存中，根据排序过程的要求不能在内外存之间移动数据的排序。
### 1.2 常见的排序算法


<a href="https://imgse.com/i/vzhzr9"><img src="https://s1.ax1x.com/2022/09/16/vzhzr9.png" alt="vzhzr9.png" border="0" /></a>   

其中基数排序是比较特殊的一类，它是分类拆开后按顺序合并，以此类推，反复几次。

## 2.常见排序算法的实现
### 2.1 插入排序
#### 2.1.1基本思想：
直接插入排序是一种简单的插入排序法，其基本思想是：把待排序的记录按其关键码值的大小逐个插入到一个已经排好序的有序序列中，直到所有的记录插入完为止，得到一个新的有序序列。实际中我们玩扑克牌时，就用了插入排序的思想。

<a href="https://imgse.com/i/vz4LdI"><img src="https://s1.ax1x.com/2022/09/16/vz4LdI.jpg" alt="vz4LdI.jpg" border="0" /></a>
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

<a href="https://imgse.com/i/vzIFje"><img src="https://s1.ax1x.com/2022/09/16/vzIFje.png" alt="vzIFje.png" border="0" /></a> 

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
    //即就是begin的位置就是最大值的位置
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