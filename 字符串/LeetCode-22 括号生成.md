## LeetCode-22 括号生成（middle）


首先想到括号匹配的原则，只要右括号左边的左括号数量大于等于右括号的数量，那么就可以构成括号对，基于这个想法写出如下的回溯算法：
（1）判断条件就是括号数量，右括号数量不能多于左括号且左右括号都不能多于给定的n；
（2）每次递归调用就加上左括号或者右括号进行下一级递归。


```cpp
class Solution {
public:
    vector<string> res;
    vector<string> generateParenthesis(int n) {
        // 右括号的左边括号个数必须大于等于右括号的数量
        string s="";
        backTrace(s, 0, 0, n);
        return res;
    }v

    /*
    @s 字符串
    @left 当前左括号数量
    @right 当前右括号数量
    @target ==n代表左或右括号最大数量
    */
    void backTrace(string s, int left, int right, int target) {
        if(left < right || left > target || right > target) return;
        if(left==target&&right==target){
            res.push_back(s);
            return;
        }
        backTrace(s+'(', left+1, right, target);
        backTrace(s+')', left, right+1, target);
        return;
    }
};
```
---------------
### 小插曲
第一次写回溯算法，在最开始写这段代码的时候写出了一个小BUG，我在递归调用的地方对left和right并不是以`+1`的形式传递下一层参数，而是采用`++left`自增的方式，导致结果错误，DEBUG才发现在自增之后由于两个迭代是连续的，#1中自增的left会以`left+1`的形式传递进入#2调用，导致结果一直不对。
```cpp
backTrace(s+'(', ++left, right, target); // #1
backTrace(s+')', left, ++right, target); // #2
```
