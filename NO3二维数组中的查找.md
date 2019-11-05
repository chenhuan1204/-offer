# <center>二维数组中查找目标值
>题目要求
1. 在一个二维数组中，每一行从左至右递增，每一列从上到下递增
2. 输入一个二维数组和目标值，判断数组是否含有目标值
>分析

    1. 到右下角都是递增的，所以选一行列的最大值开始查找，即右上或者左下
    2. 因为是递增的，所以判断原来元素大还是小，直接移动
    3. 在一列看，只要比他小就上移动，因为最左边一列就是本行最小值，小了就直接排除，进入下一行
    4. 一旦一个属比左下角的大，就不可能在想等左边那一列，因为它比所有的都大，所以排除一列，一次递增
    5. 并未说明正方形矩阵，所以长度分开取值

>代码
```java
public class Solution {
    public boolean Find(int target, int [][] array) {
 //判断数组存在
        if(array == null)
            return  false;
 
        int row = 0;
        int colum = array[0].length-1;
 
        while(row < array.length && colum >= 0 ){
            if(array[row][colum] == target)
                return true;
            if(array[row][colum] > target){
                colum--;
            }else {         //此处不能用 if替代 ，数值变化会影响下一次判断
                row++;     // if(array[row][colum] < target)
            }
        }
        return false;
    }
}
```