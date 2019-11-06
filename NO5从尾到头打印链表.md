# <center>NO5 从尾到头打印链表
>题目要求

    输入一个链表，按链表从尾到头的顺序返回一个ArrayList。

>分析-方法一

    1. listNode 是链表，只能从头遍历到尾，但是输出却要求从尾到头，这是典型的"先进后出"，我们可以想到栈！
    2. ArrayList 中有个方法是 add(index,value)，可以指定 index 位置插入 value 值
    3. 所以我们在遍历 listNode 的同时将每个遇到的值插入到 list 的 0 位置，最后输出 listNode 即可得到逆序链表

>代码
```java

import java.util.*;
public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        ArrayList<Integer> list = new ArrayList<>();
        ListNode tmp = listNode;
        while(tmp!=null){
            list.add(0,tmp.val);
            tmp = tmp.next;
        }
        return list;
    }
}
```
>复杂度

    时间复杂度：O(n)
    空间复杂度：O(n)
>分析-方法二

    既然非递归都实现了，那么我们也可以利用递归，借助系统的"栈"帮忙打印

>代码
```java
import java.util.*;
public class Solution {
    ArrayList<Integer> list = new ArrayList();
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        if(listNode!=null){
            printListFromTailToHead(listNode.next);
            list.add(listNode.val);
        }
        return list;
    }
}
```
>复杂度

    时间复杂度：O(n)
    空间复杂度：O(n)