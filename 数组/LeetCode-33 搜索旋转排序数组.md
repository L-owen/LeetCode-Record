## LeetCode-33 搜索旋转排序数组

因为题目要求时间复杂度为`O(logn)`，因此想到二分查找，只不过这里数组旋转了一下，需要稍微改动一下二分查找的思路，多一层判断条件，不过基本思想还是不变的。
拿题目给的数组举例`[4,5,6,7,0,1,2]`，中间元素是`7`，如果我们查询元素`0`，那么首先判断`nums[mid]`和`nums[left]`之间的大小，显然`nums[mid]>nums[left]`说明数组前半段是升序序列，接着比较`target`和`nums[mid]`以及`nums[left]`之间的关系，显然`target(0)`不在区间`[4,5,6,7]`中，那么修改'left=mid+1'，然后再重复上述步骤在曲建忠进行查找，直到'left>=right'

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left=0, right=nums.size()-1;

        while(left<=right) {
            int mid=left+(right-left)/2;
            if(nums[mid]==target) return mid;
             // 先根据 nums[mid] 与 nums[left] 的关系判断 mid 是在左段还是右段 
            if (nums[mid]>=nums[left]) {
                // 再判断 target 是在 mid 的左边还是右边，从而调整左右边界 left和 right
                if (target>=nums[left] && target<nums[mid]) {
                    right=mid-1;
                } else {
                    left=mid+1;
                }
            } else {
                if (target>nums[mid] && target<=nums[right]) {
                    left=mid+1;
                } else {
                    right=mid-1;
                }
            }
        }
        return -1;
    }
};
```