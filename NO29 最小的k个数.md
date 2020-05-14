<center>NO29 最小的k个数</center>

## 题目描述

    输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

## 分析

    使用最大堆，保存目前已知的最小的k个数，堆顶是k个数中最大的元素。遍历数组，若堆中元素个数小于k，则直接添加到当前数字到堆中；若当前数字小于堆顶元素（即堆中最大元素），说明堆顶元素不可能是最小的k个数之一，因此用当前数字替换掉堆顶元素，然后保持堆有序（即最大元素在堆顶）；若当前数字大于堆顶元素，说明当前数字不可能是最小的k个数之一，跳过该数字。

    Java最大堆API：可使用优先队列来实现最大堆。需要设置比较器为逆序：
    使用最大堆（或最小堆）查找最小（或最大）的k个数，比较适合处理海量数据。因为内存的限制，通常不能一次全部载入所有输入数据到内存中。因此，可以每次只读取一部分数据，使用堆来维持目前已知的状态。

## 代码
```java

import java.util.ArrayList;
import java.util.Comparator;
import java.util.PriorityQueue;
import java.util.Queue;
public class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        if (input == null) return new ArrayList<>();
        int length = input.length;
        if (length == 0 || k <= 0 || k > length) return new ArrayList<>();
        //最大堆
        Queue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
        for (int currentValue : input)
        {
            if (maxHeap.size() < k)
            {
                maxHeap.add(currentValue);
            } else
            {
                //当前值比最大堆中的最大值小，则用当前值替换最大值
                if (currentValue < maxHeap.peek())
                {
                    maxHeap.poll();  //移除最大值
                    maxHeap.add(currentValue);  //添加当前值
                }
            }
        }
        return new ArrayList<>(maxHeap);
    }
}

```
## 快排代码
```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
       ArrayList<Integer> result=new ArrayList<Integer>();
        if(k<=0){
            return result;
        }
        if(input.length==0||input.length<k){
            return result;
        }
        Quick quick = new Quick();
        quick.sort(input);
        for(int i =0; i < k;i++){
            result.add(input[i]);
        }
        return result;
        
    }
}
class Quick{
    public  void sort(int[] a) {
		int lo =0;
		int hi = a.length-1;
		sort(a,lo,hi);
	}
	public  void sort(int[] a, int lo, int hi) {
		//安全性校验
		if(lo>=hi) {
			return ;
		}
		int partition = partition(a,lo,hi);
		sort(a,lo,partition-1);
		sort(a,partition+1,hi);
	}
	public   int partition(int[] a, int lo, int hi) {
		int key = a[lo];
	    int left = lo;
	    int right = hi+1;
	    while(true) {
	    	while(less(key,a[--right])) {
	    		if(right==lo) {
	    			break;
	    		}
	    	}
	    	while(less(a[++left],key)) {
	    		if(left==hi) {
	    			break;
	    		}
	    	}
	    	if(left>=right) {
	    		break;
	    	}else {
	    		exch(a,left,right);
	    	}
	    }
	   	exch(a,lo,right);
    	return right;
	}
	public  boolean less(int v, int w) {
		return v<w? true:false;
	}
	public  void exch(int[] a, int i,int j) {
		int temp =a[i];
		a[i] = a[j];
		a[j] = temp;
	}
}
```
## 普通方法调用Arrays sort

```java
import java.util.*;

public class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int[] input, int k) {
        ArrayList<Integer> al = new ArrayList<>();
        if(input.length <= 0 || input == null || k <= 0 || k > input.length){
            return al;
        }
        Arrays.sort(input);
        for(int i = 0; i < k; i++){
            al.add(input[i]);
        }
        return al;
    }
}

```