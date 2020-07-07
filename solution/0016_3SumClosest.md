# 0016_3SumClosest
## 想法
和 0015 差不多的作法，應該還能更快就是了
## 作法
Runtime: 16 ms (65.66%)
Memory Usage: 9.8 MB (56.09%)
```C++
#include <stdlib.h>
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());
        int minv = INT_MAX, c = INT_MAX;
        for (int i = 0; i < nums.size(); ++i) {
            int head = i+1, tail = nums.size()-1;
            
            while (head < tail) {                
                int sum = nums[i] + nums[head] + nums[tail];
                if (minv > abs(target - sum)) {
                    c = sum;
                    minv = abs(target - sum);
                }
                if (sum < target)
                    ++head;
                else if (sum > target)
                    --tail;
                else
                    return target;
            }
            
        }
        return c;
    }
};


```