## &#127800; 554. Brick Wall &#127800;

### &#127826; 题目

There is a rectangular brick wall in front of you with `n` rows of bricks. The i<sup>th</sup> row has some number of bricks each of the same height (i.e., one unit) but they can be of different widths. The total width of each row is the same.

Draw **a vertical line from the top to the bottom** and cross **the least** bricks. If your line goes through the edge of a brick, then the brick is not considered as crossed. **You cannot draw a line just along one of the two vertical edges of the wall, in which case the line will obviously cross no bricks.**

Given the 2D array wall that contains the information about the wall, return ***the minimum number of crossed bricks after drawing such a vertical line.***

<br>
<details>
<summary> &#127809; 尽量不看翻译 &#127809; </summary>
  
你的面前有一堵矩形的、由 `n` 行砖块组成的砖墙。这些砖块高度相同（也就是一个单位高）但是宽度不同。每一行砖块的宽度之和应该相等。

你现在要画一条 **自顶向下** 的、穿过 **最少** 砖块的垂线。如果你画的线只是从砖块的边缘经过，就不算穿过这块砖。你**不能沿着墙的两个垂直边缘之一画线，这样显然是没有穿过一块砖的。**

给你一个二维数组 wall ，该数组包含这堵墙的相关信息。其中，`wall[i]` 是一个代表从左至右每块砖的宽度的数组。你需要找出怎样画才能使这条线 **穿过的砖块数量最少** ，并且返回 **穿过的砖块数量** 。
  
</details>
<br>

**Example 1:**

![](http://lc-dDwI9S44.cn-n1.lcfile.com/a5oecYp3wPrqpyuRh0bgK1DfafF2fBzW/wall.png)
Input: wall = `[[1,2,2,1],[3,1,2],[1,3,2],[2,4],[3,1,2],[1,3,1,1]]`<br>
Output: 2<br>

**Example 2:**<br>
Input: wall = `[[1],[1],[1]]`<br>
Output: 3<br>

Constraints:

- `n == wall.length`
- `1 <= n <= 104`
- `1 <= wall[i].length <= 104`
- `1 <= sum(wall[i].length) <= 2 * 104`
- `sum(wall[i]) is the same for each row i.`
- `1 <= wall[i][j] <= 231 - 1`

### &#127826; 题解


<details>
<summary>&#127808; 哈希表——AC_OIer提供写法 &#127808;</summary>

- 题目要求穿过的砖块数量最少，等效于通过的间隙最多。

- 则可以使用「哈希表」记录每个间隙的出现次数，最终统计所有行中哪些间隙出现得最多，使用「总行数」减去「间隙出现的最多次数」即是答案。
- 直接使用行前缀记录间隙。

![](http://lc-dDwI9S44.cn-n1.lcfile.com/a5oecYp3wPrqpyuRh0bgK1DfafF2fBzW/wall.png)
  
第 1 行的间隙有 [1,3,5]
第 2 行的间隙有 [3,4]
第 3 行的间隙有 [1,4]
第 4 行的间隙有 [2]
第 5 行的间隙有 [3,4]
第 6 行的间隙有 [1,4,5]

对间隙计数完成后，遍历「哈希表」找出出现次数最多间隙 4，根据同一个间隙编号只会在单行内被统计一次，用总行数减去出现次数，即得到「最少穿过的砖块数」。
  
```java
class Solution {
    public int leastBricks(List<List<Integer>> wall) {
        int n = wall.size();
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0, sum = 0; i < n; i++, sum = 0) {
            for (int cur : wall.get(i)) {
                sum += cur;
                map.put(sum, map.getOrDefault(sum, 0) + 1);
            }
            map.remove(sum); // 不能从两边穿过，需要 remove 掉最后一个
        }
        int ans = n;
        for (int u : map.keySet()) {
            int cnt = map.get(u);
            ans = Math.min(ans, n - cnt);
        }
        return ans;
    }
}

```
  
### 复杂度分析
- 时间复杂度：记所有砖块数量为 n，所有砖块都会被扫描。复杂度为 O(n)
- 空间复杂度：O(n)
  
</details>
  
  
<details>
<summary>&#127808; 自己瞎写的+测试用例 &#127808;</summary>

```java
package LeetCode_2021.Coding_2021_05_01;

import java.util.*;

public class LeetCode_554 {
    
    public int leastBricks(List<List<Integer>> wall) {
        int result = wall.size();
        int edges = wall.size();
        Map<Integer, Integer> map = new HashMap();
        List<List<Integer>> listAll = new ArrayList<>();
        for (int i = 0; i < wall.size(); i++) {
            List<Integer> tempList = new ArrayList<>();
            int num = 0;
            for (Integer integer : wall.get(i)) {
                num += integer;
                tempList.add(num);
//                edges = Math.max(edges, num);
            }
            tempList.remove(tempList.size() - 1);
            listAll.add(tempList);
        }
        for (List<Integer> integers : listAll) {
            for (Integer integer : integers) {
                int i = map.getOrDefault(integer, 0) + 1;
                map.put(integer, i);
                result = Math.min(result, edges - i);
            }
        }
        return result;
    }

    public static void main(String[] args) {
        List<List<Integer>> list = new ArrayList();
        List<Integer> list1 = new ArrayList<>();
        list1.add(1);
        list1.add(2);
        list1.add(2);
        list1.add(1);
        List<Integer> list2 = new ArrayList<>();
        list2.add(3);
        list2.add(1);
        list2.add(2);
        List<Integer> list3 = new ArrayList<>();
        list3.add(1);
        list3.add(3);
        list3.add(2);
        List<Integer> list4 = new ArrayList<>();
        list4.add(2);
        list4.add(4);
        List<Integer> list5 = new ArrayList<>();
        list5.add(3);
        list5.add(1);
        list5.add(2);
        List<Integer> list6 = new ArrayList<>();
        list6.add(1);
        list6.add(3);
        list6.add(1);
        list6.add(1);
        list.add(list1);
        list.add(list2);
        list.add(list3);
        list.add(list4);
        list.add(list5);
        list.add(list6);
        System.out.println(list.toString());

        List<List<Integer>> lists = new ArrayList<>();
        List<Integer> list7 = new ArrayList<>();
        list7.add(1);
        list7.add(1);
        List<Integer> list8 = new ArrayList<>();
        list8.add(2);
        List<Integer> list9 = new ArrayList<>();
        list9.add(1);
        list9.add(1);
        lists.add(list7);
        lists.add(list8);
        lists.add(list9);
        LeetCode_554 l = new LeetCode_554();
        System.out.println(l.leastBricks(lists));
    }
}

```

</details>

[方法一参考](AC_OIer提供写法 "链接：https://leetcode-cn.com/problems/brick-wall/solution/gong-shui-san-xie-zheng-nan-ze-fan-shi-y-gsri/")