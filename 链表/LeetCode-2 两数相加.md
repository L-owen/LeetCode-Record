## LeetCode-2 两数相加

输入是两个链表`l1,l2`，且在链表中的数字是逆序排列的，表头代表个位数、第二个节点代表十位数以此类推，要求返回和的新链表。
由于加法运算是从个位数开始计算，且刚好输入的两个链表的头部都是个位数开始，那么可以直接对链表中的数字进行加法运算的模拟，在模拟过程中需要注意：
（1）可能存在进位，这时候可以设置一个标志位`carry`来标志有无进位产生，且加法运算的最大进位数为1；
（2）当两个链表长度不相等时，可以在短的那个链表尾部补0然后与长链表相加，继续模拟加法运算，这样就可以在一个while循环中将所有的节点都加起来；
（3）当while循环结束后，还需要判断最高位是否有进位，也就是while结束之后`carry`的值是否为1，如果是，那么需要新建一个节点来保存这个进位。

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        // 边界情况
        if(!l1) return l2;
        if(!l2) return l1;
        // 模拟整数加法，当链表为nullptr时可以用0来代替
        int carry=0;
        ListNode* pResult = new ListNode(0), *node = pResult;
        // 因为链表本身数字就是倒序的，可以从头开始直接相加，模拟进位
        while(l1||l2){
            int digit1=l1? l1->val:0;
            int digit2=l2? l2->val:0;
            int sum = digit1+digit2+carry;
            carry=sum/10;
            node->next = new ListNode(sum%10);
            node=node->next;
            if(l1) l1=l1->next;
            if(l2) l2=l2->next;
        }

        if(carry){
            node->next = new ListNode(1);
        }

        return pResult->next;
    }
};
```