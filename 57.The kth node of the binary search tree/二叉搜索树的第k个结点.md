# 二叉搜索树的第k个结点
## 问题描述
给定一棵二叉搜索树，请找出其中的第k小的结点。例如，（5，3，7，2，4，6，8）中，按结点数值大小顺序第三小结点的值为4。
## 解决方法
二叉树的中序遍历即为顺序遍历。
```java
/*
public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;

    }

}
*/
public class Solution {
    int flag=0;
    TreeNode p=null;
    TreeNode KthNode(TreeNode pRoot, int k)
    {
        if(pRoot==null)
            return null;
        KthNode(pRoot.left,k);
        flag++;
        if(flag==k)
            p=pRoot;
        KthNode(pRoot.right,k);
        return p;
    }
}
```