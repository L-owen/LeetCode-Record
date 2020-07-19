## LeetCode-1 两数之和

最容易想到利用`O(n)`的复杂度先遍历一遍数组建立一个hash表，保存数组值和下标，第二遍遍历再对每个元素去查询hash表，找到出现的等于`target-nums[i]`的数并返回。

进一步分析可以发现由于当两个数a和b满足要求时，如果a在前b在后，由于a+b=b+a，那么可以先把a加入hash表，待遍历到b的时候再查询hash表找到a，这样便可以完成在一次遍历中查询到两个数，优化了时间复杂度。

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        // 用一个map来保存之前出现的数和下标
        // 由于有a+b=b+a的性质
        // 一次遍历就能找到数对，边遍历边查询
        vector<int> res;
        unordered_map<int, int> numMap;

        for(int i=0; i<(int)nums.size(); ++i){
            if(numMap.find(target-nums[i]) != numMap.end() && i!=numMap[target-nums[i]]){     
                return {numMap[target-nums[i]], i};
            }
             // 遍历的同时把当前数字加入map
            numMap[nums[i]] = i;
        }

        return res;
    }
};
```





