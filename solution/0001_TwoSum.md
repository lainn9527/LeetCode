# 想法
暴力解為 O(n^2)，有看到提示說可用 hash，但因為對這個東西不熟所以沒辦法想到解答。

## 為什麼會對 hash 不熟呢？
因為一直以來遇到 hash 都有這個問題，因此來紀錄一下

我對 hash 的理解就是 hash(a) = b, 之後只要 hash(n) = b 的話, 代表 n = a

## 那這樣的 hash 有什麼好處呢？
在於說找「是否能快速找到有 b」，hash 可以在 constant time 內做到這件事

## 那如何用在該題目上？
目標是 target - v[i]，把其存入 hash 中，
之後只要只要 hash(v[i+j]) 存在，就代表 taget = v[i] + v[i+j]，就可以 return 了

重點在於找到 target 的速度！

# 解法
## 暴力解
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> answer(2);
        for(auto i = nums.begin(); i != nums.end(); ++i) {
            int t = target - (*i);
            int flag = -1;
            cout << *i << endl;
            for(auto j = i+1; j != nums.end(); ++j ) {
                if((*j) == t) {
                    flag = j - nums.begin();
                    cout << *j << endl;
                    break;
                }
            }
            if (flag != -1) {
                answer[0] = i - nums.begin();
                answer[1] = flag;
                break;
            }
                
        }
        return answer;
        
    }
};
```
## 使用 hash 快速解
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int>h;
        for (auto i = nums.begin(); i != nums.end(); ++i) {
            int t = target - *i;
            if (h.find(t) != h.end()) {
                return {h[t], static_cast<int>(i-nums.begin())};
            }
            else {
                h[*i] = i - nums.begin();
            }
            
        }
        return {};
        
    }
};
```
# 學習
## vector
### vector iteration
用 C++ 的 vector 時，總是會被困擾，因為有太多 iterate 的方法，看了一下 stackoverflow [1]，發現關鍵在於
1. check boundary
無須多言
2. flexibility
再轉到其他 container 如 list, map 時能無痛轉換

#### iterate 方法如下

1. 傳統型
```
for (int i = 0; i < v.size(); ++i)
    cout << i << endl;
```
2. iterator
```
for (auto it = v.begin(); it != v.end(); ++it) {
    cout << *it << endl;
}
```
3. 更精簡版
```
for (auto i: v)
    cout << i << endl;
```
基本上用 2. 就好，但問題來了，如果要取得 index 時呢？

## iterator with index
根據 [2]
1. 最速版本
`index = it - v.begin()`
2. flexibility
`index = std::distance(v.begin(), it)`
這個也可用在像 list 這種非 random access 的，不過比較慢就是了

## hash in C++

### unordered_map
[API](http://www.cplusplus.com/reference/unordered_map/unordered_map/)
為無序儲存，可以做到 key-value 的架構，例如 `um[i] = j`，這樣 i = key, j = value
之後就能 `um.find(i)` 來看是否有該 key 值存在

### unordered_set
[API](http://www.cplusplus.com/reference/unordered_set/unordered_set/)
為無序儲存，結構是 key = value，因此只能 `us.insert(element)`




# Reference
[1] https://stackoverflow.com/questions/12702561/iterate-through-a-c-vector-using-a-for-loop
[2] https://stackoverflow.com/questions/2152986/what-is-the-most-effective-way-to-get-the-index-of-an-iterator-of-an-stdvector
