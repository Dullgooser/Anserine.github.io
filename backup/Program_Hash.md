# 哈希表
## 两数之和
这道题给我做的完全没有思路，大概是因为我之前基本上不怎么使用map的原因，从这道题可以看出map我完全不会用。
但是map特别是unorderedmap是一个很强大的查找工具，所以还是不能轻视
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map <int,int> m;
        for(int i = 0; i < nums.size(); i++){
            auto x = m.find(target - nums[i]);
            if(x != m.end()){
                return {x->second, i};
            }
            else{
                m.insert(pair<int, int>(nums[i], i));
            }
        }
        return {};
    }
};
```