## LeetCode-75 颜色分类

一遍指针遍历，`left`左指针指向0填充的位置，`right`右指针指向2填充的位置，`cur`指向当前元素，那么循环分为三种情况：
（1） 当`nums[cur]==0`时，这时候需要将`cur`位置和`left`指向的位置交换元素，并自增`left`和`cur`，此时，left左边的元素都已经有序；
（2） 当`nums[cur]==1`时，这时候可以不予理会直接递增`cur`指针，因为当遍历到后面的0时，会对这个1再进行交换，而如果后面没有0了，那么表示这个1的位置正确，不需要处理；
（3） 当`nums[cur]==2`时，这时候对`cur`和`right`指针进行交换，交换后递减`right`指针，但是不递增`cur`指针，这是因为right指针原本指向的位置的元素是`cur`没有遍历到的，也就是没有处理过的，这时需要`cur`保持原位继续对这个元素进行处理。
同时需要注意循环的退出条件为`cur<=right`，因为在cur左边的所有数据都已处理完，在`right`右边的数据也都已处理完。



```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int left=0, right=nums.size()-1, cur=0;

        while(cur<=right) {
            if(nums[cur]==0){
                swap(nums[cur++], nums[left++]);
            }
            else if(nums[cur]==2) {
                swap(nums[cur], nums[right--]);
            }
            else{
                cur++;
            }
        }
    }
};
```