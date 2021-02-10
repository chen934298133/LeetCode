## &#127800; 567. 字符串的排列 &#127800;

### &#127826; 题目

##### 给定两个字符串 s1 和 s2，写一个函数来判断 s2 是否包含 s1 的排列。
##### 换句话说，第一个字符串的排列之一是第二个字符串的子串。


**示例 1：**<br>

输入：s1 = "ab" s2 = "eidbaooo" <br>
输出：true <br>
解释: s2 包含 s1 的排列之一 ("ba").


**示例 2：**

输入：s1= "ab" s2 = "eidboaoo"<br>
输出：false

**注意：**<br>

1. 输入的字符串只包含小写字母
2. 两个字符串的长度都在 [1, 10,000] 之间


### &#127826; 题解


<details>
<summary>&#127808; 滑动窗口 &#127808;</summary>

![](https://pic.leetcode-cn.com/1612923521-rTbkNV-567.gif)
![](https://pic.leetcode-cn.com/1612923583-vvPUNM-567.001.jpeg)
![](https://pic.leetcode-cn.com/1612923583-pJtnRs-567.002.jpeg)
![](https://pic.leetcode-cn.com/1612923583-wSHZbg-567.003.jpeg)
![](https://pic.leetcode-cn.com/1612923583-uYfKRp-567.004.jpeg)
![](https://pic.leetcode-cn.com/1612923583-FqBUZF-567.005.jpeg)
![](https://pic.leetcode-cn.com/1612923583-IMoJec-567.006.jpeg)
![](https://pic.leetcode-cn.com/1612923583-APuRVZ-567.007.jpeg)
  
```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int n = s1.length(), m = s2.length();
        if (n > m) {
            return false;
        }
        int[] cnt1 = new int[26];
        int[] cnt2 = new int[26];
        for (int i = 0; i < n; ++i) {
            ++cnt1[s1.charAt(i) - 'a'];
            ++cnt2[s2.charAt(i) - 'a'];
        }
        if (Arrays.equals(cnt1, cnt2)) {
            return true;
        }
        for (int i = n; i < m; ++i) {
            ++cnt2[s2.charAt(i) - 'a'];
            --cnt2[s2.charAt(i - n) - 'a'];
            if (Arrays.equals(cnt1, cnt2)) {
                return true;
            }
        }
        return false;
    }
}
```
</details>
  
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




<details>
<summary>&#127808; 双指针 &#127808;</summary>

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
        }
        int left = 0;
        for (int right = 0; right < m; ++right) {
            int x = s2.charAt(right) - 'a';
            ++cnt[x];
            while (cnt[x] > 0) {
                --cnt[s2.charAt(left) - 'a'];
                ++left;
            }
            if (right - left + 1 == n) {
                return true;
            }
        }
        return false;
    }
}

```
  
##### 复杂度分析

- 时间复杂度：O(n+m+∣Σ∣)O(n+m+|\Sigma|)O(n+m+∣Σ∣)。
    创建 cnt\textit{cnt}cnt 需要 O(∣Σ∣)O(|\Sigma|)O(∣Σ∣) 的时间。
    遍历 s1s_1s1​ 需要 O(n)O(n)O(n) 的时间。
    双指针遍历 s2s_2s2​ 时，由于 left\textit{left}left 和 right\textit{right}right 都只会向右移动，故这一部分需要 O(m)O(m)O(m) 的时间。

- 空间复杂度：O(∣Σ∣)O(|\Sigma|)O(∣Σ∣)。
</details>


