# 0033_SearchInRotatedSortedArray
## 想法
先用 binary search 找到 pivot (就是旋轉點)，這個點會是最小的點，所以以它為 begin, 又因為 index 超過 vector size，要以 (pivot + vector size - 1) % vector size 為 end 進行 binary search。

例如範例的 `[4,5,6,7,0,1,2]`，就以用 low = 4 (0), high = (4+7-1) % 7 = 3 (7) 去做 binary search
## 作法
Runtime: 8 ms (71%)
Memory Usage: 11.9 MB (44%)

```C++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int low = 0, high = nums.size() - 1;
        
        while (low < high) {
            int mid = (low + high) / 2;
            if (nums[mid] > nums[high])
                low = mid + 1;
            else
                high = mid;
        }
        
        int pivot = low;
        low = pivot, high = pivot + nums.size() - 1;
        
        while (low <= high) {
            int mid = (low + high) / 2;
            int vmid = (low + high) / 2 % nums.size();
            if (nums[vmid] == target)
                return vmid;
            else if (nums[vmid] > target)
                high = mid - 1;
            else
                low = mid + 1;
        }
        return -1;
    }
};
```
## 學習
### binary search
binary search 到底要 low = mid + 1 還是 low = mid 就好之類的問題
```
[1 3 5 8 9 10 14] target = 7
while low <= high
    mid = (low + high) / 2
    if v[mid] == target: return mid
    else if v[mid] > target: high = mid - 1
    else if v[mid] < target: low = mid + 1
```
```
low high mid value
0    6    3    8
0    2    1    3
2    2    2    5
3    2    *    *
```
```
[1 3 5 8 9 10 14] target = 7
while low <= high
    mid = (low + high) / 2
    if v[mid] == target: return mid
    else if v[mid] > target: high = mid - 1
    else if v[mid] < target: low = mid
```
```
low high mid value
0    6    3    8
0    2    1    3
1    2    1    3
1    2    *    * -> infibite loop
```
```
[1 3 5 8 9 10 14] target = 7
while low < high
    mid = (low + high) / 2
    if v[mid] == target: return mid
    else if v[mid] > target: high = mid
    else if v[mid] < target: low = mid + 1
```
```
low high mid value
0    6    3    8
0    3    1    3
2    3    2    5
3    3    3    8 -> infinite loop, nedd low < high
```