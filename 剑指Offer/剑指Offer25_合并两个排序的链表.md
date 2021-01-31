## &#127800; 剑指 Offer 25. 合并两个排序的链表 &#127800;

### &#127826; 题目

**输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。**

示例1：

输入：1->2->4, 1->3->4

输出：1->1->2->3->4->4

### &#127826; 题解

方法一： 简单思路
<details>
<summary>&#127808; View The Codes &#127808;</summary>

1. 初始化： 伪头节点 dumdumdum ，节点 curcurcur 指向 dumdumdum 。
2. 循环合并： 当 l1l_1l1​ 或 l2l_2l2​ 为空时跳出；
 - 当 l1.val<l2.vall_1.val < l_2.vall1​.val<l2​.val 时： curcurcur 的后继节点指定为 l1l_1l1​ ，并 l1l_1l1​ 向前走一步；
 - 当 l1.val≥l2.vall_1.val \geq l_2.vall1​.val≥l2​.val 时： curcurcur 的后继节点指定为 l2l_2l2​ ，并 l2l_2l2​ 向前走一步 ；
 - 节点 curcurcur 向前走一步，即 cur=cur.nextcur = cur.nextcur=cur.next 。

3. 合并剩余尾部： 跳出时有两种情况，即 l1l_1l1​ 为空 或 l2l_2l2​ 为空。

 - 若 l1≠nulll_1 \ne nulll1​​=null ： 将 l1l_1l1​ 添加至节点 curcurcur 之后；
 - 否则： 将 l2l_2l2​ 添加至节点 curcurcur 之后。

4. 返回值： 合并链表在伪头节点 dumdumdum 之后，因此返回 dum.nextdum.nextdum.next 即可。


```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dum = new ListNode(0);
        ListNode cur = dum;

        while(l1 != null && l2 != null){
            if(l1.val < l2.val){
                cur.next = l1;
                l1 = l1.next;
            }else {
                cur.next = l2;
                l2 = l2.next;
            }
            cur = cur.next;
        }
        cur.next = (l1 == null ? l2 : l1);
        return dum.next;
    }
}
```
</details>
  
方法二： 递归

<details>
<summary>&#127808; View The Codes &#127808;</summary>

```java
class Solution {
public ListNode mergeTwoLists_Recursive(ListNode l1, ListNode l2) {
        //递归实现
        return recur(l1, l2);
    }

    public ListNode recur(ListNode l1, ListNode l2) {
        //是否为null判断
        if (l1 == null && l2 == null) return null;
        if (l1 == null) return l2;
        if (l2 == null) return l1;

        //新建头结点
        ListNode head = null;

        //如果l1.val <= l2.val，那么头结点的值为l1.head的值，然后开始递归
        if (l1.val <= l2.val) {
            head = new ListNode(l1.val);
            head.next = recur(l1.next, l2);
        }
        //否则，头结点的值为l2.head的值，然后开始递归
        else {
            head = new ListNode(l2.val);
            head.next = recur(l1, l2.next);
        }

        //返回该链表
        return head;
    }
}
```
</details>
  