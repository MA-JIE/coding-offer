给你一个链表数组，每个链表都已经按升序排列。 <b>

请你将所有链表合并到一个升序链表中，返回合并后的链表。<b>

示例 1：

输入：lists = [[1,4,5],[1,3,4],[2,6]]
输出：[1,1,2,3,4,4,5,6]
解释：链表数组如下：
[
  1->4->5,
  1->3->4,
  2->6
]
将它们合并到一个有序链表中得到。
1->1->2->3->4->4->5->6
示例 2：

输入：lists = []
输出：[]
示例 3：

输入：lists = [[]]
输出：[]

``` cpp
class Solution {
public:
    struct compare {
        bool operator()(ListNode* l1, ListNode* l2) {
            return l1->val > l2->val;
        }
    };
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<ListNode*, vector<ListNode*>, compare> pq;
        for(auto list : lists) {
            if(list) {
                pq.push(list);
            }
        }
        ListNode *dummy = new ListNode(0);
        ListNode *cur = dummy;
        while(!pq.empty()) {
            cur->next = pq.top();
            pq.pop();
            cur = cur->next;
            if(cur->next) {
                pq.push(cur->next);
            }
        }
        return dummy->next;
    }
};
```
