# 0031_ NextPermutation
有演算法能根據 lexicographical order 產生下一個，根據 [wiki](https://en.wikipedia.org/wiki/Permutation#Generation_in_lexicographic_order)

## 想法
The following algorithm generates the next permutation lexicographically after a given permutation. It changes the given permutation in-place.

1. Find the largest index k such that a[k] < a[k + 1]. If no such index exists, the permutation is the last permutation.
2. Find the largest index l greater than k such that a[k] < a[l].
3. Swap the value of a[k] with that of a[l].
4. Reverse the sequence from a[k + 1] up to and including the final element a[n].
## 作法
```C++
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int k = nums.size()-1;
        while (--k >= 0 && nums[k] >= nums[k+1])
            ;
        if (k < 0)
            reverse(nums.begin(), nums.end());
        else {
            int l = nums.size();
            while (nums[--l] <= nums[k])
                ;
            swap(nums[k], nums[l]);
            reverse(nums.begin() + k + 1, nums.end());

        }
        
        
    }
};
```
