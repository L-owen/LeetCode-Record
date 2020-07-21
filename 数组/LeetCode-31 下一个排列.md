## LeetCode-31 下一个排列


```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        // 升序的数为最小字典排列 例如12345
        // 降序的数为最大字典排列 例如54321
        // 对于又升又降的数 例如 423521 
        // 先逆向从后到前找到第一个打破升序规则的数字 然后和其后面的比它大的数字中最小的进行交换
        // e.g. 423521找到第一个打破升序的3和之前的5交换 得到425321
        // 可以把425321看成两部分 由于425>423已经确定了，因此需要将后半部分改为最小字典序 也就是升序 123
        // 最终得到425123

        // 逆向找到第一个打破升序的数
        int pos=nums.size()-1; 
        
        // 从后往前遍历找到第一个打破升序的数
        while(pos>0 && nums[pos]<=nums[pos-1]){
            --pos;
        }
        if(pos==0){
            reverse(nums.begin(), nums.end());
            return;
        }

        // 在遍历过的数字中找到比该数大的最小的数并交换
        int greaterMin=nums[pos-1], idx=pos;
        for(int i=pos; i<nums.size(); ++i) {
            if(nums[i]>nums[pos-1]) {
                idx=i;
            }
            else break;
        }
        // 交换数字，且交换后后方数字仍保持降序排列
        swap(nums[pos-1], nums[idx]);
        reverse(nums.begin()+pos, nums.end());
        return;
    }
};
```