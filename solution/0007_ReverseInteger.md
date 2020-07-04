# 0007_ReverseInteger
## 想法
一開始是想說轉成字串後倒過來，結果竟然才 55%，太慢了
看了一下最佳解，是用除的（最直覺的方式），果然都是 O(n) 的話做加減乘除運算還是最快的

## 作法
### 字串倒反法
Runtime: 4 ms (52.93%)
Memory Usage: 5.9 MB (72.61%)
```C++
class Solution {
public:
    int reverse(int x) {
        string s = to_string(x);
        string rvs = s;
        for (int i = s.length() - 1; i > -1; --i) {
            rvs[s.length() - 1 - i] = s[i];
        }   
        long ans = stol(rvs);
        if (rvs[rvs.length()-1] == '-')
            ans = ans * -1;
        return (ans > INT_MAX || ans < INT_MIN) ? 0 : ans;
    }
};
```
### 最佳解（除法）
Runtime: 0 ms
Memory Usage: 5.9 MB
```C++
class Solution {
public:
    int reverse(int x) {
        long ans = 0;
        while (x) {
            ans = ans*10 + x%10;
            x /= 10;
        }
        return (ans > INT_MAX || ans < INT_MIN) ? 0 : ans;
    }
};
```