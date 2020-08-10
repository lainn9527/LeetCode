# 0024_SwapNodesInPairs
## 想法
創建一個 dummy node，維持兩個 pointer，一個 next 指向 n1，另一個 next 指向 n2，如此往下切換

這應該是最佳解了
## 作法
```C++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if (!head || !head->next)
            return head;
        ListNode *h = new ListNode(1), *r = head->next;

        while(head && head->next) {
            h->next = head->next;
            head->next = head->next->next;
            h->next->next = head;
            h = head;
            head = head->next;

        }
        return r;
    }
};
```
