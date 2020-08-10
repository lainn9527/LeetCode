# 0036_ValidSudoku
## 想法
先構建 3 個一維 array[81] 分別紀錄 row, column, sub-box 的 9 個(row, column, sub-box) 1-9 是否 valid
稍微想一下就能知道個別的表示方法

## 作法
Runtime: 32 ms (90.98%)
Memory Usage: 18.1 MB (81.18%)
```C++
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        vector<bool> r(81, 0), c(81, 0), s(81, 0);
        for (int i = 0; i < 9; ++i) {
            for (int j = 0; j < 9; ++j) {
                if (board[i][j] == '.')
                    continue;
                int num = int(board[i][j] - '0') - 1;
                if (r[i*9+num] || c[j*9+num] || s[(i/3) * 27 + (j/3)*9 + num])
                    return false;
                r[i*9+num] = c[j*9+num] = s[(i/3) * 27 + (j/3)*9 + num] = true;
            }
        }
        return true;
    }
};

```