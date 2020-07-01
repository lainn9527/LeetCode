# 0002_AddTwoNumbers
linked list
## 想法
因為之前做過還記憶猶新，對 linked list in C++ 也已經熟悉，因此可以快速的做出最佳解，就是按照 list 順序一個一個加起來並創造 new node，直到 2 list 都為空才停止

## 學習
### create instance of struct in C++
1. 直接宣告實體
`ListNode h(5); h.val = 4;`
2. 用指針 new 出來
`ListNode *h = new ListNode(5); h->val = 4`



## 作法
```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *h = new ListNode(0);
        ListNode *ph = h;
        int a = 0;
        while (l1 != NULL || l2 != NULL) {
            int s = 0;
            if (l1 != NULL) {
                s += l1->val;
                l1 = l1->next;
            }
            if (l2 != NULL) {
                s += l2->val;
                l2 = l2->next;
            }
            if (a == 1) {
                ++s;
                a = 0;
            }
            if (s >= 10) {
                s -= 10;
                a = 1;
            }
            ph->next = new ListNode(s);
            ph = ph->next;
        }
        if (a == 1)
            ph->next = new ListNode(1);
        return h->next;
        
    }
};
```