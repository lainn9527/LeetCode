# 0011_ContainerWithMostWater
## 想法
這次也是靠自己想出最佳解！
因為意識到是由高度最小的決定容量，因此設立頭尾 2 個 pointer，計算容量後，移動高度較小的，一直到 2 個重合就找到了


## 作法
Runtime: 28 ms (91.27%)
Memory Usage: 14.3 MB (50.46%)
```C++
class Solution {
public:
    int maxArea(vector<int>& height) {
        auto head = height.begin(), tail = --height.end();
        int mc = 0;
        while (head != tail) {
            if (*head >= *tail)
                mc = max((*tail) * int(tail-- -head), mc);
            else
                mc = max((*head) * int(tail-head++), mc);
        }
        return mc;
    }
};
```