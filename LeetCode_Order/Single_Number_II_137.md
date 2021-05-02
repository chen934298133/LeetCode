## &#127800; 137. Single Number II &#127800;

### &#127826; 题目

Given an integer array `nums` where every element appears `three times` except for one, which appears `exactly once`. <br>
Find the single element and return it.
<br>
<details>
<summary> &#127809; 尽量不看翻译 &#127809; </summary>
  
给你一个整数数组 nums ，除某个元素仅出现 一次 外，其余每个元素都恰出现 三次 。
  
请你找出并返回那个只出现了一次的元素。

</details>
<br>
Example 1:

Input: nums = `[2,2,3,2]`<br>
Output: `3`

Example 2:

Input: nums = `[0,1,0,1,0,1,99]`<br>
Output: `99`<br>

Note:
- `1 <= nums.length <= 3 * 104`
- `-231 <= nums[i] <= 231 - 1`
- Each element in nums appears exactly **three times** except for one element which appears **once**.

### &#127826; 题解


<details>
<summary>&#127808; 哈希表 &#127808;</summary>

- 我们可以使用哈希映射统计数组中每个元素的出现次数。对于哈希映射中的每个键值对，键表示一个元素，值表示其出现的次数。

- 在统计完成后，我们遍历哈希映射即可找出只出现一次的元素。

```java
class Solution {
    public int singleNumber(int[] nums) {
        Map<Integer, Integer> freq = new HashMap<Integer, Integer>();
        for (int num : nums) {
            freq.put(num, freq.getOrDefault(num, 0) + 1);
        }
        int ans = 0;
        for (Map.Entry<Integer, Integer> entry : freq.entrySet()) {
            int num = entry.getKey(), occ = entry.getValue();
            if (occ == 1) {
                ans = num;
                break;
            }
        }
        return ans;
    }
}
```
  
### 复杂度分析
- 时间复杂度：O(n)，其中 n 是数组的长度。

- 空间复杂度：O(n)。哈希映射中包含最多 `⌊n/3⌋+1` 个元素，即需要的空间为 `O(n)`。
</details>
  
  
<details>
<summary>&#127808; 依次确定每一个二进制位 &#127808;</summary>

### 思路与算法
为了方便叙述，我们称「只出现了一次的元素」为「答案」。

由于数组中的元素都在 int（即 32 位整数）范围内，因此我们可以依次计算答案的每一个二进制位是 0 还是 1。

具体地，考虑答案的第 i 个二进制位（i 从 0 开始编号），它可能为 0 或 1。对于数组中非答案的元素，每一个元素都出现了 3 次，对应着第 i 个二进制位的 3 个 0 或 3 个 1，无论是哪一种情况，它们的和都是 3 的倍数（即和为 0 或 3）。因此：
> 答案的第 i 个二进制位就是数组中所有元素的第 i 个二进制位之和除以 3 的余数。

这样一来，对于数组中的每一个元素 x，我们使用位运算 (x >> i) & 1 得到 x 的第 i 个二进制位，并将它们相加再对 3 取余，得到的结果一定为 0 或 1，即为答案的第 i 个二进制位。

### 细节

需要注意的是，如果使用的语言对「有符号整数类型」和「无符号整数类型」没有区分，那么可能会得到错误的答案。这是因为「有符号整数类型」（即 int 类型）的第 31 个二进制位（即最高位）是补码意义下的符号位，对应着 31
 ，而「无符号整数类型」由于没有符号，第 31 个二进制位对应着 ${2^3}$
 。因此在某些语言（例如 Python）中需要对最高位进行特殊判断。

```java
class Solution {
    public int singleNumber(int[] nums) {
        int ans = 0;
        for (int i = 0; i < 32; ++i) {
            int total = 0;
            for (int num: nums) {
                total += ((num >> i) & 1);
            }
            if (total % 3 != 0) {
                ans |= (1 << i);
            }
        }
        return ans;
    }
}
```
  
### 复杂度分析
- 时间复杂度：O(nlogC)，其中 n 是数组的长度，C 是元素的数据范围，在本题中 ${logC=log2^32=32}$，也就是我们需要遍历第 0∼31 个二进制位。

- 空间复杂度：O(1)。
</details>

<details>
<summary>&#127808; 方法三、四数字电路设计与优化 &#127808;</summary>

[数字电路设计与优化](https://leetcode-cn.com/problems/single-number-ii/solution/zhi-chu-xian-yi-ci-de-shu-zi-ii-by-leetc-23t6/)
</details>

  <details>
<summary>&#127808; 自己瞎写的哈希表 &#127808;</summary>

```java
    class Solution {
   public int singleNumber(int[] nums) {
         int value = 1;
        Map<Integer, Integer> map = new HashMap();
        for (int num : nums) {
            if (map.containsKey(num)) {
                map.put(num, 3);
                continue;
            } else {
                map.put(num, 1);
            }
        }
        int result = -1;
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            if (value == entry.getValue()) {
                result = entry.getKey();
            }
        }
        return result;
    }
}
```
</details>


