## &#127800; 剑指 Offer 68 - II. 二叉树的最近公共祖先  &#127800;

### &#127826; 题目

给定一个**二叉树**, 找到该树中两个指定节点的最近公共祖先。

给定如下二叉搜索树:  root = `[3,5,1,6,2,0,8,null,null,7,4]`

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/15/binarytree.png)

##### 示例 1:
> 输入: root = `[3,5,1,6,2,0,8,null,null,7,4]`, p = 5, q = 1<br>
> 输出: 3 <br>
> 解释: 节点 2 和节点 8 的最近公共祖先是 6。<br>

##### 示例 2:

> 输入:  root = `[3,5,1,6,2,0,8,null,null,7,4]`, p = 5, q = 4<br>
> 输出: 5 <br>
> 解释: 节点 5 和节点 4 的最近公共祖先是节点 5。因为根据定义最近公共祖先节点可以为节点本身。。<br>

##### 说明：
- 所有节点的值都是唯一的。
- p、q 为不同节点且均存在于给定的二叉树中。

### &#127826; 题解

- 过递归对二叉树进行后序遍历，
  - 当遇到节点 p 或 q 时返回，从底至顶回溯。
  - 当节点 p,q 在节点 root 的异侧时，节点 root 即为最近公共祖先，则向上返回 root 。



<details>
<summary>&#127808; 迭代 &#127808;</summary>

### 思路
- 迭代
  
### 步骤
- 终止条件：
    1. 当越过叶节点，则直接返回 nullnull ；
    2. 当 rootroot 等于 p, qp,q ，则直接返回 rootroot ；
- 递推工作：
    1. 开启递归左子节点，返回值记为 leftleft ；
    2. 开启递归右子节点，返回值记为 rightright ；
- 返回值： 根据 leftleft 和 rightright ，可展开为四种情况；
    1. 当 leftleft 和 rightright 同时为空 ：说明 rootroot 的左 / 右子树中都不包含 p,qp,q ，返回 nullnull ；
    2. 当 leftleft 和 rightright 同时不为空 ：说明 p, qp,q 分列在 rootroot 的 异侧 （分别在 左 / 右子树），因此 rootroot 为最近公共祖先，返回 rootroot ；
    3. 当 leftleft 为空 ，rightright 不为空 ：p,qp,q 都不在 rootroot 的左子树中，直接返回 rightright 。具体可分为两种情况：
        1. p,qp,q 其中一个在 rootroot 的 右子树 中，此时 rightright 指向 pp（假设为 pp ）；
        2. p,qp,q 两节点都在 rootroot 的 右子树 中，此时的 rightright 指向 最近公共祖先节点 ；
    4. 当 leftleft 不为空 ， rightright 为空 ：与情况 3. 同理；

- 观察发现， 情况 1. 可合并至 3. 和 4. 内，详见文章末尾代码。

