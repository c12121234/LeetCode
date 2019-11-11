# 206. Reverse Linked List

Reverse a singly linked list.

**Example:**

    Input: 1->2->3->4->5->NULL
    Output: 5->4->3->2->1->NULL

**Follow up:**
A linked list can be reversed either iteratively or recursively. Could you implement both?

#### 思路:

經典題型，反轉linklist，一定要會的

只是單純反轉的話，不需要假定頭節點，存下next的pointer即可

最後遞移關係，注意while迴圈是以pCurr為條件，因此跳出迴圈必定為nullptr

故必須返還pPrev的值

以下兩種方式參考:

#### 參考code:

```cpp
class Solution 
{
public:
    ListNode* reverseList(ListNode* head) 
    {
        ListNode* pCurr = head;
        ListNode* pNext = nullptr;
        ListNode* pPrev = nullptr;
        while(pCurr)
        {
            pNext = pCurr->next;
            pCurr->next = pPrev;
            pPrev = pCurr;
            pCurr = pNext;
        }
        
        return pPrev;
    }
};
```

Runtime: 4 ms, faster than 98.90%

Memory Usage: 9.1 MB, less than 98.47%

```cpp
class Solution 
{
public:
    ListNode* reverseList(ListNode* head) 
    {
        ListNode* pPrev = nullptr;
        return DFS(head,pPrev);
    }
private:
    ListNode* DFS(ListNode* head,ListNode* prev)
    {
        if(head == nullptr)
            return prev;
        ListNode* pNext = head->next;
        head->next = prev;
        prev = head;
        return DFS(pNext,prev);
    }
};
```

Runtime: 8 ms, faster than 77.60%

Memory Usage: 9.3 MB, less than 46.56%
