# 和为S的两个数字
## 问题描述
输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。
## 解决方法（双指针）
两个指针分别指向数组最高位置和最低位置（pHigh,pLow），若两指针所指向的数之和大于给定和S，则pHigh--；若两指针所指向的数之和小于给定和S，则pLow++;相等则输出结果。
```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> FindNumbersWithSum(int [] array,int sum) {
        int pLow=0;
        int pHigh=array.length-1;
        ArrayList<Integer> list=new ArrayList<>();
        while(pHigh>=pLow){
            int pSum=array[pHigh]+array[pLow];
            if(pSum==sum){
                list.add(array[pLow]);
                list.add(array[pHigh]);
                break;
            }
            if(pSum>sum)
                pHigh--;
            if(pSum<sum)
                pLow++;
        }
        return list;
    }
}
```
