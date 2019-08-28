# 109. Convert Sorted List to Binary Search Tree

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

**Example:**

    Given the sorted linked list: [-10,-3,0,5,9],

    One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

          0
         / \
       -3   9
       /   /
     -10  5

#### 題意：

給一串列，節點值已經過排序(遞增) 求出一可能的 height-balanced binary tree

#### 思路：

昨天才解過一個分治法的題目，想了一下後馬上寫出，只是效能還可以改善就是了。
特別注意的地方是mid值要(left+right+1)/2 補正偶數個數和奇數個數的差異

#### 參考code：
```cpp
class Solution {
public:
    TreeNode* sortedListToBST(ListNode* head) 
    {
        vector<int> vAns;
        ListNode* pCurr = head;
        while(pCurr)
        {
            vAns.push_back(pCurr->val);
            pCurr = pCurr->next;
        }
        return DivConquer(vAns,0,vAns.size()-1);
    }
private:
    TreeNode* DivConquer(vector<int>& nums,int left,int right)
    {
        if(left > right)
            return nullptr;
        int mid = (left+right+1)/2;
        TreeNode* pRoot = new TreeNode(nums[mid]);
        pRoot->left = DivConquer(nums,left,mid-1);
        pRoot->right = DivConquer(nums,mid+1,right);
        return pRoot;
    }
};
```
Runtime: 32 ms, faster than 44.21%

Memory Usage: 24.6 MB, less than 50.00%
