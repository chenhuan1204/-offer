# <center> NO22 包含min函数的栈
> 题目要求

    定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。
    注意：保证测试中不会当栈为空的时候，对栈调用pop()或者min()或者top()方法。

>原理分析

    Stack.Peek 与 stack.pop 的区别

    相同点：大家都返回栈顶的值。

    不同点：peek 不改变栈的值(不删除栈顶的值)，pop会把栈顶的值删除。



> 代码

```java 
import java.util.Stack;
import java.util.Iterator;
public class Solution {

    Stack<Integer> stack = new Stack<Integer>();
    public void push(int node) {
        stack.push(node);
    }
    
    public void pop() {
        stack.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int min() {
        int min = stack.peek();
        int tmp = 0;
        Iterator<Integer> iterator = stack.iterator();
        while(iterator.hasNext()){
            tmp = iterator.next();
            if(min > tmp){
                min = tmp;
            }
        }
        return min;
    }
}
```