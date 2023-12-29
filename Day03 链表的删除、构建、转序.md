# 力扣203. 移除链表元素

这一题的要点在于掌握链表的基础特征，知道如何增删元素。这题使用虚拟头节点的方法处理。

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
    public ListNode RemoveElements(ListNode head, int val) {
        ListNode dummyHead = new ListNode();
        dummyHead.next = head;

        if (head == null)
            return head;

        ListNode pre = dummyHead;
        ListNode current = head;

        while (current != null) {
            if (current.val == val) {
                pre.next = current.next;
            }
            else {
                pre = current;
            }

            current = current.next;
        }

        return dummyHead.next;
    }
}
```

 # 力扣707. 设计链表

这题感觉还是没有掌握好，跟着答案写也还是有点糊涂，过几天再回过头来研究下

```c#
class ListNode
{
    public int val;
    public ListNode next;
    public ListNode(int val) { this.val = val; }
}
public class MyLinkedList
{
    ListNode dummyHead;
    int count;

    public MyLinkedList()
    {
        dummyHead = new ListNode(0);
        count = 0;
    }

    public int Get(int index)
    {
        if (index < 0 || count <= index) return -1;
        ListNode current = dummyHead;
        for (int i = 0; i <= index; i++)
        {
            current = current.next;
        }
        return current.val;
    }

    public void AddAtHead(int val)
    {
        AddAtIndex(0, val);
    }

    public void AddAtTail(int val)
    {
        AddAtIndex(count, val);
    }

    public void AddAtIndex(int index, int val)
    {
        if (index > count) return;
        index = Math.Max(0, index);
        count++;
        ListNode tmp1 = dummyHead;
        for (int i = 0; i < index; i++)
        {
            tmp1 = tmp1.next;
        }
        ListNode tmp2 = new ListNode(val);
        tmp2.next = tmp1.next;
        tmp1.next = tmp2;
    }

    public void DeleteAtIndex(int index)
    {

        if (index >= count || index < 0) return;
        var tmp1 = dummyHead;
        for (int i = 0; i < index; i++)
        {
            tmp1 = tmp1.next;
        }
        tmp1.next = tmp1.next.next;
        count--;

    }
}
```



# 力扣206. 反转链表

说实话，一开始确实没想到只靠调换下指针指向就可以反转了。链表还挺有意思的。

```C#
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
    public ListNode ReverseList(ListNode head) {
        ListNode pre = null;
        ListNode current = head;
        ListNode temp = null;

        while (current != null) {
            temp = current.next;
            current.next = pre;
            pre = current;
            current = temp;
        }
        return pre;
    }
}
```

