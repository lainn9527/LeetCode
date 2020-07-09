# 0022_GenerateParentheses
## 想法

排列組合的想法都差不多，用遞迴解決
不過還是有更精簡的作法，而且不知道為啥速度就提升了，真他媽神奇

### DP
看了一下，竟然還有 DP 的作法
想法是有 n 組()，則給 1 組後，剩下 n-1 組排法如下：
()(...) n-1組在後面, 0 組在裡面
(())(...) n-2組在後面, 1 組在裡面
...
((...)) 0 組在後面, n-1 組在裡面

變成 (x)y 的形式，x + y = n-1 組
用 table[n] 存放所有可能，table[i] 表 n=i 時所有組合
此時 table[n] = { (x)y for x in table[i] for y in talbe [n-1-i] }, i=0->n-1
看起來很炫炮，但不知道快不快


## 作法
Runtime: 8 ms (52.78%)
Memory Usage: 15 MB (48.73%)

```C++
class Solution {
public:
    void recur(int na, int nb, string s, vector<string> &v) {
        if (na == 0 && nb == 0)
            return v.push_back(s);
        if (na == nb)
            return recur(na-1, nb, s+'(', v);
        
        if (na == 0)
            return recur(na, nb-1, s+')', v);
        recur(na-1, nb, s+'(', v);
        recur(na, nb-1, s+')', v);
        
    }
    vector<string> generateParenthesis(int n) {
        vector<string> v;
        recur(n, n, "", v);
        return v;
    }
};
```
### 更精簡（然後就加速了）
Runtime: 0 ms (100%)
Memory Usage: 14.9 MB (58.17%)
```C++
class Solution {
public:
    void recur(int na, int nb, string s, vector<string> &v) {
        if (na == 0 && nb == 0)
            return v.push_back(s);
        if (nb > 0) recur(na, nb-1, s+')', v);
        if (na > 0) recur(na-1, nb+1, s+'(', v);
        
    }
    vector<string> generateParenthesis(int n) {
        vector<string> v;
        recur(n, 0, "", v);
        return v;
    }
};
```