# 0017_LetterCombinationsOfAPhoneNumber
## 想法
這種排列組合的題目，就用 for-loop + 遞迴解決
## 作法
Runtime: 0 ms (這題好像壞掉了，大家都差不多)
Memory Usage: 6.3 MB
```C++
class Solution {
public:
    string dtl[10] = {
            "",
            "",
            "abc",
            "def",
            "ghi",
            "jkl",
            "mno",
            "pqrs",
            "tuv",
            "wxyz",
    };
    void recur(vector<string> &v, string &d, string t, int i) {
        if (i == d.length()) {
            v.push_back(t);
            return;
        }
        int digit = d[i] - '0';
        if (digit < 2 || digit > 9) {
            return recur(v, d, t, ++i);
        }
        string letter = dtl[digit];
        for (int j = 0; j < letter.size(); ++j) {
            recur(v, d, t+letter[j], i+1);
        }
        return;
    }
    vector<string> letterCombinations(string digits) {
        int s = digits.length();
        vector<string> vec;
        if (s > 0)
            recur(vec, digits, "", 0);
        return vec;
        
    }
};
```