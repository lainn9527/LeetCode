# 0035_SearchInsertPosition 
## 想法
先用 binary search 找 target，因為沒有重複的找到就能 return 那個點，若沒找到 target，則插在最後的 mid 前 or 後，而該 mid 因為停止條件的關係會出現 `..., low, high, ...` 情況，此時要插入的點就會落在 `m=(low+high)/2` 或後面一個
## 作法
Runtime: 8 ms （94.06%)
Memory Usage: 9.9 MB (17.14%)
```C++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int start = 0, end = nums.size()-1;
        while (start <= end) {
            int mid = (start + end)/2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] > target) end = mid-1;
            else start = mid+1;
        }
        int m = (start + end)/2;
        if (nums[m] > target)
            return m;
        else
            return m + 1;
    }
};

```
