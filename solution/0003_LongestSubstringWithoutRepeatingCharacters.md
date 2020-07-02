# 0003_LongestSubstringWithoutRepeatingCharacters

## 想法
一開始就想到能夠 O(n) 解，就是用 vector 儲存被挑過的字，之後只要查看 vector 就知道是否有重複。
有想到 vector 裡面儲存順序，但沒有仔細去思考就錯過最佳解了。

總之，我想到的是用 queue 儲存當下處理中的連續字串，遇到重複的就從頭開始 pop 直到重複的那個，但這樣太慢了。
快速做法是，每次 ++i 往下時，都將 i 當作該 char 的編號，在存連續字串頭的編號叫 start，往下時先比較該 char 的編號是否 > start，是的話代表重複了，將當下的 i - start 就是連續字串長度

## 作法
### 使用 queue
```C++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<bool> rep(260, 0);
        queue<int> q;
        int counter = 0;
        int max_num = 0;
        for(auto i:s) {
            int t = int(i);
            if (rep[t]) {
                max_num = max(counter, max_num);
                int top = q.front();
                while(top != t) {
                    rep[top] = 0;
                    q.pop();
                    --counter;
                    top = q.front();
                }
                q.pop();
            }
            else {
                rep[t] = 1;
                ++counter;
            }
            q.push(t);
            
            
        }
        return max(counter, max_num);
    }
};
```
### 最佳解
```C++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> rep(260, -1);
        int start = 0;
        int max_num = 0;
        int i = 0;
        for (; i < s.size(); ++i) {
            if (rep[int(s[i])] >= start) {
                max_num = max(max_num, i - start);
                start = rep[int(s[i])] + 1;
            }
            rep[int(s[i])] = i;
                
        }
        return max(max_num, (i - start));
    }
};
```
## 學習
`for(auto i:s)` 也能用在 string 上