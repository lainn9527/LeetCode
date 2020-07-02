# 0005_LongestPalindromicSubstring
## 想法
[參考](https://tangshusen.me/2018/12/01/Longest-Palindromic-Substring/)
有三種思路

**DP**
若長字串為回文，則其去頭尾後的短字串必為回文，因此建立一個 table[n, n]記錄短字串是否為回文, 其中若 table[i, j] == 1 (i <= j)，代表 s[i:j] 為回文，從長度 1:n 藉由 table 確認短字串為回文後，再確認頭尾是否一樣，如此往前。

**中心擴張**
從 s[0:n] 以每個單字為中心一一檢查頭尾是否一樣，是的話再往下檢查。要注意回文的長度有基數和偶數，因此要 for loop 要跑兩次

**馬拉車**
待補

## 作法
### DP
Runtime: 616 ms (12.7%)
Memory Usage: 42.6 MB (28.54%)
```C++
class Solution {
public:
    string longestPalindrome(string s) {
        int size = s.size();
                
        vector<vector<bool>> v(1005, vector<bool>(1005, 0));
        
        v[0][0] = 1;
        for (int i = 1; i < size; ++i) {
            v[i][i] = 1;
            v[i][i-1] = 1;
        }
        
        string maxstr = s.substr(0, 1);
        int maxlen = 1;
        
        for (int i = size - 2; i >= 0; --i ) {
            for (int j = i+1; j < size; ++j) {
                if (v[i+1][j-1] && s[i] == s[j]) {
                    v[i][j] = 1;
                    if (maxlen < j-i+1) {
                        maxlen = j-i+1;
                        maxstr = s.substr(i, j-i+1);
                    }
                }
            }
        }
        return maxstr;                    
    }
};
```
### 中心擴張
Runtime: 52 ms (74.04%)
Memory Usage: 11 MB (53.65%)

```C++
class Solution {
public:
    string longestPalindrome(string s) {
        int maxlen = 1;
        string maxstring = s.substr(0, 1);
        for (int i = 1; i < s.size(); ++i) {
            int prelen = 1;
            int pre = i-1, pos = i+1;
            while (pre > -1 && pos < s.size() && s[pre] == s[pos]) {
                prelen += 2;
                if (prelen > maxlen) {
                    maxlen = prelen;
                    maxstring = s.substr(pre, prelen);
                }                        
                --pre, ++pos;
            }
            prelen = 0, pre = i-1, pos = i;
            while (pre > -1 && pos < s.size() && s[pre] == s[pos]) {
                prelen += 2;
                if (prelen > maxlen) {
                    maxlen = prelen;
                    maxstring = s.substr(pre, prelen);
                }                        
                --pre, ++pos;
            }
        }
        return maxstring;
    }
};
```
