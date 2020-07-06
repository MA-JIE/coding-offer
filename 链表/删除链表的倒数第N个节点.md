# 删除链表的倒数第N个节点
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。<br>
示例：<br>
给定一个链表: 1->2->3->4->5, 和 n = 2. <br>
当删除了倒数第二个节点后，链表变为 1->2->3->5. <br>
说明：<br>
给定的 n 保证是有效的。<br>
进阶：<br>
你能尝试使用一趟扫描实现吗？ <br>
思路:双指针,一快一慢
```cpp
class Solution
{
public:
    ListNode *removeNthFromEnd(ListNode *head, int n)
    {
        if (!head)
        {
            return nullptr;
        }
        ListNode *dummy = new ListNode();
        ListNode *slow = dummy;
        dummy->next = head;
        ListNode *fast = head;
        while (n--)
        {
            fast = fast->next;
        }
        while (fast)
        {
            slow = slow->next;
            fast = fast->next;
        }
        slow->next = slow->next->next;
        ListNode *res = dummy->next;
        delete dummy;
        return res;
    }
};
```
