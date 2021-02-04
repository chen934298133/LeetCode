## &#127800; 剑指 Offer 06. 从尾到头打印链表 &#127800;

### &#127826; 题目

**用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )**

示例 1：

输入：<br>
`["CQueue","appendTail","deleteHead","deleteHead"]`<br>
`[[],[3],[],[]]`<br>
输出：`[null,null,3,-1]`<br>

示例 2：

输入：<br>
`["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]`<br>
`[[],[],[5],[2],[],[]]`<br>
输出：`[null,-1,null,null,5,2]`<br>

提示：<br>
`1 <= values <= 10000`
`最多会对 appendTail、deleteHead 进行 10000 次调用`



### &#127826; 题解


<details>
<summary>&#127808; View The Codes &#127808;</summary>

```java
package LeetCode_2021.Coding_2021_02_04;

import java.util.LinkedList;

public class Offer09 {

    /**
     * A 栈只负责添加
     * B栈负责将A栈的元素弹出后存储下来，然后弹出达到换序的效果
     */
    LinkedList<Integer> A, B;

        public  Offer09() {
            A = new LinkedList<Integer>();
            B = new LinkedList<Integer>();
        }

        public void appendTail(int value) {
            A.addLast(value);
        }

        public int deleteHead() {

            // 三种情况

            // 在B栈有元素时，无序从A栈调取，直接弹栈
            if(!B.isEmpty()) return B.removeLast();

            // 在B栈为空，且A栈为空时直接退出
            if(A.isEmpty()) return -1;

            // 在B栈为空，A栈不为空时，先从A栈调取元素
            while(!A.isEmpty())
                B.addLast(A.removeLast());

            // 然后弹栈
            return B.removeLast();
        }

        public static void main(String[] args){
            Offer09 o1 = new Offer09();
            o1.appendTail(1);
            o1.appendTail(2);
            o1.appendTail(3);
            System.out.println(o1.deleteHead());
        }
}

```
</details>