<![1](https://pic.leetcode-cn.com/c44f8946548954a2513f7d72e20be260c36c157b506749c788afce1e7bd3416c-Picture1.png),![2](https://pic.leetcode-cn.com/55f7683ceee27def129a50c9a26305e56b25175dbd3da55983b5848145559354-Picture2.png),![3](https://pic.leetcode-cn.com/0c3217c102953090030aec857ef2e1e96672b38c450a90356a3e64f0dfc97af2-Picture3.png),![4](https://pic.leetcode-cn.com/f137a75004bf105ae2f9d2987d3d75c0d0cbddfda54126e549b5a3a99b06a6ef-Picture4.png),![5](https://pic.leetcode-cn.com/3334d8bc74cad490584a03ca6e6637f4d431626f75ca589710d6a382fe9ab06b-Picture5.png),![6](https://pic.leetcode-cn.com/fd6ef030cf8acac250792828c04df471ccab669d4153b49b934bc4cc3517efcf-Picture6.png),![7](https://pic.leetcode-cn.com/e03f2505635e77816e12bdfd2ce5c1c4ace3d2dfa2a0e10eefe683e11e88c98b-Picture7.png),![8](https://pic.leetcode-cn.com/a9cf21e0a271c74af5ab00e39da09d485de8a3dabbfaa6d6cd2a2a1c7f60d2a8-Picture8.png),![9](https://pic.leetcode-cn.com/6540e7106efa4461cb19c21a682e9b7c9bd33367d6c5a8bd97982cc7bcec9ec3-Picture9.png),![10](https://pic.leetcode-cn.com/d249c4379aee12e4a5bce4f20c4ad8b709ff35e358cfdb3255ed6d9c6dc4ae2c-Picture10.png),![11](https://pic.leetcode-cn.com/fa87c46c8e8360cf3ab5ea852161ab5f9e4a2ca1b5ff6cd9e9ba0897dcbd455a-Picture11.png),![12](https://pic.leetcode-cn.com/91287818231c969dcc8c69ac9c79197a9b29085d120b18b5230dda77d092f6d6-Picture12.png),![13](https://pic.leetcode-cn.com/bf71136a0329cf5d48933cb7dc1d8c1bd0cec96c1ad13bcca97cea2f58d14fb5-Picture13.png),![14](https://pic.leetcode-cn.com/68aced35d03027033c2552b35d477d700e38e7c01f8c1fa76b4cf8b0a1858d30-Picture14.png),![15](https://pic.leetcode-cn.com/ddf6279a32122924d3608ad7fcdf3f518091da353a1961c0e0e1afaf51d09623-Picture15.png),![16](https://pic.leetcode-cn.com/b4777e4a6ff72ed49356e20a0a897fd866bb3e4dfdb5e0c8fc1dc0f918029237-Picture16.png),![17](https://pic.leetcode-cn.com/df510a1fe4750116a935e61ef63ad30a5092bfefe38845497ff9431b3656a793-Picture17.png),![18](https://pic.leetcode-cn.com/0724b87055c4bc4d744ab64775e6eefa348777c0ea0b07a00ff917773f4b494e-Picture18.png)>
  
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null || root == p || root == q) return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if(left == null && right == null) return null; // 1.
        if(left == null) return right; // 3.
        if(right == null) return left; // 4.
        return root; // 2. if(left != null and right != null)
    }
}
```
优化：情况 1. 合并至 3. 和 4. 内
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null || root == p || root == q) return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if(left == null) return right;
        if(right == null) return left;
        return root;
    }
}
```   
## 复杂度分析：
  
- 时间复杂度 O(N) ： 其中 N 为二叉树节点数；最差情况下，需要递归遍历树的所有节点。
- 空间复杂度 O(N) ： 最差情况下，递归深度达到 N ，系统使用 O(N) 大小的额外空间。

</details>
  
<details>
<summary>&#127808; 迭代 &#127808;</summary>

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null) return null; // 如果树为空，直接返回null
        if(root == p || root == q) return root; // 如果 p和q中有等于 root的，那么它们的最近公共祖先即为root（一个节点也可以是它自己的祖先）
        TreeNode left = lowestCommonAncestor(root.left, p, q); // 递归遍历左子树，只要在左子树中找到了p或q，则先找到谁就返回谁
        TreeNode right = lowestCommonAncestor(root.right, p, q); // 递归遍历右子树，只要在右子树中找到了p或q，则先找到谁就返回谁
        if(left == null) return right; // 如果在左子树中 p和 q都找不到，则 p和 q一定都在右子树中，右子树中先遍历到的那个就是最近公共祖先（一个节点也可以是它自己的祖先）
        else if(right == null) return left; // 否则，如果 left不为空，在左子树中有找到节点（p或q），这时候要再判断一下右子树中的情况，如果在右子树中，p和q都找不到，则 p和q一定都在左子树中，左子树中先遍历到的那个就是最近公共祖先（一个节点也可以是它自己的祖先）
        else return root; //否则，当 left和 right均不为空时，说明 p、q节点分别在 root异侧, 最近公共祖先即为 root
    }
}
```
</details>

  
[参考](Krahets "链接：https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/solution/mian-shi-ti-68-i-er-cha-sou-suo-shu-de-zui-jin-g-7/")