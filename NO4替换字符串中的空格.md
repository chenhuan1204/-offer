# <center>二维数组中查找目标值
>题目要求

    请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

>分析

    1. indexOf("aa",n)从索引n开始，返回第一次出现aa的索引；
    2. deleteCharAt(index)删除index位置处的索引；insert(index,"bb")
    3. 在索引index处插入bb；结合这几个方法，就可以达到替换的目的

>代码
```java
public String replaceSpace(StringBuffer str) {
    int n  = 0;
    while(str.indexOf(" ",n)!=-1){
        int index = str.indexOf(" ",n);
        str.deleteCharAt(index);
        str.insert(index,"%20");
        n+=2;
    }
    return str.toString();
}
```