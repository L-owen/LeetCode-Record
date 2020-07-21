## LeetCode-2 无重复的最长子串

采用两种方法，但两种方法都是滑动窗口的思路，第二种方法比较好想，具体讲一下方法一的思路：
利用一个数组或者hash表来记录每个字符在`end`指针之前出现的位置（可以全部初始化为-1），`start`则代表靠前位置的指针，在窗口滑动的过程中，如果发现当前（end指针指向的字符，记为`c=s[end]`）在数组或者hash表中的值（代表的是`c`字符最后出现的位置）是大于等于`start`指针所指向的位置，那么说明c这个字符在`[start, end)`区间中也出现过，和`end`位置重复了，这个时候就需要去更新指针的位置，将`start`指针指向c出现的位置后一位，那么在子串区间`[start+1, end]`中c就只出现了一次，满足要求，并更新一下`len=end-start`，继续进行比较。


### 方法一
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int start=0, end=0, maxLen=0, len=0;
        // 用来保存每个数字最后一次出现的位置
        // 初试化为-1，当做字符在第-1的位置出现
        vector<int> wordsLoc(128, -1);

        while(end<s.size()) {
            char c=s[end];
            // 如果当前字符出现在start之后的某个位置，即重复
            // 那么可以将start直接更新到之前出现的位置之后
            if(wordsLoc[c-'\0'] >= start) {
                start=wordsLoc[c-'\0']+1;
                len=end-start;
            }
            // 更新当前字符出现的位置
            wordsLoc[c-'\0']=end;
            // 注意这里len需要自增，不论是否进入if条件
            maxLen=max(maxLen, ++len);
            end++;
        }

        return maxLen;
    }
};
```

### 方法二
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int maxLen=0, tmp=0;
        vector<int> wordsCnt(128, 1);
        int i=0, j=0; // 双指针

        while(j<s.size()) {
            // 当前字符还未使用过
            if(wordsCnt[s[j]-'\0'] == 1) {
                wordsCnt[s[j]-'\0']--;
                j++, tmp++;
            } else {
                maxLen = max(maxLen, tmp);
                wordsCnt[s[i]-'\0']++;
                // 慢指针后移，并重置计数
                i++, tmp--;
            }
        }
        maxLen=max(maxLen, tmp);
        
        return maxLen;
    }
};
```