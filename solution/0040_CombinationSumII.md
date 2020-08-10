# 0040_CombinationSumII
## 想法
和 I 差不多，只是每個 number 有次數限制，超過就只能往下
## 作法
(code 有點醜，待改)
Runtime: 8 ms (90.22%)
Memory Usage: 13.2 MB (30.37%)
```C++
class Solution {
public:
    
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        map<int, int> count;
        for (int i = 0; i < candidates.size(); ++i) {
            ++count[candidates[i]];
        }
        vector<int> pv;
        vector<vector<int> > ans;
        rec(count, target, count.begin(), pv, ans);
        return ans;
        
    }

private:
    void rec(map<int, int>& comb, int t, map<int,int>::iterator it, vector<int>& pv, vector<vector<int> >& ans) {
        if (it->second == 0)
            ++it;
        if (it == comb.end() || t < it->first)
            return;
        pv.push_back(it->first);
        --it->second;
        if (t == it->first) {
            ans.push_back(pv);
            pv.pop_back();
            ++it->second;
            return;
        }
        else {
            rec(comb, t - it->first, it, pv, ans);
            pv.pop_back();
            ++it->second;
            if (++it != comb.end())
                rec(comb, t, it, pv, ans);            
        }
    }
};

```