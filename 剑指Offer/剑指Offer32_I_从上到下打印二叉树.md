&#127800; 剑指 Offer 32 - I. 从上到下打印二叉树 &#127800;

### &#127826; 题目

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

- 例如:
给定二叉树: `[3,9,20,null,null,15,7]`
```
    3
   / \
  9  20
    /  \
   15   7
```

- 返回：

`[3,9,20,15,7]`

- 提示：
`节点总数 <= 1000`

### &#127826; 题解


<details>
<summary>&#127808; 广度优先搜索（BFS） &#127808;</summary>

### 思路
- 广度优先搜索（BFS）
  - BFS 通常借助 队列 的先入先出特性来实现。

### 步骤
1. 特例处理： 当树的根节点为空，则直接返回空列表 [] ；
2. 初始化： 打印结果列表 res = [] ，包含根节点的队列 queue = [root] ；
3. BFS 循环： 当队列 queue 为空时跳出；
    - 出队： 队首元素出队，记为 node；
    - 打印： 将 node.val 添加至列表 tmp 尾部；
    - 添加子节点： 若 node 的左（右）子节点不为空，则将左（右）子节点加入队列 queue ；
4. 返回值： 返回打印结果列表 res 即可。
  
<![1](https://pic.leetcode-cn.com/81604b4d1970088e7ed58e2b2243735e441e64c3aa1f22a5d595ec4b4ad2c351-Picture1.png),![2](https://pic.leetcode-cn.com/bf865a277b6ab6e3c2684b23e4b186305876fe38f8c2e7db2dd35b43ead41ab9-Picture2.png),![3](https://pic.leetcode-cn.com/e282c67bd76355c77af24ecf9f4bc19190f5e024face86422cab17ef5de449b6-Picture3.png),![4](https://pic.leetcode-cn.com/1d7590d312a484b9b47e532f4662be769585fe5eaba69f2f5faeed06027997a3-Picture4.png),![5](https://pic.leetcode-cn.com/92136b0557c7fd88b314d089e6faf33f91abaaeb0ba1ca6b29ebd1b59656ce98-Picture5.png),![6](https://pic.leetcode-cn.com/03a0fc894740a6ea79b48c8e3dca402661c650fd5c0c06e639bd27baca8517ff-Picture6.png),![7](https://pic.leetcode-cn.com/9ab182cc66f6ca12c2b587106d3982b2114da24ec9569e7be3d0f0547f2e07b9-Picture7.png),![8](https://pic.leetcode-cn.com/a3591e9682de1be4944802bb51d94ec0256217dc0741020c0f680470f788d32d-Picture8.png),![9](https://pic.leetcode-cn.com/bc8d6229f7e22607fa624cf8cb06cd810850c21f1a682a52b29109908cbbe2bd-Picture9.png),![10](https://pic.leetcode-cn.com/9aa6400bb899b4d3ac5412f1750c6bbfa0ade5d7a7dad73b119a2dd44541b121-Picture10.png),![11](https://pic.leetcode-cn.com/cd3572f1cf8d859607e69706f513e69f7c93167fea781cd8801efd36cf962cca-Picture11.png),![12](https://pic.leetcode-cn.com/afc24744e6e087232cadb11e0d521b740190e5f8e56a115cea6243059dc709df-Picture12.png),![13](https://pic.leetcode-cn.com/df88918f467ebdbc7e84e766a1b7c28532ab0529ef37fdcbdd9a7075af1e5cdc-Picture13.png),![14](https://pic.leetcode-cn.com/d4caeb99e97cb8468ab9c31b823faa6dc792fde9cc68c0d9ce3a6f10a9a3cc3d-Picture14.png),![15](https://pic.leetcode-cn.com/27ac8470be8628c9848f6329a57fcda49510ef226a91354dcd5d063dcd56662d-Picture15.png),![16](https://pic.leetcode-cn.com/0303d49a3b2eddfd68343fc507e84eed1a8f45b191794b067ba47f04527df353-Picture16.png),![17](https://pic.leetcode-cn.com/c6ce654ff63d54592344cded38b0040a551c866e7662d71f6725148f265eb9cd-Picture17.png)>
  
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
    public int[] levelOrder(TreeNode root) {
        // 1. 当树的根节点为空，则直接返回空列表 [] ；
        if(root == null) return new int[0];

        // 2. 初始化容器
        // Queue: 包含根节点的队列 queue = [root]
        // List: 打印结果列表 res = []
        Queue<TreeNode> queue = new LinkedList(){{ add(root); }};
        ArrayList<Integer> ans = new ArrayList<>();

        // 3. 当队列 queue 为空时跳出；
        while(!queue.isEmpty()) {
            // 1. 出队： 队首元素出队，记为 node；
            TreeNode node = queue.poll();
            // 2. 将 node.val 添加至列表 tmp 尾部；
            ans.add(node.val);
            // 3. 添加子节点： 若 node 的左（右）子节点不为空，则将左（右）子节点加入队列 queue ；
            if(node.left != null) queue.add(node.left);
            if(node.right != null) queue.add(node.right);
        }

        // 将 List 转为 int数组并返回
        int[] res = new int[ans.size()];
        for(int i = 0; i < ans.size(); i++){
            res[i] = ans.get(i);
        }
        System.out.println(Arrays.toString(ans.toArray()));
        return res;
    }
}
```
  
</details>
  

[参考](Krahets "链接：https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/solution/mian-shi-ti-32-i-cong-shang-dao-xia-da-yin-er-ch-4/")