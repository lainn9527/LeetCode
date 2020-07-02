# 0006_ZigZagConversion

## 想法
一開始想說建立一個 big table 按順序存下後，再按照題目要求的順序輸出，結果發現超麻煩，就開始尋找規律。
規律其實不複雜，畫個圖想一下就好，想法雖然對了，但離最佳解的 4ms 還是有差距，這就是代碼質量的差異嗎？

## 作法
Runtime: 20 ms (88.09%)
Memory Usage: 7.8 MB (94.99%)
```C++
class Solution {
public:
    string convert(string s, int numRows) {
        if (numRows == 1)
            return s;
        int n = 0;
        string h = s;
        for (int i = 0; i < s.size(); i+= 2*numRows-2) {
            h[n++] = s[i];
        }
        for (int i = 1; i < numRows-1 && i < s.size(); ++i) {
            h[n++] = s[i];
            for (int j = i+2*numRows-2-2*i; j < s.size(); j += 2*numRows-2-2*i) {
                h[n++] = s[j];
                j += 2*i;
                if (j < s.size())
                    h[n++] = s[j];
                else
                    break;
            }
        }
        for (int i = numRows-1; i < s.size(); i+= 2*numRows-2) {
            h[n++] = s[i];
        }
        return h;
    }
};
```

## 學習
string 可以直接家 string
快還可以再更快