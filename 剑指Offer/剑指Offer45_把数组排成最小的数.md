## &#127800; 剑指 Offer 45. 把数组排成最小的数 &#127800;

### &#127826; 题目

输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。


##### 示例 1:

- 输入: [10,2]
- 输出: "102"

##### 示例 2:
- 输入: [3,30,34,5,9]
- 输出:  "3033459"

##### 限制：

- 0 < nums.length <= 100

### &#127826; 题解
[题解参考](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/solution/mian-shi-ti-45-ba-shu-zu-pai-cheng-zui-xiao-de-s-4/ "Krahets")


<details>
<summary>&#127808; 快排 &#127808;</summary>
  
  
```java
 
class Solution {
      public String minNumber3(int[] nums) {
        // 1. 转为 String 数组
        String[] strs = new String[nums.length];
        for (int i = 0; i < nums.length; i++) {
            strs[i] = String.valueOf(nums[i]);
        }

        // 2. 进入快排
        quickSort(strs, 0, strs.length - 1);

        // 3. 拼接字符
        StringBuilder res = new StringBuilder();
        for (String s : strs) {
            res.append(s);
        }
        return res.toString();
    }

    // 快排
    public void quickSort(String[] strs, int low, int high) {
        if (low < high) {
            int middle = getMiddle(strs, low, high);
            quickSort(strs, low, middle - 1);
            quickSort(strs, middle + 1, high);
        }
    }

    // 找到中位数
    public int getMiddle(String[] strs, int low, int high) {
        //数组的第一个数为基准元素
        String temp = strs[low];
        while (low < high) {
            //从后向前找比基准小的数
            while (low < high && (strs[high] + temp).compareTo(temp + strs[high]) >= 0) {
                high--;
            }
            //把比基准小的数移到低端
            strs[low] = strs[high];

            //从前向后找比基准大的数
            while (low < high && (strs[low] + temp).compareTo(temp + strs[low]) <= 0) {
                low++;
            }
            //把比基准大的数移到高端
            strs[high] = strs[low];
        }
        strs[low] = temp;
        return low;
    }
```
  
</details>

  