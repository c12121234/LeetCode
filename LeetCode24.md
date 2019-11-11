# 24. Swap Nodes in Pairs

Given a linked list, swap every two adjacent nodes and return its head.

You may **not** modify the values in the list's nodes, only nodes itself may be changed.

 

**Example:**

    Given 1->2->3->4, you should return the list as 2->1->4->3.
    
#### 思路:
做linklist類的題目時，通常都要假定一個頭節點來方便計算

遞移式的儲存節點 pointer

跳出迴圈的條件

以上都有思考到的話，此類題目都算簡單(想不到的就...想破頭都想不到)


#### 參考code:

```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) 
    {
        if(head == nullptr || head->next == nullptr)
            return head;
        ListNode* pRoot = new ListNode(0);
        ListNode* pCurr = head,*pPrev = pRoot;
        pRoot->next = pCurr;
        
        while(pPrev)
        {
            if(!pPrev->next || !pPrev->next->next)
                break;
            pCurr = pPrev->next;
            pPrev->next = pCurr->next;
            pCurr->next = pCurr->next->next;
            pPrev->next->next = pCurr;
            pPrev = pCurr;
        }
        return pRoot->next;
    }
};
```

Runtime: 4 ms faster than 68.64%

Memory Usage: 8.6 MB, less than 94.64%

時間複雜度為O(n)
