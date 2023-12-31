# 力扣24. 两两交换链表中的结点

交换的过程需要梳理一下，但弄清楚了还是很简单，就是需要两个暂存结点。

```c#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode SwapPairs(ListNode head) {
        ListNode dummyHead = new ListNode();
        dummyHead.next = head;
        ListNode current = new ListNode();
        current = dummyHead;
        while (current.next != null && current.next.next != null) {
            ListNode temp0 = current.next; //1
            ListNode temp1 = current.next.next.next; //3

            current.next = current.next.next;
            current.next.next = temp0;
            current.next.next.next =temp1;

            current = current.next.next;
        }
        return dummyHead.next;
    }
}
```

# 力扣19. 删除链表的倒数第 N 个结点

删除某个结点，则需要获取其前一个结点进行操作。

```c#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode RemoveNthFromEnd(ListNode head, int n) {
        ListNode dummyHead = new ListNode();
        dummyHead.next = head;
        ListNode fastPoint = dummyHead;
        ListNode slowPoint = dummyHead;

        for (int i = 0; i < n + 1; i++) {
            fastPoint = fastPoint.next;
        }

        while (fastPoint != null) {
            fastPoint = fastPoint.next;
            slowPoint = slowPoint.next;
        }
        
        slowPoint.next = slowPoint.next.next;
        return dummyHead.next;
    }
}
```

# 面试题 02.07. 链表相交

这题还是有些不理解，需要我之后再琢磨一下

```c#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode GetIntersectionNode(ListNode headA, ListNode headB) {
    if (headA == null || headB == null) return null;
    ListNode cur1 = headA, cur2 = headB;
    while (cur1 != cur2)
        {
            cur1 = cur1 == null ? headB : cur1.next;
            cur2 = cur2 == null ? headA : cur2.next;
        }
    return cur1;
    }
}
```

# 力扣142. 环形链表 II

理解了如何得知存在环，但对如何判断入口还不是很懂，之后再看看。

```c#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode DetectCycle(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if (slow == fast) {
                ListNode index0 = head;
                ListNode index1 = fast;

                while (index0 != index1) {
                    index0 = index0.next;
                    index1 = index1.next;
                }

                return index0;
            }
        }

        return null;
    }
}
```

# 总结

链表的特点是通过结点进行连接，每个结点保存下一个结点的地址，从而形成链条。

对链表进行修改和删除的要点在于，要获取所需要修改或删除的结点**前一个**结点的位置，再进行操作。