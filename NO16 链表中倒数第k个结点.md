 # <center> NO16 链表中倒数第k个结点
> 题目要求

    输入一个链表，输出该链表中倒数第k个结点

> 分析

    定义两个指针：
    通过初始化两个移动节点的位置距离为k，然后同时移动两个节点，知道第二个节点移动到链表的末尾时，移动节点1的位置就是链表倒数第k个节点。
<center><img src = "img/06.png"></center>

> 代码

```java 
/**
*    public class ListNode {
*        int val;
*        ListNode next = null;
*
*        ListNode(int val) {
*            this.val = val;
*        }
*    }
*
*/
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
            ListNode removeNode = head;
            while (k != 0) {
                if (removeNode == null) { 
                    /// k 大于链表的长度，直接返回null
                    return null;
                }
                removeNode = removeNode.next;
                k--;
            }
            while (removeNode != null) { 
                 /// 这个循环其实就是同时移动head和removeNode两个节点。
                removeNode = removeNode.next;
                head = head.next;
            }
            return head;
    }
}
```