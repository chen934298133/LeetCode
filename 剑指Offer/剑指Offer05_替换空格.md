## &#127800; 剑指 Offer 05. 替换空格&#127800;

### &#127826; 题目

**请实现一个函数，把字符串 s 中的每个空格替换成"%20"。**

示例：

输入：s = "We are happy."<br>
输出："We%20are%20happy."

限制：
0 <= s 的长度 <= 10000


### &#127826; 题解

方法一：遍历添加
<details>
<summary>&#127808; View The Codes &#127808;</summary>

```java
class Solution {
    public String replaceSpace1(String s) {
        StringBuilder res = new StringBuilder();
        for(Character c : s.toCharArray())
        {
            if(c == ' ') res.append("%20");
            else res.append(c);
        }
        return res.toString();
    }

}
```
</details>

<br>
方法二：使用java库函数replace
<details>
<summary>&#127808; View The Codes &#127808;</summary>

```java
class Solution {
    public String replaceSpace(String s) {
        return s.toString().replace(" ", "%20");
    }
}
```
</details>