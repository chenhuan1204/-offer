<center>NO29 最小的k个数</center>

## 题目描述

    输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

## 代码
```java

public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        if (k  > input.length || k == 0) {
            return new ArrayList<>();
        }

        int[] a = new int[k]; // 用数组去模拟k个节点的堆结构
        System.arraycopy(input, 0, a, 0, k); // 初始化堆中元素
        // 下面就开始维护堆使其成为大顶堆 - > 堆的初始化
        for (int i = k / 2 - 1; i >= 0; i--) {
            // i -> i其实就是我们所要去维护堆的节点下标
            initiate(i, a, k);
        }
        // 去遍历剩余的len - k个节点
        for (int i = k; i < input.length; i++) {
            if (input[i] < a[0]) {
                a[0] = input[i];
                initiate(0, a, k);
            }
        }
        // 将大顶堆中的节点元素进行升序操作
        for (int i = a.length - 1; i > 0; i--) {
            // 分为两个过程， 第一步交换，第二步固定(固定的操作其实是通过控制堆的节点个数去实现的)
            int temp = a[i];
            a[i] = a[0];
            a[0] = temp;
            initiate(0, a, i);
        }
        // 返回
        ArrayList<Integer> ans = new ArrayList<>();
        for (int x : a) {
            ans.add(x);
        }
        return ans;
    }

    /**
     * 初始化堆的函数,其实就是维护每一个节点的位置的函数
     * @param index 维护当前堆的下标
     * @param a 数组->堆
     * @param length 堆的节点个数
     */
    private void initiate(int index, int[] a, int length) {
        int temp = a[index]; // 先去保存当前位置的值
        for (int k = index * 2 + 1; k < length; k = k * 2 + 1) {
            if ((k + 1) < length && a[k + 1] > a[k]) {
                // 取出当前位置的左右孩子中节点值最大的节点
                k++;
            }
            if (a[k] > temp) {
                a[index] = a[k];
                index = k; // 更新index的值，index -> 代表的是temp数字最终在堆中位置，当k = k * 2 + 1执行后,index和k的关系其实就是父亲节点和孩子节点的关系。
            } else {
                break; // 由于我们是从下往上去维护的，所以说我们就没有往下更新的必要了
            }
        }
        a[index] = temp; // index所在的位置进行更新就行了

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