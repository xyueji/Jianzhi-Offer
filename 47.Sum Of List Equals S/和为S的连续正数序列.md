# 和为S的连续正数序列
## 问题描述
小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck!
## 解决方法
### 方法一（双指针）
以求和为9的所有连续序列为例，我们先把pLow初始化为1，pHigh初始化为2，序列和为3，比9小，把pHigh增加1得序列和为6，还是比9小，pHigh再增加1得序列和为10，比9大，把pLow增加1得序列和为9满足。
继续把pLow增加1，重复上述过程得序列{4，5}。（初始序列和比给出和小，增加pHigh;初始序列和比给出和大（或相等），增加pLow；）
```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<ArrayList<Integer> > FindContinuousSequence(int sum) {
       ArrayList<ArrayList<Integer>> lrs=new ArrayList<>();
        int pLow=1;
        int pHigh=2;
        while(pHigh>pLow){
            int pSum=(pLow+pHigh)*(pHigh-pLow+1)/2;
            if(pSum==sum){
                ArrayList<Integer> list=new ArrayList<>();
                for(int i=pLow;i<=pHigh;i++){
                    list.add(i);
                }
                lrs.add(list);
                pLow++;
            }
            if(pSum<sum)
                pHigh++;
            if(pSum>sum)
                pLow++;
        }
        return lrs;
    }
}
```
### 方法二（连续序列和的特点）
（1）当序列长度n为奇数时，平均数为序列中心的数。（sum%n==0&&(n&1)==1)<br>
（2）当序列长度n为偶数时，平均数为序列中心两个数的平均数。（sum%n*2==n)<br>
为了使sum尽量大，让n从1开始，由sum=(n+1)*n/2；满足n<Math.sqrt(2*sum);n从2遍历即可。
```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<ArrayList<Integer> > FindContinuousSequence(int sum) {
       ArrayList<ArrayList<Integer>> lrs=new ArrayList<>();
        for(int n=(int)Math.sqrt(2*sum);n>=2;n--){//序列间按照开始数字从小到大的顺序
            if((n&1)==1&&sum%n==0||(sum%n)*2==n){
                ArrayList<Integer> list=new ArrayList<>();
                int i,j;
                for(i=0,j=(sum/n)-(n-1)/2;i<n;i++,j++){
                    list.add(j);
                }
                lrs.add(list);
            }
        }
        return lrs;
    }
}
```
