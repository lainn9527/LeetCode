# 0034_FindFirstAndLastPositionOfElementIn SortedArray
## 想法
先用 binary search 找到 target 的某個點，再從該點分別往往頭 & 尾做 binary search
## 作法
Runtime: 16 ms (92.64%)
Memory Usage: 13.9 MB (29%)
```C++
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int id = bs(nums, 0, nums.size()-1, target);
        if (id == -1)
            return {-1, -1};
        int head = id, tail = id;
        while ( (head-1) >= 0 && nums[head-1] == target)
            head = bs(nums, 0, head-1, target);
        while ( (tail+1) < nums.size() && nums[tail+1] == target)
            tail = bs(nums, tail+1, nums.size()-1, target);
        return {head, tail};
    }
    
private:
    int bs(vector<int>& nums, int start, int end, int target) {
        while (start <= end) {
            int mid = (start + end)/2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] > target) end = mid-1;
            else start = mid+1;
        }
        return -1;
    }
};

```
