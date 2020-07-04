# 0009_PalindromeNumber
## 想法
藉著之前的 0007_ReverseInteger 作法，先將 integer 倒反過來再比大小，但速度比我想像中的慢，應該還有更快的方法

## 作法
```C++
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0)
            return false;
        unsigned rx = 0, t = x;
        while (t) {
            rx = rx * 10 + t % 10;
            t /= 10;
        }
        return rx==x;
    }
};
```