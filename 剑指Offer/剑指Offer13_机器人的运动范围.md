## &#127800; 剑指 Offer 13. 机器人的运动范围 &#127800;

### &#127826; 题目

地上有一个`m`行`n`列的方格，从坐标 `[0,0]` 到坐标 `[m-1,n-1]` 。一个机器人从坐标 `[0, 0]` 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于`k`的格子。例如，当`k`为`18`时，机器人能够进入方格 `[35, 37]` ，因为`3+5+3+7=18`。但它不能进入方格 `[35, 38]`，因为`3+5+3+8=19`。请问该机器人能够到达多少个格子？

**示例 1：**<br>
输入：m = 2, n = 3, k = 1<br>
输出：3

**示例 2：**<br>
输入：m = 3, n = 1, k = 0<br>
输出：1<br>

**提示：**

- `1 <= n,m <= 100`
- `0 <= k <= 20`

### &#127826; 题解


<details>
<summary>&#127808; DFS + 剪枝 &#127808;</summary>

### 思路
- 题目中描述是从 (0,0) 位置开始的，每次只能走一格，上下左右都行
- 简化一下问题，因为(0,0)位置是一个角落，那么走的方向只有两种
  - 1：往下走一格 即:(x+1,y)
  - 2：往右走一格 即:(x,y+1)
  
### 剪枝
- 走过的格子记忆
1：判断此格子走没走过，如果走过则剪枝return
2：如果没有走过，将此位置记录，继续dfs，往下或往右，直至不符合条件

### 步骤
1. 检测是否访问过、是否到达边界、是否满足数位和小于k值
2. 剪枝测试
3. 修改返回值
4. 进入递归（向下向右走）
```java
        // 记忆数组(剪枝)
    boolean[][] memory;
    int res = 0;

    public int movingCount(int m, int n, int k) {
        //
        if (k == 0 || m == 1 && n == 1) return 1;
        // 初始化默认为false
        memory = new boolean[m][n];
        // 从(0,0)位置开始遍历
        dfs(0, 0, k, m, n);
        return res;
    }

    /**
     *
     * @param x 当前行
     * @param y 当前列
     * @param k k值
     * @param m 行边界
     * @param n 列边界
     */
    private void dfs(int x, int y, int k, int m, int n) {
        // 1. 
        // 如果memory[x][y] == true 说明遍历过了
        // 到边界 也return
        if (x == m || y == n || memory[x][y]) return;

        // 判断是否满足另外一个条件: 数位和 大于 k return
        if (panduan(x) + panduan(y) > k) return;

        // 2. 
        // 走到这里说明此格没有遍历过 将memory置为true
        memory[x][y] = true;

        // 3. 
        // 返回值+1
        res++;

        // 4. 
        // 往下走一格
        dfs(x + 1, y, k, m, n);

        // 往右走一格
        dfs(x, y + 1, k, m, n);
    }

    // 返回 传参x 的各个位相加的和
    int panduan(int x) {
//        if (x == 100) return 1;
//        if (x <= 9) return x;
//        return x / 10 + x % 10;
        int s = 0;
        while (x != 0) {
            s += x % 10;
            x = x / 10;
        }
        return s;
    }
```
  
</details>
  
  
<details>
<summary>&#127808; BFS &#127808;</summary>

### 思想 
- 一般来说，能采用DFS解决的问题，也能采用BFS解决，只是搜索策略不同
  - `DFS:` 是沿着某一个方向先走到低，直到不满足条件了才回头，借助栈实现，递归就是利用的系统栈
  - `BFS:` 是先把当前离格子最近的新格子先访问，借助队列实现

### 核心思路：模拟DFS
- 每次访问队列的第一个元素
- 判断该元素是否符合要求
- 将该元素**能访问到**的存入队列
  
### 步骤
1. 创建一个队列，保存的是访问到的格子坐标，是个二维数组
2. 开始循环访问（每次访问队列的第一个元素，将该元素**能访问到**的存入队列）
3. 更新返回值
  
```java
  
    // visited记录格子是否被访问过
    boolean[][] visited;
    int res = 0;

    public int movingCount(int m, int n, int k) {
        // 1.
        // 创建一个队列，保存的是访问到的格子坐标，是个二维数组
        Queue<int[]> queue = new LinkedList<>();
        // 把起始结点存入队列
        queue.add(new int[]{0, 0});
        // 开始循环访问
        while (queue.size() > 0) {
            // 将队列的第一个结点出队，访问
            int[] temp = queue.poll();
            // 获取此次访问的行列坐标，准备测试格子是否合格
            int x = temp[0], y = temp[1];
            // 跳过不合格的坐标格子
            if (x >= m || y >= n || get(x) + get(y) > k || visited[x][y]) {
                continue;
            }
            // 将合格的格子标记为已经访问过
            visited[x][y] = true;
            // 满足条件的格子数加一
            res++;
            // 向右边移动
            queue.add(new int[]{x + 1, y});
            // 向下移动
            queue.add(new int[]{x, y + 1});
        }
        return res;
    }

    // 计算一个数的各个位数之和
    private int get(int x) {
        int res = 0;
        while (x != 0) {
            res += x % 10;
            x /= 10;
        }
        return res;
    }
```

</details>

[参考](BonFire提供写法 "链接：https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/solution/jian-zhi-offerer-shua-javadfs-bfs-tu-jie-py05/")