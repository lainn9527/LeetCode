# 0020_ValidParentheses
## 想法
用 stack 就搞定了
## 作法
Runtime: 0 ms (100.00%)
Memory Usage: 6.2 MB (74.27%)
```C++
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        for (auto i : s) {
            if (i == '{' || i == '[' || i == '(')
                st.push(i);
            else if (!st.empty() &&
                     (st.top() == '{' && i == '}' ||
                     st.top() == '[' && i == ']' ||
                     st.top() == '(' && i == ')'))
                st.pop();
            else
                return false;
        }
        return st.empty();
    }
};
```
