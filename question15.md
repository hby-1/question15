# 左叶子之和

给定二叉树的根节点 `root` ，返回所有左叶子之和。

## 示例 1：
![alt text](image.png)
>### 输入: 
>root = [3,9,20,null,null,15,7]
>### 输出:
>24
>### 解释:
>在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24

## 示例 2：
>### 输入:
>root = [1]
>### 输出:
>0

## 代码：
1.

    /**
    * Definition for a binary tree node.
    * public class TreeNode {
    *     public int val;
    *     public TreeNode left;
    *     public TreeNode right;
    *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
    *         this.val = val;
    *         this.left = left;
    *         this.right = right;
    *     }
    * }
    */
    public class Solution {
        public int SumOfLeftLeaves(TreeNode root) {
            int sum = 0;
            Queue<TreeNode> queue = new Queue<TreeNode>();
            queue.Enqueue(root);
            while (queue.Count > 0) {
                TreeNode node = queue.Dequeue();
                if (node.left != null) {
                    if (IsLeaf(node.left)) {
                        sum += node.left.val;
                    } else {
                        queue.Enqueue(node.left);
                    }
                }
                if (node.right != null) {
                    if (!IsLeaf(node.right)) {
                        queue.Enqueue(node.right);
                    }
                }
            }
            return sum;
        }

        public bool IsLeaf(TreeNode node) {
            return node.left == null && node.right == null;
        }
    }
2.

    /**
    * Definition for a binary tree node.
    * public class TreeNode {
    *     public int val;
    *     public TreeNode left;
    *     public TreeNode right;
    *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
    *         this.val = val;
    *         this.left = left;
    *         this.right = right;
    *     }
    * }
    */
    public class Solution {
        public int SumOfLeftLeaves(TreeNode root) {
            if(root==null){
                return 0;
            }
            int sum=0;
            if (root.left != null && root.left.left == null && root.left.right == null) {
                sum += root.left.val;
            } else {
                // 递归计算左子树中的左叶子节点
                sum += SumOfLeftLeaves(root.left);
            }
            sum += SumOfLeftLeaves(root.right);
            return sum;
        }
    }
3.

    /**
    * Definition for a binary tree node.
    * public class TreeNode {
    *     public int val;
    *     public TreeNode left;
    *     public TreeNode right;
    *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
    *         this.val = val;
    *         this.left = left;
    *         this.right = right;
    *     }
    * }
    */
    public class Solution {
        public int SumOfLeftLeaves(TreeNode root) {
            int sum = 0;
            if (root.left != null) {
                if (IsLeaf(root.left)) {
                    sum += root.left.val;
                } else {
                    sum += SumOfLeftLeaves(root.left);
                }
            }
            if (root.right != null && !IsLeaf(root.right)) {
                sum += SumOfLeftLeaves(root.right);
            }
            return sum;
        }

        public bool IsLeaf(TreeNode node) {
            return node.left == null && node.right == null;
        }
    }

