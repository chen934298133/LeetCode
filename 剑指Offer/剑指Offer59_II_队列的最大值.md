## &#127800; 剑指 Offer 59 - II. 队列的最大值 &#127800;

### &#127826; 题目

请定义一个队列并实现函数 max_value 得到队列里的最大值，要求函数max_value、push_back 和 pop_front 的均摊时间复杂度都是O(1)。

若队列为空，pop_front 和 max_value 需要返回 -1


##### 示例 1:

- 输入: 
```
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
```
- 输出: `[null,null,null,2,1,2]`

##### 示例 2:
- 输入: 
```
["MaxQueue","pop_front","max_value"]
[[],[],[]]
```
- 输出: `[null,-1,-1]`

##### 限制：

- `1 <= push_back,pop_front,max_value的总操作数 <= 10000`
- ${1 <= value <= 10^5}$

### &#127826; 题解
[题解参考](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/solution/jian-zhi-offer-59-ii-dui-lie-de-zui-da-z-0pap/ "Krahets")

- 最直观的想法是 **维护一个最大值变量** ，在元素入队时更新此变量即可；但当最大值出队后，并无法确定下一个 次最大值 ，因此不可行。
- 其次是维护一个双端链表，依次存入比当前最值，重点在于时刻保持此列表递减
  - 为了实现此递减列表，需要使用 双向队列 ，假设队列已经有若干元素：
  - 当执行入队 `push_back()` 时： 若入队一个比队列某些元素更大的数字 xx ，则为了保持此列表递减，需要将双向队列 **尾部所有小于 xx 的元素** 弹出。
  - 当执行出队 `pop_front()` 时： 若出队的元素是最大元素，则 双向队列 需要同时 **将首元素出队** ，以**保持**队列和双向队列的元素一致性。

<details>
<summary>&#127808; 利用双向链表 &#127808;</summary>
  
<![1](https://pic.leetcode-cn.com/1609261619-jyPPLT-Picture3.png),![2](https://pic.leetcode-cn.com/1609261619-bCHZki-Picture4.png),![3](https://pic.leetcode-cn.com/1609261619-VJHbWU-Picture5.png),![4](https://pic.leetcode-cn.com/1609261757-CwSwSi-Picture6.png),![5](https://pic.leetcode-cn.com/1609261619-TeDGxf-Picture7.png),![6](https://pic.leetcode-cn.com/1609261619-xvlryq-Picture8.png),![7](https://pic.leetcode-cn.com/1609261619-ARzNSA-Picture9.png),![8](https://pic.leetcode-cn.com/1609261619-UZBWSp-Picture10.png),![9](https://pic.leetcode-cn.com/1609261619-CiZXVu-Picture11.png)>
  
```java
 
class MaxQueue {
    Queue<Integer> q;//q作为辅助队列，按正常顺序放入元素
    Deque<Integer> d;//d作为双端队列，始终维持一个递减的队列，这样队列头就是最大值

    public MaxQueue() {
        q = new LinkedList<Integer>();
        d = new LinkedList<Integer>();
    }

    public int max_value() {
        if (q.isEmpty() || d.isEmpty()) {
            return -1;
        }
        return d.getFirst();
    }

    public void push_back(int value) {
        while (!d.isEmpty() && value > d.getLast()) {
            d.pollLast();
        }
        q.offer(value);
//        d.push(value);
        d.offerLast(value);
//        d.add(value);
    }

    public int pop_front() {
        if (q.isEmpty()){
            return -1;
        }
        if (max_value() == q.peek()){
            d.pollFirst();
        }
        return q.poll();
    }
}

```
  
</details>

  