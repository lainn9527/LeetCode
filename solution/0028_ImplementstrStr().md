# 0028_ImplementstrStr()
## 想法
### 暴力法
照順序比對下去，開始比對後遇到錯誤要退回去當初比對的下一個，不然會錯過，例如 aaabbba bba
這樣一直退回去其實很花時間，更好的是用 KMP

### KMP

## 作法
### brute
```C++
class Solution {
public:
    int strStr(string haystack, string needle) {
        if (needle.empty()) return 0;
        int p = 0;
        for (int i = 0; i < haystack.length(); ++i) {
            if (haystack[i] == needle[p]) {
                if (++p == needle.length())
                    return i - p + 1;
            }
            else {
                i = i - p;
                p = 0;
            }
        }
        return -1;
    }
};

```
```C++
class Solution {
public:
    int strStr(string haystack, string needle) {
        if (needle.size() == 0)
            return 0;
        
        vector<int> failure = ff(needle);
        for (int i = 0, p = 0; i < haystack.size(); ++i) {
            if (haystack[i] == needle[p]) {
                ++p;
                if (p == needle.size())
                    return i-p+1;
            }
            else {
                if (p) {
                    p = failure[p-1];
                    --i;
                }
            }
            
        }
        return -1;
        
    }
private:
    vector<int> ff(string needle) {
        
        vector<int> failure(needle.size(), 0);
        
        for (int i = 1, p = 0; i < needle.size(); ++i) {
            if (needle[i] == needle[p]) {
                failure[i] = ++p;
            }
            else if (p) {
                p = failure[p-1];
                --i;
            }
        }
        return failure;
    }
};
```