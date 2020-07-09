# 0021_MergeTwoSortedLists
## 想法
一開始一直卡在 node 要合併時需要很複雜的程序，還有不知道怎麼 new 出 dummy node，所以只想得到用大小 2 個 pointer 維持的作法，還花了不少時間 (1h)

直到看了別人的作法才恍然大悟，原來是這樣啊，就是這麼的樸實無華
## 作法
### 原本的笨笨的作法
```C++
class Solution {
public:
    ListNode* next_large(ListNode *l, int v) {
        while (l->next && l->next->val < v)
            l = l->next;
        return l;
    }
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (l1 == NULL)
            return l2;
        else if (l2 == NULL)
            return l1;
        
        ListNode *b = l1, *s = l2, *h = l2;
        if (l1->val < l2->val) {
            b = l2, s = l1, h = l1;
        }
        
        ListNode *t1, *t2, *t3;
        while (b && s) {
            while (s->next && s->next->val < b->val)
                s = s->next;
            if (!s->next) {
                s->next = b;
                break;
            }
            
            t1 = b;
            while (b->next && b->next->val <= s->next->val)
                b = b->next;
            t2 = s->next;
            t3 = b->next;
            s->next = t1;
            b->next = t2;
            b = t3;
            s = t2;
        }
        return h;
    }
};
```
### 被智商壓制
```C++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode h(INT_MIN), *p = &h;
        while (l1 && l2) {
            if (l1->val < l2->val) {
                p->next = l1;
                l1 = l1->next;
            }
            else {
                p->next = l2;
                l2 = l2->next;
            }
            p = p->next;
        }
        p->next = l1 ? l1 : l2;
        return h.next;

    }
};
```
## 學習
### dummy node
`ListNode dummy(0), *pointer = &dummy`
