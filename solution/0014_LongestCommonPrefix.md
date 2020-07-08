# 0014_LongestCommonPrefix
## 想法
最簡單的就是一一比對了

## 作法
Runtime: 8 ms (69.92%)
Memory Usage: 9.4 MB (30.59%)
```C++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if (strs.empty())
            return "";
        int min_length = INT_MAX;
        for (auto s: strs)
            min_length = min(min_length, int(s.length()));
        
        string mp = "";
        for (int i = 0; i < min_length; ++i) {
            char c = strs[0][i];
            int j = 0;
            while (++j < strs.size() && c == strs[j][i])
                ;
            
            if (j == strs.size())
                mp += strs[0].substr(i, 1);
            else
                break;
        }
        return mp;
    }
};
```
### 參考最佳解
時間差不多啊
```C++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        string mp = "";
        for (int i = 0; strs.size() > 0; ++i) {
            for (int j = 0; j < strs.size(); ++j) {
                if ( i >= strs[j].length() || strs[j][i] != strs[0][i])
                    return mp;
            }
            mp += strs[0][i];
        }
        return mp;
    }
};
```