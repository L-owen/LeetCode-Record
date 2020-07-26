## LeetCode-128 最长连续序列

题目标签是**并查集**，第一次做并查集的题目，直接按照题解的思路来写的。
（1）首先用一个`set`来存储数组中的元素并去重（方便后面查找）；
（2）先考虑一种情况，如果对于元素`x`来说存在`x,x+1,x+2,...`的序列，那么当查询`x-1`这个元素时，就会又把`x,x+1,x+2,...`重新查询了一遍，所以我们只需要在数组存在`x`而不存在`x-1`的情况进行查询，这样可以省去很多时间；
（3）遍历`set`对其中每一个元素先判断`x-1`存不存在（#1），如果存在则不需要查询这个数的值，如果不存在则表示如果此时存在最长序列，那么该数就是序列中的最小值，因此可以进入循环（#2）进行查询，并在循环结束后更新最大值。


```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> hashMap;
        for(const auto& num:nums) {
            hashMap.insert(num);
        }

        int longestLen=0;
        for(const auto& num:hashMap) {
            // 如果前一个值没有出现的话便可以从该值开始递增
            if(!hashMap.count(num-1)) {  // #1
                int curNum=num;
                int curLen=1;
                // 开始往后找存在的序列
                while(hashMap.count(curNum+1)){  // #2
                    curNum+=1;
                    curLen+=1;
                }
                longestLen=max(longestLen, curLen);
            }
        }

        return longestLen;
    }
};
```