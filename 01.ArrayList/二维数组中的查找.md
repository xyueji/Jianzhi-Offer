# 二维数组中的查找
## 问题描述
在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判
断数组中是否含有该整数。
## 解决思路：
首先选取数组中右上角的数字。如果该数字等于target则返回true，如果该数字大于target则删除该列，如果该数字小于target则删除该行，这样每一步都可以缩小查找范
围，直到找到要查找的数字，或没有查找到结果。同理，可以选取左下角的数字，如果该数字等于target则返回true，如果该数字大于target则删除该行，如果该数字小于
target则删除该列。
补充：java中求二维数组的行列数，行:array.length，列：array[0].length。本题中需考虑数组为空的情况。
```java
public class Solution {
    public boolean Find(int target, int [][] array) {
       boolean result=false;
        int rows=array.length,columns=array[0].length;
        if(array!=null&&rows>0&&columns>0){
            int row=0,column=columns-1;
            while(row<rows&&column>=0){
                if(array[row][column]==target){
                    result=true;
                    break;
                }
                else if(array[row][column]>target)
                    column--;
                else
                    row++;
            }
        }
        return result;
    }
}
```
