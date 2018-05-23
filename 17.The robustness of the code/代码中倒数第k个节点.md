# 代码中倒数第k个节点
## 问题描述
输入一个链表，输出该链表中倒数第k个结点。
## 解决方法
### 方法一：
遍历整个链表，使每个节点入栈，然后依次出栈，第k个元素即为链表的倒数第k个节点。注意：k的值要小于链表节点数且大于0，head不为空。
```java
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}
import java.util.Stack;
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        if(head==null||k<=0)
            return null;
        Stack<ListNode> stack=new Stack<ListNode>();
		ListNode p=head;
        int count=0;
		while(p!=null){
			stack.push(p);
            count++;
			p=p.next;
		}
        if(count<k)
            return null;
		while(k>0){
			p=stack.pop();
			k--;
		}
		return p;
    }
}
```
### 方法二：
使用两个指针，从头到尾遍历链表，让其中一个指针先走i-1步，然后另一个指针和先走的指针一起走，它们之间的距离为i-1；当先走的指针到链尾时，后走的指针指向的元素即为倒数第k个指针。
```java
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        if(head==null||k==0)
            return null;
        ListNode pAhead=head;
        ListNode pBehind=null;
        for(int i=0;i<k-1;i++){
            if(pAhead.next!=null)
                pAhead=pAhead.next;
            else
                return null;
        }
        pBehind=head;
        while(pAhead.next!=null){
            pAhead=pAhead.next;
            pBehind=pBehind.next;
        }
        return pBehind;
    }
}
```
