## 和为S的连续正数序列
1. 方法一：通过动态的移动滑动窗口的左右区间的端点位置，找出所有连续序列数字之和等于S的情况。

```java
public ArrayList<ArrayList<Integer> > FindContinuousSequence(int sum) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<>();
        int l = 1;
        int r = 2;
        ArrayList<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        while (l < (sum + 1) / 2) {
            int tempSum = cul(l, r);
            while (tempSum > sum) {
                tempSum -= l;
                l++;
                list.remove(0);
            }
            if (tempSum == sum) {
                ans.add(new ArrayList<>(list));
                l++;
                list.remove(0);
            }
            r++;
            list.add(r);
        }
        return ans;
    }

    private int cul(int l, int r) {
        return (l + r) * (r - l + 1) / 2;
    }
```
2. 方法二:通过等差数列的求和公式去得出第一项和项数以及S的关系，通过去枚举第一项，然后算出项数n，判断n是否为整数即可
```java
public ArrayList<ArrayList<Integer> > FindContinuousSequence(int sum) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<>();
        for (int i = 1; i <= sum; i++) {
            int x = 2 * i - 1;
            double temp = Math.sqrt(x * x + 8 * sum);
            if (judge(temp)) {
                int res = (int) temp;
                double n1 = (double) (-x + res) / 2;
                double n2 = (double) (-x - res) / 2;
                if (judge(n1) && n1 > 1) {
                    ArrayList<Integer> list = new ArrayList<>();
                    for (int j = i, k = 1; k <= n1; j++, k++) {
                        list.add(j);
                    }
                    ans.add(list);
                }
                if (judge(n2) && n2 > 1) {
                    ArrayList<Integer> list = new ArrayList<>();
                    for (int j = i, k = 1; k <= n2; j++, k++) {
                        list.add(j);
                    }
                    ans.add(list);
                }
            }
        }
        return ans;
    }

    private boolean judge(double x) {
        int res = (int) x;
        return x - res <= 0.00000001;
    }
```
