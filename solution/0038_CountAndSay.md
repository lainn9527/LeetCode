# 0038_CountAndSay
## 想法
因為是固定的，所以就從 i=1 按照規律一直到 i=n
## 作法
Runtime: 4 ms (88.14%)
Memory Usage: 6.2 MB (95.34%)
```C++
class Solution {
public:
    string countAndSay(int n) {
        string f = "1";
        for(int i = 2; i <= n; ++i) {
            string nf;
            for (int j = 0; j < f.size(); ++j) {
                int l = 1;
                while (j+1 < f.size() && f[j+1] == f[j])
                    ++l, ++j;
                nf += to_string(l) + f[j];
                
            }
            f = nf;
        }
        return f;
    }
};
```
