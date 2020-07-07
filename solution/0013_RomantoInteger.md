# 0013_RomantoInteger
## 想法
將 roman-integer 的對應關係列出來，再從頭開始檢查 string ，在對應關係中由大到小去比對，每個字比對到後，還要去 check 他後面一個字看是否為 IV, CM 等特殊 case。
可想而知這種方式一定很慢，因為每個字都要從對應關係中由大到小去比較。

另一種想法是用 hash 把 roman-integer 關係列出來，再從後面 `i=s.length()-2` 開始檢查，如果 `RI[i] < RI[i+1]`，代表這個是 4 or 9 開頭得，要剪掉 `RI[i]`，不然則是加上 `RI[i]`。這個方法超聰明的，但效率和我的差不
多而以
## 作法
### 繁瑣
Runtime: 40 ms (14.23%)
Memory Usage: 6 MB
```C++
class Solution {
public:
    int romanToInt(string s) {
        int num[] = {
            1,
            4,
            5,
            9,
            10,
            40,
            50,
            90,
            100,
            400,
            500,
            900,
            1000
        };
        string st[] = {
            "I",
            "IV",
            "V",
            "IX",
            "X",
            "XL",
            "L",
            "XC",
            "C",
            "CD",
            "D",
            "CM",
            "M"
        };
        int total = 0;
        for (int i = 0; i < s.length(); ++i) {
            int j = 12;
            while(j >= 0) {
                if (st[j].length()-1+i < s.length()) {
                    if (st[j] == s.substr(i, st[j].length())) {
                        total += num[j];
                        i += st[j].length()-1;
                        break;
                    }
                }
                --j;
            }
        }
        return total;
    }
};
```
### 簡潔聰明
```C++
class Solution {
public:
    int romanToInt(string s) {
        unordered_map<char, int> m = { { 'I' , 1 },
                                       { 'V' , 5 },
                                       { 'X' , 10 },
                                       { 'L' , 50 },
                                       { 'C' , 100 },
                                       { 'D' , 500 },
                                       { 'M' , 1000 } };
       int sum = m[s.back()];
       for (int i = s.length() - 2; i >= 0; --i)  {
           if (m[s[i]] < m[s[i + 1]]) {
               sum -= m[s[i]];
           }
           else {
               sum += m[s[i]];
           }
       }

       return sum;
    }
};
```
### 參考第一名
把 hash 變成 switch statement 並用 function 包起來，快了不少 (40ms -> 16ms)，但第一名的做法其實差不多，合理推測快到一定程度後 leetcode 都覺得差不多了
```C++
class Solution {
public:
    int value(char c){
        switch(c) {
                case 'I': return 1; break;
                case 'V': return 5; break;
                case 'X': return 10; break;
                case 'L': return 50; break;
                case 'C': return 100; break;
                case 'D': return 500; break;
                case 'M': return 1000; break;
        }
        return 0;
    }
    int romanToInt(string s) {
       int sum = value(s.back());
       for (int i = s.length() - 2; i >= 0; --i)  {
           if (value(s[i]) < value(s[i+1])) {
               sum -= value(s[i]);
           }
           else {
               sum += value(s[i]);
           }
       }

       return sum;
    }
};
```
    