# 包含min函数的栈
## 问题描述
定义栈的数据结构，请在该类型中实现一个能够得到栈最小元素的min函数。
## 解决方法
声明原始和辅助两个栈，一个存储原始数据，另一个存储当前原始栈中的最小数字，栈顶就是栈中最小数字。当弹出一个数字时，两个栈弹出栈顶元素；当压入一个元素时，
原始压入数字，辅助栈栈顶元素如果大于栈顶元素或栈为空时，则压入该元素，否则压入栈顶元素。注意：Java中获取栈顶元素的函数是peek()。
```java
import java.util.Stack;

public class Solution {
    private Stack<Integer> s=new Stack<Integer>();
    private Stack<Integer> m=new Stack<Integer>();
    
    public void push(int node) {
        s.push(node);
        if(m.size()==0||m.peek()>node){
            m.push(node);
        }else{
            m.push(m.peek());
        }
    }
    
    public void pop() {
        if(s.size()>0&&m.size()>0){
            s.pop();
            m.pop();
        }
    }
    
    public int top() {
        return s.peek();
    }
    
    public int min() {
        return m.peek();
    }
}
```
