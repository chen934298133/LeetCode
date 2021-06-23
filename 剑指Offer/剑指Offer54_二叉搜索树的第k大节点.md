## &#127800; 剑指 Offer 54. 二叉搜索树的第k大节点  &#127800;

### &#127826; 题目

给定一棵二叉搜索树，请找出其中第k大的节点。

##### 示例一：
输入: root = `[3,1,4,null,2]`, k = 1
```
   3
  / \
 1   4
  \
   2
```
输出: 4

##### 示例二：
输入: root = `[5,3,6,2,4,null,null,1]`, k = 3
```
       5
      / \
     3   6
    / \
   2   4
  /
 1
```
输出: 4

##### 
1 ≤ k ≤ 二叉搜索树元素个数

### &#127826; 题解


<details>
<summary>&#127808; 广度优先搜索（BFS）+ 双端队列 &#127808;</summary>

### 思路
- 注意是二叉搜索树，不是二叉树，那么不需要排序，本题即变为简单题
  - 二叉搜索树的中序遍历为 递增序列 。
  - 根据以上性质，易得二叉搜索树的 **中序遍历倒序** 为 **递减序列** 。
  - 因此，`求二叉搜索树第 k 大的节点` 可转化为求 `此树的中序遍历倒序的第 k 个节点`。

- 为求第 kk 个节点，需要实现以下 三项工作 ：
    1. 递归遍历时计数，统计当前节点的序号；
    2. 递归到第 kk 个节点时，应记录结果 resres ；
    3. 记录结果后，后续的遍历即失去意义，应提前终止（即返回）。

<details>
<summary>&#127808; 中序遍历 &#127808;</summary>

```java
void dfs(TreeNode root) {
    if(root == null) return;
    dfs(root.left); // 左
    System.out.println(root.val); // 根
    dfs(root.right); // 右
}
```
  
</details>
  
<details>
<summary>&#127808; 中序遍历倒序 &#127808;</summary>

```java
void dfs(TreeNode root) {
    if(root == null) return;
    dfs(root.right); // 右
    System.out.println(root.val); // 根
    dfs(root.left); // 左
}

```
  
</details>
  
![](https://pic.leetcode-cn.com/4ebcaefd4ecec0d76bfab98474dfed323fb86bfcd685d1a5bf610200fdca4405-Picture1.png)  
 
## 步骤
1. 终止条件： 当节点 rootroot 为空（越过叶节点），则直接返回；
2. 递归右子树： 即 dfs(root.right)dfs(root.right) ；
3. 三项工作：
    1. 提前返回： 若 k = 0k=0 ，代表已找到目标节点，无需继续遍历，因此直接返回；
    2. 统计序号： 执行 k = k - 1k=k−1 （即从 kk 减至 00 ）；
    3. 记录结果： 若 k = 0k=0 ，代表当前节点为第 kk 大的节点，因此记录 res = root.valres=root.val ；
4. 递归左子树： 即 dfs(root.left)dfs(root.left) ；


  
```java
class Solution {
    int res, k;
    public int kthLargest(TreeNode root, int k) {
        this.k = k;
        dfs(root);
        return res;
    }
    void dfs(TreeNode root) {
        if(root == null) return;
        dfs(root.right);
        if(k == 0) return;
        if(--k == 0) res = root.val;
        dfs(root.left);
    }
}
```
  
</details>
  
  
[参考](Krahets "链接：https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/solution/mian-shi-ti-54-er-cha-sou-suo-shu-de-di-k-da-jie-d/")