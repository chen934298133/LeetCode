## &#127800; 剑指 Offer 28. 对称的二叉树 &#127800;

### &#127826; 题目

###### 请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:
```
    1
   / \
  2   2
   \   \
   3    3
```
**示例 1：**<br>

输入：root = [1,2,2,3,4,4,3] <br>
输出：true <br>


**示例 2：**

输入：root = [1,2,2,null,3,null,3]<br>
输出：false

**限制：**<br>
`0 <= 节点个数 <= 1000`

### &#127826; 题解


<details>
<summary>&#127808; View The Codes &#127808;</summary>

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
    public boolean isSymmetric(TreeNode root) {
        // 若根节点 root 为空，则直接返回 truetruetrue
        return root == null ? true : recur(root.left, root.right);
    }
  
    // 递归
    boolean recur(TreeNode L, TreeNode R) {
        // 当 LLL 和 RRR 同时越过叶节点： 此树从顶至底的节点都对称，因此返回 true
        if(L == null && R == null) return true;
        // 当 LLL 或 RRR 中只有一个越过叶节点： 此树不对称，返回 false
        // 当节点 L ！= 节点 R 值，此树不对称，返回 false
        if(L == null || R == null || L.val != R.val) return false;
        // 两对节点都对称时，才是对称树，因此用与逻辑符 && 连接。
        return recur(L.left, R.right) && recur(L.right, R.left);
    }
}
```
</details>
