# 0026_RemoveDuplicatesFromSortedArray
## 想法
最後前 n 個要為不同的數，可用一個 pointer 記錄前 i 個相異的數，可在 O(n) 完成
## 作法
```C++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.empty())
            return 0;        
        int ni = 0;
        for (int i = 1; i < nums.size(); ++i) {
            if (nums[i] != nums[i-1])
                nums[++ni] = nums[i];
        }
        return ++ni;
    }
};

```


