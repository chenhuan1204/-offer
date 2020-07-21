## 和为S的两个数字

### 方法一:通过设置两个所有指针去查找和为S的两个数字，对于当前l和r指针指向的两个数字和而言，如果说小于S，那就往右移动L指针，如果说大于S，那就往左移动R指针。
```java
public ArrayList<Integer> FindNumbersWithSum(int [] array, int sum) {
        ArrayList<Integer> list = new ArrayList<>();
        int l = 0;
        int r = array.length - 1;

        while (l <= r - 1) {
            if (array[l] + array[r] == sum) {
                list.add(array[l]);
                list.add(array[r]);
                break;
            } else if (array[l] + array[r] < sum) {
                l++;
            } else {
                r--;
            }
        }
        return list;
    }
```
