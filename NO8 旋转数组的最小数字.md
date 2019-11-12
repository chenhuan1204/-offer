# <center> NO8 旋转数组的最小数字
>题目要求

    把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。例如数{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。
    NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。
>分析

    利用 Arrays 工具类里的排序函数，默认的排序规则是从小到大，排序后的数组第一个值就是最小值

> 代码

```java
import java.util.*;
public class Solution {
    public int minNumberInRotateArray(int [] array) {
        int n = array.length;
        if(n == 0){
            return 0;
        }
        Arrays.sort(array);
        return array[0];
    }
}
```

> 复杂度

    1. 时间复杂度O(nlogn)
    2. 空间复杂度O(1)