# 2. Add Two Numbers

You are given **two non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

    Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
    Output: 7 -> 0 -> 8
    Explanation: 342 + 465 = 807.
    
#### 題意：

給予兩個非空串列表達兩非負整數，數字會以反序方式呈現。

兩個數字皆不會有以0開頭，除了0。

#### 思路：

簡單的串列操作，此題重點為必須宣告一個進位變數(bCarry)

其他的就遍巡串列來操作即可。

另外這題已經很好心只要反序即可，基本上不難。

#### code參考：

```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) 
    {
        bool bCarry = false;
        ListNode* pRoot = new ListNode(0);
        ListNode* pAns = pRoot;
        while(l1 || l2 || bCarry)
        {
            int sum =  ((l1 == nullptr)? 0 :(l1->val)) + ((l2 == nullptr)? 0 :(l2->val)) + bCarry;
            bCarry = sum >= 10 ? true : false;
            sum %= 10;
            pAns->next = new ListNode(sum);
            pAns = pAns->next; 
            if(l1)
                l1 = l1->next;
            if(l2)
                l2 = l2->next;
        }
        return pRoot->next;
    }
};
```

Runtime: 24 ms, faster than 63.63%

Memory Usage: 10.5 MB, less than 42.86% 


不過只贏63%，應該是還有許多地方可以改善。
