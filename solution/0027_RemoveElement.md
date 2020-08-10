# 0027_RemoveElement 
## 想法
同 26., 用 pointer 記錄更新後的數字就好
## 作法
```C++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int count = 0;
        for (int i = 0; i < nums.size(); ++i) {
            if (nums[i] != val)
                nums[count++] = nums[i];
                
        }
        return count;
    }
};
```
