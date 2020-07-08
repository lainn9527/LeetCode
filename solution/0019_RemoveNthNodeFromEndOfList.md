# 0019_RemoveNthNodeFromEndOfList
## 想法
原本思路是 loop 兩次，一次尋找 linked list 長度，第二次找到倒數第 n 個

看了其他人的作法發現，可以只 loop 一次就找到倒數第 n 個：

方法是用 2 個 pointer p1, p2, 首先讓 p2 往前走 n 次，接著 p1 和 p2一起往前走，這時兩個會相距離 n，當走到底時 p2 指向最後一個，p1 因為距離 n 就會剛好在倒數第 n 個，太神奇了

要注意的是為了移除倒數第 n 個，我們必須指向 n - 1 個，也就是 t1 一開始不能指向 1th node，而是指向 "指著 1th node 的 pointer"，也就是要用 pointer of pointer
## 作法
```C++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode **t1 = &head, *t2 = head;
        for (int i = 0; i < n; ++i)
            t2 = t2->next;
        while (t2) {
            t2 = t2->next;
            t1 = &((*t1)->next);
        }
        *t1 = (*t1)->next;
        return head;
    }
};
```
## 學習
### 複習 pointer
`ListNode **t1 = &head` 代表 t1 指向 `head` 的記憶體位置
`t1 = &((*t1)->next);` 代表 t1 指向下一個 node 中 next 的記憶體位置，因為 next 為 `ListNode *`，因此用 `*t1` 就能獲得 next 指向的 `ListNode`
