# 0039_CombinationSum
## 想法
先對 candidates 做 sort，再用 backtrack 由小到大去遞迴。
## 作法
Runtime: 4 ms (98.91%)
Memory Usage: 11.1 MB (64.03%)
```C++
class Solution {
public:
    
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        vector<int> pv;
        vector<vector<int> > ans;
        rec(candidates, target, 0, pv, ans);
        return ans;
        
    }

private:
    void rec(vector<int>& comb, int t, int p, vector<int>& pv, vector<vector<int> >& ans) {
        if (p >= comb.size() || t < comb[p])
            return;
        pv.push_back(comb[p]);        
        if (t == comb[p]) {
            ans.push_back(pv);
            pv.pop_back();
            return;
        }
        else
            rec(comb, t-comb[p], p, pv, ans);
        pv.pop_back();
        rec(comb, t, p+1, pv, ans);
    }
};
    

    
```

