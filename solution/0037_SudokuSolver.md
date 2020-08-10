# 0037_SudokuSolver
## 想法
用了比較慢的 backtrack，用 row major 的方式前進。
valid list 會根據目前 board 上有的去製作。
遇到未填的格子，則用該格中所有 valid number 去遞迴往下，直到找到解答。
真 D 慢，但對數獨來講其實夠了啦！
## 作法
Runtime: 72 ms (23.18%)
Memory Usage: 10.8 MB (17.34%)
```C++
class Solution {
public:
    void solveSudoku(vector<vector<char>>& board) {
        // vector< vector<vector<bool>>> valid(9, vector< vector<bool>> (9, vector<bool> (9, 0)));
        solver(board, 0, 0);
    }
private:
    bool solver(vector<vector<char>>& board, int i, int j) {
        if (i == 9)
            return true;
        if (j == 9)
            return solver(board, i+1, 0);
        if (board[i][j] != '.')
            return solver(board, i, j+1);
        
        vector<bool> vl = valid_list(board, i, j);
        for (int k = 1; k < 10; ++k) {
            if (!vl[k])
                continue;
            board[i][j] = k + '0';
            if (solver(board, i, j+1))
                return true;            
        }
        board[i][j] = '.';
        return false;
        
    }
    vector<bool> valid_list(vector<vector<char>>& board, int i, int j) {
        vector<bool> valid(10, 1);
        for (int k = 0; k < 9; ++k) {
            if (board[i][k] != '.')
                valid[int(board[i][k] - '0')] = 0;
            if (board[k][j] != '.')
                valid[int(board[k][j] - '0')] = 0;
            if (board[i - i%3 + k/3][j - j%3 + k%3] != '.')
                valid[int(board[i - i%3 + k/3][j - j%3 + k%3]) - '0'] = 0;
        }
        return valid;
    }
};

```


