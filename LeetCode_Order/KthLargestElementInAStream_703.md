## &#127800; 703. 数据流中的第 K 大元素 &#127800;
## (KthLargestElementInAStream_703)

### &#127826; 题目

##### 设计一个找到数据流中第 k 大元素的类（class）。注意是排序后的第 k 大元素，不是第 k 个不同的元素。
##### 请实现 KthLargest 类：
- **KthLargest(int k, int[] nums) 使用整数 k 和整数流 nums 初始化对象。**
- **int add(int val) 将 val 插入数据流 nums 后，返回当前数据流中第 k 大的元素。**


**示例 1：**<br>

输入：<br>
 `["KthLargest", "add", "add", "add", "add", "add"]`<br>
 `[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]`<br>
输出：<br>
`[null, 4, 5, 5, 8, 8]`

解释：
```java
KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3);   // return 4
kthLargest.add(5);   // return 5
kthLargest.add(10);  // return 5
kthLargest.add(9);   // return 8
kthLargest.add(4);   // return 8
```




**提示：**<br>

- $\ce{1 <= k <= 10^4}$
- $\ce{0 <= nums.length <= 104}$
- ${-10^4 <= nums[i] <= 10^4}$
- $-10^4 <= val <= 10^4$
- 最多调用 add 方法 $10^4$ 次
- 题目数据保证，在查找第 k 大元素时，数组中至少有 k 个元素

### &#127826; 题解


<details>
<summary>&#127808; 滑动窗口优化 &#127808;</summary>

```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int n = s1.length(), m = s2.length();
        if (n > m) {
            return false;
        }
        int[] cnt = new int[26];
        for (int i = 0; i < n; ++i) {
            --cnt[s1.charAt(i) - 'a'];
            ++cnt[s2.charAt(i) - 'a'];
        }
        int diff = 0;
        for (int c : cnt) {
            if (c != 0) {
                ++diff;
            }
        }
        if (diff == 0) {
            return true;
        }
        for (int i = n; i < m; ++i) {
            int x = s2.charAt(i) - 'a', y = s2.charAt(i - n) - 'a';
            if (x == y) {
                continue;
            }
            if (cnt[x] == 0) {
                ++diff;
            }
            ++cnt[x];
            if (cnt[x] == 0) {
                --diff;
            }
            if (cnt[y] == 0) {
                ++diff;
            }
            --cnt[y];
            if (cnt[y] == 0) {
                --diff;
            }
            if (diff == 0) {
                return true;
            }
        }
        return false;
    }
}
```
  
##### 复杂度分析：

- 时间复杂度：O(n+m+∣Σ∣)O(n+m+|\Sigma|)O(n+m+∣Σ∣)，其中 nnn 是字符串 s1s_1s1​ 的长度，mmm 是字符串 s2s_2s2​ 的长度，Σ\SigmaΣ 是字符集，这道题中的字符集是小写字母，∣Σ∣=26|\Sigma|=26∣Σ∣=26。
- 空间复杂度：O(∣Σ∣)O(|\Sigma|)O(∣Σ∣)。
</details>


