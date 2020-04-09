# <center>NO6 重建二叉树
>题目要求

    输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

>已知前序、中序、求后序遍历
    例如：

    前序遍历:         1,2,4,7,3,5,6,8

    中序遍历:        4,7,2,1,5,3,8,6

>画树求法：

    1. 题目中给了我们先序遍历和中序遍历；在二叉树的前序遍历中，第一个数字总是树的根结点的值。但在中序遍历序列中，根结点的值在序列的中间，左子树的结点的值位于根结点的值的左边，而右子树的结点的值位于根结点的值的右边。因此我们需要扫描中序遍历序列，才能找到根结点的值。

    2. 题目给出的前序遍历序列的第一个数字1就是根结点的值。扫描中序遍历序列，就能确定根结点的值的位置。根据中序遍历的特点，在根结点的值1前面的3个数字都是左子树结点的值，位于1后面的数字都是右子树结点的值。

    3. 由于在中序遍历序列中，有3个数字是左子树结点的值，因此左子树总共有3个左子结点。同样，在前序遍历的序列中，根结点后面的3个数字就是3个左子树结点的值，再后面的所有数字都是右子树结点的值。这样就在前序和中序遍历的两个序列中，分别找到了左右子树对应的子序列。

    4. 我们已经分别找到了左右子树的前序和中序遍历，我们可以用同样的方法分别去构建左右子树，即递归实现。

1 确定根,确定左子树，确定右子树。

2 在左子树中递归。

3 在右子树中递归。

4 打印当前根。

那么，我们可以画出这个二叉树的形状：


>实例
<center><img src = "img/01.png"></center>
    
    前序遍历：1,2,4,7,3,5,6,8 根左右
    后序遍历：4,7,2,1,5,3,8,6 左右根
>代码
```java

/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
 public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
         TreeNode root=reConstructBinaryTree(pre,0,pre.length-1,in,0,in.length-1);
        return root;
    }
    //前序遍历{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}
    private TreeNode reConstructBinaryTree(int [] pre,int startPre,int endPre,int [] in,int startIn,int endIn) {
          
        if(startPre>endPre||startIn>endIn)//终止递归条件
            return null;
        TreeNode root=new TreeNode(pre[startPre]);
          
        for(int i=startIn;i<=endIn;i++)
            if(in[i]==pre[startPre]){
                //(i-startIn)左子树的元素个数
                //左子树
                root.left=reConstructBinaryTree(pre,startPre+1,startPre+(i-startIn),in,startIn,i-1);
                //右子树
                root.right=reConstructBinaryTree(pre,(i-startIn)+startPre+1,endPre,in,i+1,endIn);
            }
                  
        return root;
    }
}
```

>举一反三：

    类似的由中序和后序构建二叉树和有前序和中序构建二叉树的思想是类似的。重建二叉树可以有前序和中序推导出来，也可以由中序和后序推导出来。这里实现由中序和后序重建二叉树。

>代码
```java

/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
public static TreeNode rebuildBinaryTree(int[] postorder, int[] inorder) {
	if (postorder == null || inorder == null) {
		return null;
	}
	TreeNode root = rebuildBinaryTreeCore(postorder, 0,
			postorder.length - 1, inorder, 0, inorder.length - 1);
	return root;
}
 
public static TreeNode rebuildBinaryTreeCore(int[] postorder,
		int startPostorder, int endPostorder, int[] inorder,
		int startInorder, int endInorder) {
 
	if (startPostorder > endPostorder || startInorder > endInorder) { // 终止递归的条件
		return null;
	}
	TreeNode root = new TreeNode(postorder[endPostorder]);
	for (int i = startInorder; i <= endInorder; i++) {
		if (inorder[i] == postorder[endPostorder]) {
			root.left = rebuildBinaryTreeCore(postorder, startPostorder,
					startPostorder - 1 + (i - startInorder), inorder,
					startInorder, i - 1);
			root.right = rebuildBinaryTreeCore(postorder, startPostorder
					+ (i - startInorder), endPostorder - 1, inorder, i + 1,
					endInorder);
		}
	}
	return root;
}
}
```
