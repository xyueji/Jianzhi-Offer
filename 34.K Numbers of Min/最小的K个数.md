# 最小的K个数
## 问题描述
输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。
### 方法一（快排）
使用快速排序，找出数组的第k个数（左边小于第k个数，右边大于第k个数）。
```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        int len=input.length;
        int start=0;
        int end=len-1;
        ArrayList<Integer> lrs=new ArrayList<Integer>();
        if(len<k||k<1)
            return lrs;
        int index=Partition(input,start,end);
        while(index!=k-1){
            if(index>k-1){
                index=Partition(input,start,index-1);
            }else{
                index=Partition(input,index+1,end);
            }
        }
        for(int i=0;i<k;i++)
            lrs.add(input[i]);
        return lrs;
    }
    public int Partition(int[] a,int start,int end){
        int key=a[start];
        int i=start;
        int j=end;
        while(i<j){
            while(i<j&&a[j]>=key)
                j--;
            while(i<j&&a[i]<=key)
                i++;
            if(i<j){
                int temp=a[i];
                a[i]=a[j];
                a[j]=temp;
            }
        }
        a[start]=a[i];
        a[i]=key;
        return i;
    }
}
```
### 方法二
使用工具类PriorityQueue，使其大堆存储（o2.compareTo(o1)从大到小排序，默认从小到大排序）。若PriorityQueue.size()!=k时，添加数据。否则，判断input[i]是否小于PriorityQueue中的值，是则移除最大值，添加当前值。
```java
import java.util.ArrayList;
import java.util.PriorityQueue;
import java.util.Comparator;
public class Solution {
   public ArrayList<Integer> GetLeastNumbers_Solution(int[] input, int k) {
       ArrayList<Integer> result = new ArrayList<Integer>();
       int length = input.length;
       if(k > length || k == 0){
           return result;
       }
        PriorityQueue<Integer> maxHeap = new PriorityQueue<Integer>(k, new Comparator<Integer>() {
 
            @Override
            public int compare(Integer o1, Integer o2) {
                return o2.compareTo(o1);
            }
        });
        for (int i = 0; i < length; i++) {
            if (maxHeap.size() != k) {
                maxHeap.offer(input[i]);
            } else if (maxHeap.peek() > input[i]) {
                Integer temp = maxHeap.poll();
                temp = null;
                maxHeap.offer(input[i]);
            }
        }
        for (Integer integer : maxHeap) {
            result.add(integer);
        }
        return result;
    }
}
```
