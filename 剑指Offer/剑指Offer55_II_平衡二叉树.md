## &#127800; 剑指 Offer 55 - II. 平衡二叉树  &#127800;

### &#127826; 题目

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

##### 示例 1:

给定二叉树 `[3,9,20,null,null,15,7]`

```
    3
   / \
  9  20
    /  \
   15   7
```
返回 true 。

##### 示例 2:

给定二叉树 `[1,2,2,3,3,null,null,4,4]`

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```
返回 false 。

##### 限制：
0 <= 树的结点个数 <= 10000

### &#127826; 题解

- 先序遍历 + 判断深度 （从顶至底）
  - 
- 后序遍历 + 剪枝 （从底至顶）
  - 此方法为本题的最优解法，但剪枝的方法不易第一时间想到。

<details>
<summary>&#127808; 先序遍历 + 判断深度 （从顶至底） &#127808;</summary>

### 思路
思路是构造一个获取当前子树的深度的函数 depth(root) （即 面试题55 - I. 二叉树的深度 ），思路是构造一个获取当前子树的深度的函数 depth(root) （即 面试题55 - I. 二叉树的深度 ）
`abs(depth(root.left) - depth(root.right)) <= 1`
是否成立，来判断某子树是否是二叉平衡树。若所有子树都平衡，则此树平衡。



### 步骤
- **isBalanced(root) 函数**： 判断树 root 是否平衡
  - 特例处理： 若树根节点 root 为空，则直接返回 truetrue ；
  - 返回值： 所有子树都需要满足平衡树性质，因此以下三者使用与逻辑 \&\&&& 连接；
    1. abs(self.depth(root.left) - self.depth(root.right)) <= 1 ：判断 当前子树 是否是平衡树；
    2. self.isBalanced(root.left) ： 先序遍历递归，判断 当前子树的左子树 是否是平衡树；
    3. self.isBalanced(root.right) ： 先序遍历递归，判断 当前子树的右子树 是否是平衡树；
  
  
- **depth(root) 函数**： 计算树 root 的深度
  - 终止条件： 当 root 为空，即越过叶子节点，则返回高度 00 ；
  - 返回值： 返回左 / 右子树的深度的最大值 +1+1 。


<![1](https://pic.leetcode-cn.com/8464f2bae6181353f9960c9ada3f060672a7b309dd313155526efba0d3a8b38d-Picture12.png),![2](https://pic.leetcode-cn.com/997c6c77469be3c3cfada7d89a45cf56634742ee86140a7f0c970d8cd335cafe-Picture13.png),![3](https://pic.leetcode-cn.com/23fc976dcc45a11c7c2398da3d5c4bc49768f0fb6a8eacb14837f1e48bb16897-Picture14.png),![4](https://pic.leetcode-cn.com/36272beee5f24ed421e0267f39408c7304862e73a5e40737090226da24e93300-Picture15.png),![5](https://pic.leetcode-cn.com/f7b74ef888f602cd1215e8ebb04a3638e8a9566ce9b76a945e3f45e2f101a367-Picture16.png),![6](https://pic.leetcode-cn.com/06490aa3308753df2554cf86efccf70345394200fe98c2cf01b2451faee18d4b-Picture17.png)>
  
```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        if (root == null) return true;
        return Math.abs(depth(root.left) - depth(root.right)) <= 1 && isBalanced(root.left) && isBalanced(root.right);
    }

    private int depth(TreeNode root) {
        if (root == null) return 0;
        return Math.max(depth(root.left), depth(root.right)) + 1;
    }
}
```
  
## 复杂度分析：
  
- 时间复杂度 O(N log N)： 最差情况下（为 “满二叉树” 时）， isBalanced(root) 遍历树所有节点，判断每个节点的深度 depth(root) 需要遍历 各子树的所有节点 。
  
![](https://files.mdnice.com/user/1562/e82b1f76-5802-42c4-b16a-ca8d597932b2.png)

- 空间复杂度 O(N)： 最差情况下（树退化为链表时），系统递归需要使用 O(N) 的栈空间。

</details>
  
<details>
<summary>&#127808; BFS &#127808;</summary>

### 思路
- 思路是对二叉树做后序遍历，从底至顶返回子树深度，
- 若判定某子树不是平衡树则 “剪枝” ，直接向上返回。

### 步骤
- recur(root) 函数：
  - 返回值：
    1. 当节点root 左 / 右子树的深度差 ≤1 ：则返回当前子树的深度，即节点 root 的左 / 右子树的深度最大值 +1 （ max(left, right) + 1 ）；
    2. 当节点root 左 / 右子树的深度差 >2 ：则返回 −1 ，代表 **此子树不是平衡树** 。
  - 终止条件：
    1. 当 root 为空：说明越过叶节点，因此返回高度 0 ；
    2. 当左（右）子树深度为 -1 ：代表此树的 **左（右）子树** 不是平衡树，因此剪枝，直接返回 −1 ；
  
- isBalanced(root) **函数**：

- 返回值： 若 recur(root) != -1 ，则说明此树平衡，返回 true ； 否则返回 false 。



<![1](https://pic.leetcode-cn.com/001672aae76bc81f0a5cd237163b3d48e554d1e2051c7f62f8ca836579a8d58a-Picture2.png),![2](https://pic.leetcode-cn.com/2adb8e019afec7079b58bfa8c841d10dc9ff29af2942672c6d7f341cd4f0ac06-Picture3.png),![3](https://pic.leetcode-cn.com/43ea0075ea08373d971c05725c9b049f42405f9d4a2399f5d6d03f043e9737ad-Picture4.png),![4](https://pic.leetcode-cn.com/ea59831b3e50203ff7751f8fc1a26cebe630b2bf47d5b4a22feba023af5757b5-Picture5.png),![5](https://pic.leetcode-cn.com/24d38dffc26e333ee92b8ac505586d4fe89b6d3e1bdd660d1130288429b64461-Picture6.png),![6](https://pic.leetcode-cn.com/dc5f22d5798cd4ef4fcc1ba2db268cf41dfb112df33350b36cbe1d84cacf4573-Picture7.png),![7](https://pic.leetcode-cn.com/6a56da4adeb7730e97d1ae46829e9e7bec8c2ed4eb45a88f6e7bfdc77c0c419b-Picture8.png),![8](https://pic.leetcode-cn.com/c0b1b016e1f3255cb65a1df3aaa1d3ff19bd6701a0d372fc9626c28865d7219d-Picture9.png),![9](https://pic.leetcode-cn.com/8f1b123e15154ddcb6656bdd37696eefe2ccfc452a23534943753ca1f7bb12b7-Picture10.png),![10](https://pic.leetcode-cn.com/350bae669dfe5d3aec8a371fac860fcfa12b77e5dbc17ada2abf51a27b0985a5-Picture11.png)>
  
```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return recur(root) != -1;
    }

    private int recur(TreeNode root) {
        if (root == null) return 0;
        int left = recur(root.left);
        if(left == -1) return -1;
        int right = recur(root.right);
        if(right == -1) return -1;
        return Math.abs(left - right) < 2 ? Math.max(left, right) + 1 : -1;
    }
}
```
  
## 复杂度分析：
  
时间复杂度 O(N)： N 为树的节点数；最差情况下，需要递归遍历树的所有节点。
空间复杂度 O(N)： 最差情况下（树退化为链表时），系统递归需要使用 O(N) 的栈空间。


</details>
  
[参考](Krahets "链接：https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/solution/mian-shi-ti-55-i-er-cha-shu-de-shen-du-xian-xu-bia/")