73. 二叉树的最近公共祖先 + 搜索二维矩阵 II + 最长不含重复字符的子字符串

这里有三题。
(1) 二叉树的最近公共祖先(同题 19)

leetcode 原题链接：236. 二叉树的最近公共祖先

难度级别：中等

题目：

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉树:  root = [3,5,1,6,2,0,8,null,null,7,4]

		3
	  /   \
	 5	   1
	/ \   / \
   6   2 0   8
      / \
     7   4

示例1：

    输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1 输出: 3 解释: 节点 5 和节点 1 的最近公共祖先是节点 3。

示例2：

    输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4 输出: 5 解释: 节点 5 和节点 4 的最近公共祖先是节点 5。因为根据定义最近公共祖先节点可以为节点本身。

说明：

    所有节点的值都是唯一的。
    p、q 为不同节点且均存在于给定的二叉树中。

思路：

  与找二叉搜索树的最近公共祖先类似，如果一个节点的左子树上有与p或q相等的节点且右子树上有与p或q相等的节点，说明此时该节点即为最近公共节点

递归
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null || p == root || q == root)
        	return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if(left == null)
        	return right;
        if(right == null)
        	return left;
        return root;
    }
}
```
(2) 搜索二维矩阵 II

leetcode 原题链接：240. 搜索二维矩阵 II

难度级别：中等

题目：

编写一个高效的算法来搜索 m x n 矩阵 matrix 中的一个目标值 target。该矩阵具有以下特性：

    每行的元素从左到右升序排列。
    每列的元素从上到下升序排列。

示例：

现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]

给定 target = 5，返回 true。

给定 target = 20，返回 false。

思路：

切割数组
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix.length == 0)
			return false;
        int m = matrix.length, n = matrix[0].length;
        int i=0,j=n-1;
        while(i<m && j>=0) {
        	if(matrix[i][j] < target) {
        		i++;
        	}else if(matrix[i][j] > target) {
        		j--;
        	}else {
        		return true;
        	}
        }
        return false;
    }
}
```
(3) 最长不含重复字符的子字符串

leetcode 原题链接：剑指 Offer 48. 最长不含重复字符的子字符串

难度级别：中等

题目：

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

示例1：

    输入: "abcabcbb" 输出: 3 解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

示例2：

    输入: "bbbbb" 输出: 1 解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。

示例3：

    输入: "pwwkew" 输出: 3 解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。   请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。

提示：

    s.length <= 40000

思路：

使用双指针加 set
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
		Set<Character> set = new HashSet<>();
        int left = 0, right = 0, max = 0;
        while(right < s.length()) {
            while(set.contains(s.charAt(right))) {
                set.remove(s.charAt(left));
                left++;
            }
            set.add(s.charAt(right));
            right++;
            max = Math.max(right - left, max);
        }
        return max;
    }
}
```
