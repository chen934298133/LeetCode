## &#127800; 剑指 Offer 68 - I. 二叉搜索树的最近公共祖先  &#127800;

### &#127826; 题目

给定一个**二叉搜索树**, 找到该树中两个指定节点的最近公共祖先。

给定如下二叉搜索树:  root = `[6,2,8,0,4,7,9,null,null,3,5]`

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/binarysearchtree_improved.png)

##### 示例 1:
> 输入: root = `[6,2,8,0,4,7,9,null,null,3,5]`, p = 2, q = 8<br>
> 输出: 6 <br>
> 解释: 节点 2 和节点 8 的最近公共祖先是 6。<br>

##### 示例 2:

> 输入: root = `[6,2,8,0,4,7,9,null,null,3,5]`, p = 2, q = 4<br>
> 输出: 2<br>
> 解释: 节点 2 和节点 4 的最近公共祖先是 2, 因为根据定义最近公共祖先节点可以为节点本身。<br>

##### 说明：
- 所有节点的值都是唯一的。
- p、q 为不同节点且均存在于给定的二叉搜索树中。

### &#127826; 题解

- 本题给定了两个重要条件：
  - ① 树为 **二叉搜索树** ，
  - ② 树的所有节点的值都是 **唯一** 的。
  
根据以上条件，可方便地判断 p,q 与 root 的子树关系，即：
- 若 root.val < p.val ，则 p 在 root **右子树** 中；
- 若 root.val > p.val ，则 p 在 root **左子树** 中；
- 若 root.val = p.val ，则 p 和 root 指向 **同一节点** 。


<details>
<summary>&#127808; 迭代 &#127808;</summary>

### 思路
- 迭代
  
### 步骤
- 循环搜索： 当节点 root 为空时跳出；
    1. 当 p, q 都在 root 的 **右子树** 中，则遍历至 root.right ；
    2. 否则，当 p, q 都在 root 的 **左子树** 中，则遍历至 root.left ；
    3. 否则，说明找到了 **最近公共祖先** ，跳出。
- 返回值： 最近公共祖先 root 。


<![1](https://pic.leetcode-cn.com/f66371f5682d214f0fde7957e754e98d70a81e6f7182843fa274411dca632de2-Picture3.png),![2](https://pic.leetcode-cn.com/2f21fc1821859d8cdd28d2c0edacab7d30121292d6c9112d9ab9a56dc6932445-Picture4.png),![3](https://pic.leetcode-cn.com/f6a8b6d148fc1e223991f8b558bdd42719e58c8cfb131aaac0fbb8c41e4026b1-Picture5.png),![4](https://pic.leetcode-cn.com/ed42815f9c30b0b7a51cf8f35ed0011de8b773b096ad9fa8fe4fc710747fa9c5-Picture6.png)>
  
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        while(root != null) {
            if(root.val < p.val && root.val < q.val) // p,q 都在 root 的右子树中
                root = root.right; // 遍历至右子节点
            else if(root.val > p.val && root.val > q.val) // p,q 都在 root 的左子树中
                root = root.left; // 遍历至左子节点
            else break;
        }
        return root;
    }
}
```
优化：若可保证 p.val < q.val ，则在循环中可减少判断条件。
```
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(p.val > q.val) { // 保证 p.val < q.val
            TreeNode tmp = p;
            p = q;
            q = tmp;
        }
        while(root != null) {
            if(root.val < p.val) // p,q 都在 root 的右子树中
                root = root.right; // 遍历至右子节点
            else if(root.val > q.val) // p,q 都在 root 的左子树中
                root = root.left; // 遍历至左子节点
            else break;
        }
        return root;
    }
}
```                     
## 复杂度分析：
  
- 时间复杂度 O(N) ： 其中 N 为二叉树节点数；每循环一轮排除一层，二叉搜索树的层数最小为 ${\log N}$ （满二叉树），最大为 N （退化为链表）。
- 空间复杂度 O(1) ： 使用常数大小的额外空间。

</details>
  
<details>
<summary>&#127808; 递归 &#127808;</summary>

### 思路
- 递归

### 步骤
- **递推工作**：
    1. 当 p, q 都在 root 的 **右子树** 中，则开启递归 root.right 并返回；
    2. 否则，当 p, q 都在 root 的 **左子树** 中，则开启递归 root.left 并返回；
- **返回值**： 最近公共祖先 root 。
  
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
            //终止条件：不需要，因为官方给了均存在与树中的条件
            //          即老子现在肯定是这两个乖孙子的公共祖先
            //递推操作：
            //第一种情况：
            if(root.val>p.val&&root.val>q.val){//看看是不是都是左儿子的后代
                return lowestCommonAncestor(root.left,p,q);//是的话就丢给左儿子去认后代（继续递归）
            }
            //第二种情况：
            if(root.val<p.val&&root.val<q.val){//不是左儿子的后代，看看是不是都是右儿子的后代
                return lowestCommonAncestor(root.right,p,q);//是的话就丢给右儿子去认后代（继续递归）
            }
            //第三种情况：
            //左儿子和右儿子都说我只认识一个，唉呀妈呀，那就是老子是你们最近的祖先，因为老子本来就是你们的公共的祖先
            //现在都只认一个，那就是老子是最近的。
            //其实第三种才是题目需要找到的解，所以返回，拜托我的祖先们也传一下（递归回溯返回结果），我才是他们最近的公共曾爷爷
        return root;
    }
}
```
  
## 复杂度分析：
  
- **时间复杂度 O(N)** ： 其中 N 为二叉树节点数；每循环一轮排除一层，二叉搜索树的层数最小为 ${\log N} （满二叉树），最大为 N （退化为链表）。
- **空间复杂度 O(N)** ： 最差情况下，即树退化为链表时，递归深度达到树的层数 N 。

</details>
  
[参考](Krahets "链接：https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/solution/mian-shi-ti-68-i-er-cha-sou-suo-shu-de-zui-jin-g-7/")