## LeetCode-4 最长回文子串

`findPalindrome()`函数作为辅助作用，用于寻找回文子串的长度以及位置，然后通过一个for循环来遍历所有字符并向该字符两端进行发散寻找最长的回文串，并用`start`和`end`来标识回文串出现的位置，`end-start`还可用于标识长度，不过注意`end`和`start`在求取的时候`start = i-(maxLen-1)/2`（针对aba和abba类型—统一适用）。

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int start=0, end=0;
        for(int i=0; i<s.size(); ++i) {
            int aba = findPalindrome(s, i, i); // aba类型
            int abba = findPalindrome(s, i, i+1); // abba类型
            int maxLen = max(aba, abba);
            if(maxLen>end-start) {
                end = i+maxLen/2;
                start = i-(maxLen-1)/2;
            }
        }
        return s.substr(start, end-start+1);
    }

    // 判断字符串是否回文，返回长度
    int findPalindrome(string& s, int i, int j) {
        while(i>=0&&j<s.size()&&s[i]==s[j]){
            i--, j++;
        }
        // 返回回文串长度
        return j-i-1;
    }
};
```